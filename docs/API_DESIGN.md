# CodingInsight AI - API Design

# 1. API Overview

Base URL:

/api/v1

The API follows REST principles and returns JSON responses.

Standard Success Response:

```json
{
  "success": true,
  "message": "Operation successful",
  "data": {}
}
```

Standard Error Response:

```json
{
  "success": false,
  "message": "Error message"
}
```

---

# 2. Authentication APIs

Base Route:

/api/v1/auth

---

## Register User

POST /auth/register

Request:

```json
{
  "name": "Himanshu",
  "email": "user@example.com",
  "password": "password123"
}
```

Response:

```json
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "token": "jwt_token",
    "user": {}
  }
}
```

---

## Login User

POST /auth/login

Request:

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

Response:

```json
{
  "success": true,
  "message": "Login successful",
  "data": {
    "token": "jwt_token",
    "user": {}
  }
}
```

---

## Get Current User

GET /auth/me

Response:

```json
{
  "success": true,
  "data": {
    "user": {}
  }
}
```

---

## Logout User

POST /auth/logout

Response:

```json
{
  "success": true,
  "message": "Logout successful"
}
```

---

# 3. Coding Profile APIs

Base Route:

/api/v1/profiles

---

## Connect Profile

POST /profiles/connect

Request:

```json
{
  "platform": "leetcode",
  "username": "coding_user"
}
```

Response:

```json
{
  "success": true,
  "message": "Profile connected successfully"
}
```

---

## Get Connected Profiles

GET /profiles

Response:

```json
{
  "success": true,
  "data": {
    "profiles": []
  }
}
```

---

## Get Profile Details

GET /profiles/:id

Response:

```json
{
  "success": true,
  "data": {
    "profile": {}
  }
}
```

---

## Sync Profile

POST /profiles/:id/sync

Purpose:

Fetch latest data from coding platform and update statistics.

Response:

```json
{
  "success": true,
  "message": "Profile synchronized successfully"
}
```

---

## Remove Profile

DELETE /profiles/:id

Response:

```json
{
  "success": true,
  "message": "Profile removed successfully"
}
```

---

# 4. Dashboard APIs

Base Route:

/api/v1/dashboard

---

## Get Dashboard Data

GET /dashboard

Purpose:

Returns all dashboard data required by the frontend.

Response:

```json
{
  "success": true,
  "data": {
    "user": {},
    "profiles": [],
    "analytics": {},
    "goals": [],
    "latestAnalysis": {}
  }
}
```

---

## Get Dashboard Summary

GET /dashboard/summary

Purpose:

Returns lightweight dashboard statistics.

Response:

```json
{
  "success": true,
  "data": {
    "connectedPlatforms": 2,
    "totalSolved": 1200,
    "highestRating": 1800,
    "consistencyScore": 78
  }
}
```

---

# 5. Analytics APIs

Base Route:

/api/v1/analytics

---

## Get Analytics

GET /analytics

Purpose:

Returns processed analytics generated from coding data.

Response:

```json
{
  "success": true,
  "data": {
    "consistencyScore": 80,
    "activityScore": 75,
    "contestPerformanceScore": 72,
    "strongestTopics": [],
    "weakestTopics": []
  }
}
```

---

## Get Growth Analytics

GET /analytics/growth

Purpose:

Returns historical growth information.

Response:

```json
{
  "success": true,
  "data": {
    "growth": []
  }
}
```

---

## Recalculate Analytics

POST /analytics/recalculate

Purpose:

Rebuild analytics using latest snapshots.

Response:

```json
{
  "success": true,
  "message": "Analytics recalculated successfully"
}
```

---

# 6. Snapshot APIs

Base Route:

/api/v1/snapshots

---

## Get Historical Snapshots

GET /snapshots

Query Parameters:

```text
?platform=leetcode
```

Response:

```json
{
  "success": true,
  "data": {
    "snapshots": []
  }
}
```

---

## Get Snapshot Details

GET /snapshots/:id

Response:

```json
{
  "success": true,
  "data": {
    "snapshot": {}
  }
}
```

---

# 7. Goal APIs

Base Route:

/api/v1/goals

---

## Create Goal

POST /goals

Request:

```json
{
  "goalType": "leetcode_problems",
  "platform": "leetcode",
  "targetValue": 500,
  "deadline": "2026-12-31"
}
```

Response:

```json
{
  "success": true,
  "message": "Goal created successfully"
}
```

---

## Get Goals

GET /goals

Response:

```json
{
  "success": true,
  "data": {
    "goals": []
  }
}
```

---

## Get Goal Details

GET /goals/:id

Response:

```json
{
  "success": true,
  "data": {
    "goal": {}
  }
}
```

---

## Update Goal

PUT /goals/:id

Response:

```json
{
  "success": true,
  "message": "Goal updated successfully"
}
```

---

## Delete Goal

DELETE /goals/:id

Response:

```json
{
  "success": true,
  "message": "Goal deleted successfully"
}
```

---

# 8. AI Analysis APIs

Base Route:

/api/v1/analysis

---

## Generate Analysis

POST /analysis/generate

Purpose:

Generate AI-powered coding profile analysis.

Response:

```json
{
  "success": true,
  "data": {
    "strengths": [],
    "weaknesses": [],
    "recommendations": [],
    "summary": ""
  }
}
```

---

## Get Latest Analysis

GET /analysis/latest

Response:

```json
{
  "success": true,
  "data": {
    "report": {}
  }
}
```

---

## Get Analysis History

GET /analysis/history

Response:

```json
{
  "success": true,
  "data": {
    "reports": []
  }
}
```

---

# 9. Company Readiness APIs

Base Route:

/api/v1/readiness

---

## Generate Readiness Report

POST /readiness/generate

Request:

```json
{
  "targetCompany": "Google"
}
```

Response:

```json
{
  "success": true,
  "data": {
    "readinessScore": 78,
    "metrics": {},
    "strengths": [],
    "weaknesses": [],
    "recommendations": []
  }
}
```

---

## Get Latest Readiness Report

GET /readiness/latest

Response:

```json
{
  "success": true,
  "data": {
    "report": {}
  }
}
```

---

## Get Readiness History

GET /readiness/history

Response:

```json
{
  "success": true,
  "data": {
    "reports": []
  }
}
```

---

# 10. Authentication Middleware

Protected Routes:

* Profile APIs
* Dashboard APIs
* Analytics APIs
* Snapshot APIs
* Goal APIs
* Analysis APIs
* Readiness APIs

Authentication Method:

JWT Bearer Token

Header:

```text
Authorization: Bearer JWT_TOKEN
```

---

# 11. Error Handling

Common Status Codes:

* 200 OK
* 201 Created
* 400 Bad Request
* 401 Unauthorized
* 403 Forbidden
* 404 Not Found
* 500 Internal Server Error

Error Response:

```json
{
  "success": false,
  "message": "Detailed error message"
}
```

---

# 12. API Versioning

Current Version:

```text
/api/v1
```

Future Versions:

```text
/api/v2
```

Versioning prevents breaking changes for future clients.

---

# 13. Backend Service Mapping

```text
Auth APIs
↓
AuthService

Profile APIs
↓
ProfileService

Dashboard APIs
↓
DashboardService

Analytics APIs
↓
AnalyticsService

Goal APIs
↓
GoalService

Analysis APIs
↓
AIAnalysisService

Readiness APIs
↓
ReadinessService
```

---

# 14. Development Order

Phase 1 (MVP)

1. Authentication APIs
2. Profile APIs
3. Dashboard APIs

Phase 2

4. Analytics APIs
5. Snapshot APIs

Phase 3

6. Goal APIs
7. AI Analysis APIs

Phase 4

8. Company Readiness APIs

This development sequence minimizes complexity and enables incremental feature delivery.
