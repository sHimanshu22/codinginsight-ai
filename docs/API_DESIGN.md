# CodingInsight AI - API Design

# 1. API Overview

Base URL:

/api/v1

The API follows REST principles and returns JSON responses.

Standard Response Format:

Success:

{
"success": true,
"message": "Operation successful",
"data": {}
}

Error:

{
"success": false,
"message": "Error message"
}

---

# 2. Authentication APIs

Base Route:

/api/v1/auth

---

## Register User

POST /auth/register

Request:

{
"name": "Himanshu",
"email": "[user@example.com](mailto:user@example.com)",
"password": "password123"
}

Response:

{
"success": true,
"message": "User registered successfully",
"data": {
"token": "jwt_token"
}
}

---

## Login User

POST /auth/login

Request:

{
"email": "[user@example.com](mailto:user@example.com)",
"password": "password123"
}

Response:

{
"success": true,
"message": "Login successful",
"data": {
"token": "jwt_token"
}
}

---

## Get Current User

GET /auth/me

Headers:

Authorization: Bearer JWT_TOKEN

Response:

{
"success": true,
"data": {
"user": {}
}
}

---

# 3. Coding Profile APIs

Base Route:

/api/v1/profiles

---

## Connect Profile

POST /profiles/connect

Request:

{
"platform": "leetcode",
"username": "coding_user"
}

Response:

{
"success": true,
"message": "Profile connected successfully"
}

---

## Get Connected Profiles

GET /profiles

Response:

{
"success": true,
"data": {
"profiles": []
}
}

---

## Sync Profile

POST /profiles/:id/sync

Purpose:

Fetch latest data from coding platform.

Response:

{
"success": true,
"message": "Profile synchronized"
}

---

## Remove Profile

DELETE /profiles/:id

Response:

{
"success": true,
"message": "Profile removed"
}

---

# 4. Dashboard APIs

Base Route:

/api/v1/dashboard

---

## Get Dashboard Data

GET /dashboard

Purpose:

Returns aggregated statistics from all platforms.

Response:

{
"success": true,
"data": {

```
  "totalSolved": 1200,

  "platforms": [],

  "contestRatings": [],

  "recentActivity": []
```

}
}

---

## Get Dashboard Summary

GET /dashboard/summary

Purpose:

Lightweight dashboard metrics.

Response:

{
"success": true,
"data": {

```
  "connectedPlatforms": 4,

  "totalSolved": 1200,

  "highestRating": 1800
```

}
}

---

# 5. Snapshot APIs

Base Route:

/api/v1/snapshots

---

## Get Historical Snapshots

GET /snapshots

Query Parameters:

?platform=leetcode

Response:

{
"success": true,
"data": {
"snapshots": []
}
}

---

## Get Growth Analytics

GET /snapshots/growth

Response:

{
"success": true,
"data": {
"growth": []
}
}

---

# 6. Goal APIs

Base Route:

/api/v1/goals

---

## Create Goal

POST /goals

Request:

{
"title": "Solve 500 Problems",
"targetValue": 500,
"deadline": "2026-12-31"
}

Response:

{
"success": true,
"message": "Goal created"
}

---

## Get Goals

GET /goals

Response:

{
"success": true,
"data": {
"goals": []
}
}

---

## Update Goal

PUT /goals/:id

Response:

{
"success": true,
"message": "Goal updated"
}

---

## Delete Goal

DELETE /goals/:id

Response:

{
"success": true,
"message": "Goal deleted"
}

---

# 7. AI Analysis APIs

Base Route:

/api/v1/analysis

---

## Generate Analysis

POST /analysis/generate

Purpose:

Generate AI report using latest profile data.

Response:

{
"success": true,
"data": {

```
  "readinessScore": 78,

  "strengths": [],

  "weaknesses": [],

  "recommendations": []
```

}
}

---

## Get Latest Analysis

GET /analysis/latest

Response:

{
"success": true,
"data": {
"report": {}
}
}

---

## Get Analysis History

GET /analysis/history

Response:

{
"success": true,
"data": {
"reports": []
}
}

---

# 8. Authentication Middleware

Protected Routes:

* Dashboard APIs
* Profile APIs
* Goal APIs
* Analysis APIs
* Snapshot APIs

Authentication Method:

JWT Bearer Token

Header:

Authorization: Bearer JWT_TOKEN

---

# 9. Error Handling

Common Errors:

400 Bad Request

401 Unauthorized

403 Forbidden

404 Not Found

500 Internal Server Error

Response Format:

{
"success": false,
"message": "Detailed error message"
}

---

# 10. API Versioning

Current Version:

v1

Example:

/api/v1/dashboard

Future Versions:

/api/v2/dashboard

This allows future upgrades without breaking existing clients.

---

# 11. Backend Service Mapping

Auth APIs

↓

AuthService

Profile APIs

↓

ProfileService

Dashboard APIs

↓

DashboardService

Goal APIs

↓

GoalService

Analysis APIs

↓

AnalysisService

This ensures clear separation of responsibilities and maintainable backend architecture.

---

# 12. Development Order

Phase 1:

1. Auth APIs
2. Profile APIs
3. Dashboard APIs

Phase 2:

4. Analysis APIs

Phase 3:

5. Snapshot APIs
6. Goal APIs

Phase 4:

7. Company Readiness APIs

This order minimizes complexity and allows incremental development.
