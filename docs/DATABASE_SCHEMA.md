# CodingInsight AI - Database Schema Design

# 1. Database Overview

Database: MongoDB

The system uses a document-based database to store:

* User accounts
* Connected coding profiles
* Aggregated statistics
* Historical snapshots
* Goals
* AI analysis reports

Collections are designed to support future coding platforms without major schema changes.

---

# 2. Collections Overview

1. users
2. codingProfiles
3. profileSnapshots
4. goals
5. analysisReports

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

email (unique)

---

# 4. Coding Profiles Collection

Purpose:

Stores connected coding platform accounts.

One user can connect multiple platforms.

Schema:

{
_id: ObjectId,

userId: ObjectId,

platform: String,

username: String,

profileUrl: String,

isConnected: Boolean,

lastSyncedAt: Date,

stats: {

```
  totalSolved: Number,

  easySolved: Number,

  mediumSolved: Number,

  hardSolved: Number,

  contestRating: Number,

  contestRank: Number,

  contributionPoints: Number
```

},

createdAt: Date,

updatedAt: Date
}

Example platform values:

* leetcode
* codeforces
* codechef
* geeksforgeeks

Indexes:

userId

platform

(userId + platform) unique

---

# 5. Profile Snapshots Collection

Purpose:

Stores historical progress data.

This enables:

* Rating growth charts
* Progress tracking
* Historical analytics

Schema:

{
_id: ObjectId,

userId: ObjectId,

platform: String,

snapshotDate: Date,

stats: {

```
  totalSolved: Number,

  easySolved: Number,

  mediumSolved: Number,

  hardSolved: Number,

  contestRating: Number,

  contestRank: Number
```

}
}

Indexes:

userId

snapshotDate

platform

---

# 6. Goals Collection

Purpose:

Stores user-defined coding goals.

Schema:

{
_id: ObjectId,

userId: ObjectId,

title: String,

description: String,

targetValue: Number,

currentValue: Number,

status: String,

deadline: Date,

createdAt: Date,

updatedAt: Date
}

Status values:

* pending
* active
* completed

Indexes:

userId

status

---

# 7. Analysis Reports Collection

Purpose:

Stores AI-generated reports.

Schema:

{
_id: ObjectId,

userId: ObjectId,

readinessScore: Number,

strengths: [

```
  String
```

],

weaknesses: [

```
  String
```

],

recommendations: [

```
  String
```

],

summary: String,

generatedAt: Date
}

Indexes:

userId

generatedAt

---

# 8. Relationships

User

↓

Coding Profiles

↓

Profile Snapshots

↓

Analysis Reports

↓

Goals

Relationship Type:

User (1) → (Many) Coding Profiles

User (1) → (Many) Snapshots

User (1) → (Many) Goals

User (1) → (Many) Analysis Reports

---

# 9. Snapshot Strategy

Purpose:

Track progress over time.

Recommended Frequency:

Once per day

Snapshot Creation:

1. Fetch latest platform data
2. Store new snapshot
3. Update current profile stats
4. Generate dashboard analytics

Benefits:

* Growth charts
* Historical trends
* AI progress analysis

---

# 10. Dashboard Aggregation Strategy

Dashboard should not query external platforms directly.

Instead:

1. Fetch data from MongoDB
2. Aggregate profile statistics
3. Return unified response

Benefits:

* Faster dashboard
* Lower API usage
* Better scalability

---

# 11. Future Extensions

The schema supports:

* Additional coding platforms
* Resume analysis
* Interview readiness reports
* Team comparisons
* Public profile sharing
* AI mentoring features

without requiring major database redesign.

---

# 12. Database Design Principles

* Avoid data duplication
* Use references where appropriate
* Store historical data separately
* Keep platform integrations generic
* Optimize for dashboard reads
* Design for future extensibility
