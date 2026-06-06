# CodingInsight AI - System Architecture

# 1. Architecture Overview

CodingInsight AI follows a layered architecture consisting of:

1. Presentation Layer (Frontend)
2. API Layer (Backend)
3. Business Logic Layer
4. Data Access Layer
5. External Integration Layer
6. Database Layer

This separation improves maintainability, scalability, and code organization.

---

# 2. High Level System Diagram

```
                +-------------------+
                |      User         |
                +---------+---------+
                          |
                          v

                +-------------------+
                | React Frontend    |
                +---------+---------+
                          |
                          v

                +-------------------+
                | Express API       |
                +---------+---------+
                          |
      +-------------------+-------------------+
      |                   |                   |
      v                   v                   v
```

+----------------+  +----------------+  +----------------+
| Auth Service   |  | Profile Service|  | AI Service     |
+----------------+  +----------------+  +----------------+

```
      |                   |                   |
      +-------------------+-------------------+
                          |
                          v

                +-------------------+
                | MongoDB Database  |
                +-------------------+

                          ^
                          |
                          |

    +--------------------------------------------+
    | External Coding Platforms                  |
    |                                            |
    | - LeetCode                                |
    | - Codeforces                              |
    | - CodeChef                                |
    | - GeeksforGeeks                           |
    +--------------------------------------------+
```

---

# 3. Frontend Architecture

Technology Stack:

* React
* React Router
* Axios
* Tailwind CSS
* Recharts

Frontend Responsibilities:

* Authentication UI
* Dashboard UI
* Charts and Analytics
* Profile Management
* Goal Tracking
* AI Analysis Display

---

# 4. Frontend Folder Structure

frontend/

src/

├── components/

├── pages/

├── services/

├── hooks/

├── context/

├── layouts/

├── utils/

├── routes/

├── assets/

└── App.jsx

---

# 5. Backend Architecture

Technology Stack:

* Node.js
* Express.js
* MongoDB
* Mongoose
* JWT Authentication

Backend Responsibilities:

* User Authentication
* Data Validation
* Business Logic
* External API Communication
* AI Processing
* Analytics Generation

---

# 6. Backend Folder Structure

backend/

src/

├── config/

├── controllers/

├── services/

├── routes/

├── middleware/

├── models/

├── validators/

├── utils/

├── jobs/

└── app.js

---

# 7. Layer Responsibilities

## Routes Layer

Responsibilities:

* Receive HTTP requests
* Forward requests to controllers

Example:

GET /dashboard

POST /auth/login

POST /profiles/connect

---

## Controller Layer

Responsibilities:

* Request handling
* Input validation
* Response formatting

Controllers should contain minimal business logic.

---

## Service Layer

Responsibilities:

* Core business logic
* Data processing
* Aggregation logic
* Analytics generation

Examples:

AuthService

ProfileService

DashboardService

AnalysisService

---

## Model Layer

Responsibilities:

* Database schema definitions
* Data relationships

Implemented using Mongoose.

---

# 8. External Integration Layer

Purpose:

Communicate with coding platforms.

Services:

* LeetCode Service
* Codeforces Service
* CodeChef Service
* GeeksforGeeks Service

Responsibilities:

* Fetch profile data
* Normalize responses
* Handle API failures
* Handle rate limits

---

# 9. Data Flow

Profile Connection Flow:

User

↓

Frontend

↓

Backend API

↓

Profile Service

↓

Platform Service

↓

External Platform

↓

MongoDB

↓

Frontend Dashboard

---

# 10. AI Analysis Architecture

Input:

* Solved problems
* Contest ratings
* Topic distribution
* Historical progress

Processing:

* Generate insights
* Identify strengths
* Identify weaknesses
* Create recommendations

Output:

* Readiness score
* Recommendations
* Improvement roadmap

---

# 11. Dashboard Architecture

Dashboard Data Sources:

* User Information
* Connected Profiles
* Aggregated Statistics
* Historical Snapshots
* AI Reports

Displayed Using:

* Cards
* Tables
* Charts
* Progress Indicators

---

# 12. Security Architecture

Authentication:

* JWT Access Tokens

Password Security:

* bcrypt password hashing

API Protection:

* Authentication middleware

Input Security:

* Validation middleware

Environment Variables:

* Database URI
* JWT Secret
* AI Keys
* Platform Credentials

---

# 13. Scalability Considerations

The architecture should support:

* Additional coding platforms
* More AI modules
* More analytics features
* Mobile application integration

without major changes to existing code.

---

# 14. Deployment Architecture

Frontend

↓

Vercel

↓

Backend

↓

Render

↓

MongoDB Atlas

This architecture provides a production-ready deployment pipeline suitable for portfolio projects and technical interviews.
