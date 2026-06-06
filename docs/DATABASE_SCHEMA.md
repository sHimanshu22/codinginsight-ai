# CodingInsight AI - Database Schema Design

# 1. Database Overview

Database: MongoDB

CodingInsight AI uses MongoDB to store:

* User accounts
* Connected coding platform profiles
* Historical coding progress
* Aggregated analytics
* User goals
* AI-generated insights and readiness reports

The schema is designed to:

* Support multiple coding platforms
* Store historical growth data
* Enable analytics generation
* Enable AI-powered recommendations
* Remain extensible for future features

---

# 2. Collections Overview

Core Collections:

1. users
2. codingProfiles
3. profileSnapshots
4. userAnalytics
5. goals
6. analysisReports

Optional Future Collection:

7. syncLogs

---

# 3. Users Collection

Purpose:

Stores authentication and account information.

Schema:

{
_id: ObjectId,

name: String,

email: String,

password: String,

avatar: String,

role: String,

createdAt: Date,

updatedAt: Date
}

Indexes:

* email (unique)

---

# 4. Coding Profiles Collection

Purpose:

Stores connected coding platform accounts.

One user can connect multiple coding platforms.

Schema:

{
_id: ObjectId,

userId: ObjectId,

platform: String,

username: String,

profileUrl: String,

isConnected: Boolean,

lastSyncedAt: Date,

platformStats: Object,

createdAt: Date,

updatedAt: Date
}

Example:

{
userId: ObjectId,

platform: "leetcode",

username: "john123",

platformStats: {

```
totalSolved: 350,

easySolved: 150,

mediumSolved: 170,

hardSolved: 30
```

}
}

Indexes:

* userId
* platform
* (userId + platform) unique

Supported Platforms:

* leetcode
* codeforces
* codechef
* geeksforgeeks

---

# 5. Profile Snapshots Collection

Purpose:

Stores historical profile data.

Used for:

* Progress tracking
* Growth charts
* Historical analytics
* AI trend analysis

Schema:

{
_id: ObjectId,

userId: ObjectId,

platform: String,

snapshotDate: Date,

stats: Object,

createdAt: Date
}

Example:

{
userId: ObjectId,

platform: "leetcode",

snapshotDate: Date,

stats: {

```
totalSolved: 320,

easySolved: 140,

mediumSolved: 150,

hardSolved: 30
```

}
}

Indexes:

* userId
* platform
* snapshotDate

---

# 6. User Analytics Collection

Purpose:

Stores processed analytics generated from coding profiles and snapshots.

Dashboard should primarily read from this collection.

Schema:

{
_id: ObjectId,

userId: ObjectId,

totalSolved: Number,

consistencyScore: Number,

contestPerformanceScore: Number,

activeDays: Number,

strongestPlatform: String,

weakestPlatform: String,

strongestTopics: [String],

weakestTopics: [String],

lastUpdated: Date
}

Indexes:

* userId (unique)

---

# 7. Goals Collection

Purpose:

Stores coding goals defined by users.

Schema:

{
_id: ObjectId,

userId: ObjectId,

goalType: String,

platform: String,

targetValue: Number,

currentValue: Number,

status: String,

deadline: Date,

createdAt: Date,

updatedAt: Date
}

Goal Types:

* leetcode_problems
* codeforces_rating
* contest_participation
* daily_streak

Status Values:

* pending
* active
* completed

Indexes:

* userId
* status

---

# 8. Analysis Reports Collection

Purpose:

Stores AI-generated profile analysis and company readiness reports.

Schema:

{
_id: ObjectId,

userId: ObjectId,

targetCompany: String,

readinessScore: Number,

metrics: {

```
problemSolving: Number,

consistency: Number,

contestPerformance: Number,

topicCoverage: Number
```

},

strengths: [String],

weaknesses: [String],

recommendations: [String],

summary: String,

generatedAt: Date
}

Example:

{
targetCompany: "Google",

readinessScore: 72,

metrics: {

```
problemSolving: 80,

consistency: 70,

contestPerformance: 65,

topicCoverage: 73
```

}
}

Indexes:

* userId
* targetCompany
* generatedAt

---

# 9. Sync Logs Collection (Future)

Purpose:

Stores profile synchronization history.

Useful for debugging API integrations.

Schema:

{
_id: ObjectId,

userId: ObjectId,

platform: String,

status: String,

message: String,

syncedAt: Date
}

Status Values:

* success
* failed

Indexes:

* userId
* platform
* syncedAt

---

# 10. Relationships

User (1)

├── Coding Profiles (Many)

├── Profile Snapshots (Many)

├── Goals (Many)

├── Analysis Reports (Many)

└── User Analytics (One)

Relationship Summary:

User (1) → (Many) Coding Profiles

User (1) → (Many) Profile Snapshots

User (1) → (Many) Goals

User (1) → (Many) Analysis Reports

User (1) → (One) User Analytics

---

# 11. Data Flow

Coding Platforms

↓

Coding Profiles

↓

Profile Snapshots

↓

User Analytics

↓

AI Analysis Reports

The AI system should analyze processed analytics instead of raw platform data.

---

# 12. Snapshot Strategy

Frequency:

* Once per day

Process:

1. Fetch latest platform data
2. Update codingProfiles
3. Create profileSnapshots
4. Recalculate userAnalytics
5. Generate AI insights when requested

Benefits:

* Growth tracking
* Historical trends
* Better AI recommendations

---

# 13. Database Design Principles

* Keep platform integrations generic
* Separate raw data from analytics
* Store historical data independently
* Optimize dashboard reads
* Support future coding platforms
* Minimize schema changes
* Enable AI-driven analysis

---
