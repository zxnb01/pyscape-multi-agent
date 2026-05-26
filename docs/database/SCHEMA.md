# PyScape Database Schema

Complete reference for all tables, columns, relationships, and functions in the PyScape database.

---

## 📊 Table Directory

| Table | Purpose | Rows | Key Columns |
|-------|---------|------|-------------|
| **profiles** | User information | ~1000s | id, full_name, avatar_url |
| **modules** | Learning modules | ~10 | name, description, order_index |
| **lessons** | Lessons within modules | ~100 | module_id, title, order_index |
| **skills** | Atomic skills | ~50 | name, domain, difficulty |
| **skill_dependencies** | Prerequisite graph | ~100 | skill_id, depends_on |
| **user_skill_mastery** | User progress | ~100k | user_id, skill_id, mastery |
| **duels** | Duel sessions | ~100k | player1_id, player2_id, winner_id |
| **duel_submissions** | Code submissions | ~300k | duel_id, user_id, code |
| **duel_stats** | Player statistics | ~1000s | user_id, wins, losses |
| **gamification** | XP/badges/level | ~1000s | user_id, total_xp, level |

---

## 🔐 Detailed Table Reference

### `profiles`
User profile and preferences.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| id | UUID | PRIMARY KEY | References auth.users(id) |
| full_name | TEXT | | User's display name |
| gender | TEXT | | Demographics |
| role | TEXT | | Student/Professional/etc |
| organization | TEXT | | School/company name |
| bio | TEXT | | User biography |
| avatar_url | TEXT | | Profile picture URL |
| profile_complete | BOOLEAN | DEFAULT false | Onboarding status |
| onboarding_completed | BOOLEAN | DEFAULT false | Topic selection done |
| selected_topics | TEXT[] | DEFAULT NULL | Array of topic IDs |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | Account creation |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Last profile update |

**Indexes:**
- PRIMARY KEY on id
- INDEX on created_at (for analytics)

**RLS Policies:**
```sql
-- Users can view their own profile
SELECT: (auth.uid() = id)

-- Users can insert their own profile
INSERT: (auth.uid() = id)

-- Users can update their own profile
UPDATE: (auth.uid() = id)
```

---

### `modules`
Learning modules (groups of lessons).

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| id | UUID | PRIMARY KEY | |
| name | TEXT | NOT NULL | e.g., "Python Basics" |
| description | TEXT | | Module overview |
| is_published | BOOLEAN | DEFAULT false | Draft/published |
| order_index | INT | | Display order |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

---

### `lessons`
Individual lessons within a module.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| id | UUID | PRIMARY KEY | |
| module_id | UUID | FOREIGN KEY | modules(id) |
| title | TEXT | NOT NULL | Lesson title |
| description | TEXT | | What you'll learn (120-180 words) |
| is_published | BOOLEAN | DEFAULT false | Published status |
| order_index | INT | | Order within module |
| parts | JSONB | DEFAULT '[]'::jsonb | Multi-level content structure |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

**Example `parts` structure:**
```json
[
  {
    "level": 1,
    "title": "Introduction",
    "content": "...",
    "keyPoints": ["...", "..."],
    "examples": ["...", "..."]
  },
  {
    "level": 2,
    "title": "Advanced Concepts",
    "content": "...",
    "exercise": "..."
  }
]
```

**Indexes:**
- FOREIGN KEY on module_id
- INDEX on order_index
- INDEX on is_published

---

### `skills`
Atomic skills that lessons teach.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| id | UUID | PRIMARY KEY | |
| name | TEXT | NOT NULL UNIQUE | "Variables and Data Types" |
| domain | TEXT | NOT NULL | python, ml, dsa, ai |
| difficulty | INT | 1-5 | Skill difficulty star rating |
| estimated_minutes | INT | | Time to master |
| icon | TEXT | | Emoji icon |
| description | TEXT | | Skill description |
| is_published | BOOLEAN | DEFAULT true | Published status |
| order_index | INT | | Order within domain |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

**Sample Data:**
```sql
INSERT INTO skills VALUES
('skill-001', 'Variables and Data Types', 'python', 1, 45, '📦', 'Learn how to store and use data'),
('skill-002', 'Functions', 'python', 1, 60, '🔧', 'Write reusable code with functions'),
('skill-003', 'Object-Oriented Programming', 'python', 3, 120, '🏗️', 'Design with classes and objects');
```

---

### `skill_dependencies`
Prerequisite graph (DAG structure).

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| skill_id | UUID | FOREIGN KEY | skills(id) |
| depends_on | UUID | FOREIGN KEY | skills(id) - prerequisite |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |

**Constraint:** `UNIQUE(skill_id, depends_on)` - can't depend on same skill twice

**Example:**
```sql
-- OOP depends on Functions depends on Variables
INSERT INTO skill_dependencies VALUES
('skill-003', 'skill-002'),  -- OOP → Functions
('skill-002', 'skill-001');  -- Functions → Variables
```

**RLS Policies:** None (public read for curriculum design)

---

### `user_skill_mastery`
User progress on each skill.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| user_id | UUID | FOREIGN KEY | auth.users(id) |
| skill_id | UUID | FOREIGN KEY | skills(id) |
| mastery | FLOAT | 0.0 to 1.0 | Progress (0% to 100%) |
| status | TEXT | locked, eligible, in_progress, mastered | Current state |
| started_at | TIMESTAMPTZ | DEFAULT NOW() | When learning started |
| completed_at | TIMESTAMPTZ | | When mastered (null if ongoing) |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | Last update |
| PRIMARY KEY | (user_id, skill_id) | | |

**Status Rules:**
- `locked` - Prerequisites not met
- `eligible` - Prerequisites met, ready to learn
- `in_progress` - User has started lessons (0 < mastery < 1.0)
- `mastered` - mastery >= 0.95

**RLS Policies:**
```sql
-- Users can only see their own mastery
SELECT: (auth.uid() = user_id)
INSERT: (auth.uid() = user_id)
UPDATE: (auth.uid() = user_id)
```

**Helper Function:**
```sql
-- Increment mastery safely
SELECT increment_mastery(user_id UUID, skill_id UUID, delta FLOAT)
RETURNS FLOAT  -- New mastery value (capped at 1.0)
```

---

### `duels`
Code duel sessions between two players.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| id | UUID | PRIMARY KEY | |
| player1_id | UUID | FOREIGN KEY | auth.users(id) |
| player2_id | UUID | FOREIGN KEY | auth.users(id) |
| problem_id | UUID | FOREIGN KEY | problems(id) |
| status | TEXT | in_progress, completed, forfeited | Current state |
| winner_id | UUID | FOREIGN KEY | auth.users(id) - null if draw |
| player1_score | INT | 0-100 | Points earned |
| player2_score | INT | 0-100 | Points earned |
| player1_time_ms | INT | | Milliseconds to complete |
| player2_time_ms | INT | | Milliseconds to complete |
| difficulty | TEXT | beginner, intermediate, advanced | Matched skill level |
| language | TEXT | python, javascript, java, cpp | Programming language |
| created_at | TIMESTAMPTZ | DEFAULT NOW() | |
| completed_at | TIMESTAMPTZ | | When duel finished |

**Indexes:**
- FOREIGN KEY on player1_id, player2_id
- INDEX on status
- INDEX on completed_at (for history queries)

**RLS Policies:**
```sql
-- Players can view their own duels
SELECT: (player1_id = auth.uid() OR player2_id = auth.uid())
```

---

### `duel_submissions`
Individual code submissions during a duel.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| id | UUID | PRIMARY KEY | |
| duel_id | UUID | FOREIGN KEY | duels(id) |
| user_id | UUID | FOREIGN KEY | auth.users(id) |
| code | TEXT | | Source code submitted |
| submission_number | INT | 1+ | Attempt number |
| status | TEXT | pending, running, success, error | Execution status |
| output | TEXT | | Test results or error message |
| score | INT | 0-100 | Points for this submission |
| submitted_at | TIMESTAMPTZ | DEFAULT NOW() | |
| completed_at | TIMESTAMPTZ | | When execution finished |

**RLS Policies:**
```sql
-- Players can view submissions in their duels
SELECT: (
  EXISTS(
    SELECT 1 FROM duels
    WHERE duels.id = duel_submissions.duel_id
    AND (duels.player1_id = auth.uid() OR duels.player2_id = auth.uid())
  )
)
```

---

### `duel_stats`
Aggregated statistics for competitive ranking.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| user_id | UUID | PRIMARY KEY | auth.users(id) |
| total_duels | INT | | Matches played |
| wins | INT | | Matches won |
| losses | INT | | Matches lost |
| draws | INT | | Matches tied |
| win_rate | FLOAT | 0.0-1.0 | wins/total_duels |
| elo_rating | INT | | Competitive ranking |
| global_rank | INT | | Position on leaderboard |
| current_streak | INT | | Consecutive wins |
| best_streak | INT | | Best win streak ever |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

**Indexes:**
- INDEX on global_rank (for leaderboard queries)
- INDEX on elo_rating (for matchmaking)

**RLS Policies:** Public read (leaderboards visible to all)

---

### `gamification`
User XP, badges, and progression.

| Column | Type | Constraints | Notes |
|--------|------|-----------|-------|
| user_id | UUID | PRIMARY KEY | auth.users(id) |
| total_xp | INT | DEFAULT 0 | Lifetime XP earned |
| level | INT | 1-100 | Player level (1-100) |
| current_level_xp | INT | 0-1000 | XP toward next level |
| badges_earned | TEXT[] | | Array of badge IDs |
| current_streak | INT | | Days learning streak |
| best_streak | INT | | Best streak ever |
| last_activity | TIMESTAMPTZ | DEFAULT NOW() | Last action date |
| updated_at | TIMESTAMPTZ | DEFAULT NOW() | |

**XP Awards:**
- Completing a lesson: +50 XP
- Passing a quiz: +25 XP
- Winning a duel: +100 XP
- Losing a duel: +20 XP
- Earning badge: +200 XP

**Badges (examples):**
- `first-lesson` - Complete first lesson
- `skill-master` - Achieve 100% on a skill
- `duel-winner` - Win first duel
- `streak-7` - 7-day learning streak
- `python-expert` - Master all Python skills

---

## 🔗 Relationships Diagram

```
auth.users (Supabase)
    ├── profiles (1:1)
    ├── user_skill_mastery (1:*)
    ├── duels (1:* as player)
    ├── duel_stats (1:1)
    └── gamification (1:1)

modules (1:*)
    └── lessons

lessons (1:*)
    └── lesson_skills

skills (N:N)
    ├── skill_dependencies (self-referential DAG)
    ├── user_skill_mastery
    └── lesson_skills

duels (1:*)
    └── duel_submissions
```

---

## 🔧 Useful SQL Queries

### Get User's Locked Skills
```sql
SELECT s.* FROM skills s
JOIN skill_dependencies sd ON s.id = sd.skill_id
JOIN user_skill_mastery usm ON sd.depends_on = usm.skill_id
WHERE usm.user_id = 'user-123'
AND usm.status != 'mastered'
GROUP BY s.id;
```

### Get User's Next Recommended Skill
```sql
SELECT s.* FROM skills s
JOIN user_skill_mastery usm ON s.id = usm.skill_id
WHERE usm.user_id = 'user-123'
AND usm.status = 'eligible'
ORDER BY s.order_index ASC
LIMIT 1;
```

### Get Duel Leaderboard
```sql
SELECT u.full_name, ds.elo_rating, ds.wins, ds.losses
FROM duel_stats ds
JOIN profiles u ON ds.user_id = u.id
ORDER BY ds.elo_rating DESC
LIMIT 100;
```

### Increment User XP
```sql
SELECT gamification.increment_xp('user-123', 50);
```

---

## 📈 Performance Recommendations

### Indexes to Add
```sql
CREATE INDEX idx_lessons_module_id ON lessons(module_id);
CREATE INDEX idx_lessons_order ON lessons(order_index);
CREATE INDEX idx_user_skill_mastery_user_id ON user_skill_mastery(user_id);
CREATE INDEX idx_duels_player1_id ON duels(player1_id);
CREATE INDEX idx_duels_created_at ON duels(created_at DESC);
CREATE INDEX idx_duel_stats_elo ON duel_stats(elo_rating DESC);
```

### Connection Pooling
Supabase automatically handles connection pooling. No configuration needed.

### Query Optimization
- Always filter by `user_id` in SELECT queries (RLS + performance)
- Use LIMIT for pagination (avoid loading 10k rows)
- Batch updates when possible (UPDATE multiple rows in one query)

---

## 📝 Changelog

| Date | Change |
|------|--------|
| 2026-05-27 | Initial schema documentation |
| 2026-04-15 | Added skill_dependencies table |
| 2026-03-20 | Added user_skill_mastery |
| 2026-03-01 | Added duel tables (duels, duel_submissions, duel_stats) |
| 2026-02-10 | Initial database schema created |

---

Last updated: May 27, 2026
