# PyScape Architecture Overview

A comprehensive guide to PyScape's system design, components, and data flow.

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     USER BROWSER                             │
│  ┌────────────────────────────────────────────────────────┐  │
│  │          React Frontend (http://localhost:3000)        │  │
│  │  - Learn (Adaptive Lessons)                            │  │
│  │  - Code Sandbox (ML Sandbox)                           │  │
│  │  - Code Duel (Matchmaking UI)                          │  │
│  │  - Portfolio (Export & Showcase)                       │  │
│  └────────────────────────────────────────────────────────┘  │
│  Protocols: HTTP/REST, WebSocket (Real-time)                │
└─────────────────────────────────────────────────────────────┘
                          ↓
        ┌─────────────────────────────────────┐
        │    Supabase (PostgreSQL + Auth)     │
        │  - User authentication              │
        │  - Database (all data)              │
        │  - Real-time subscriptions          │
        │  - RLS Policies                     │
        └─────────────────────────────────────┘
         ↓                      ↓                    ↓
    ┌─────────────┐    ┌──────────────┐    ┌────────────────┐
    │  Express    │    │ WebSocket    │    │ OpenAI/        │
    │  API Server │    │ Server       │    │ Anthropic API  │
    │ (optional)  │    │ (Duels)      │    │ (Content Gen)  │
    └─────────────┘    └──────────────┘    └────────────────┘
         ↓                    ↓                     ↓
    ┌─────────────┐    ┌──────────────┐    ┌────────────────┐
    │ Judge0 API  │    │ Judge0 API   │    │ LangChain      │
    │ (Code Exec) │    │ (Code Exec)  │    │ (Orchestration)│
    └─────────────┘    └──────────────┘    └────────────────┘
```

---

## 📦 Component Layers

### 1. **Frontend (React)**

#### Purpose
Interactive user interface for learning, coding, and dueling

#### Key Components
- **AuthComponent** - Login/signup with Supabase Auth
- **LearnPage** - Adaptive lesson interface with module selection
- **CodeSandbox** - Multi-language code editor (CodeMirror)
- **CodeDuelPage** - Matchmaking and duel UI (WebSocket client)
- **PortfolioPage** - Project showcase with PDF export

#### Technology Stack
- **React 18** - UI framework
- **Tailwind CSS** - Styling
- **Framer Motion** - Animations
- **CodeMirror** - Code editor
- **React Router** - Navigation

#### State Management
- **React Context API** - Global state (auth, user, duels)
- **Local State** - Component-level state with useState

---

### 2. **Backend Services**

#### Express API Server (`server.js`)
Provides REST endpoints for general data operations.

**Endpoints:**
- `GET /api/health` - Health check
- `POST /api/execute-code` - Code execution (Python/JS)
- `GET /api/problems` - Fetch problems for duels

**Purpose:** Optional utility endpoints (code execution, problem management)

#### WebSocket Server (`duel-server.js`)
Real-time bidirectional communication for code duels.

**Features:**
- JWT authentication via Supabase tokens
- Player matchmaking (difficulty + language)
- Duel session management
- Real-time code submission and testing
- XP/score updates

**Protocol:**
```
Client → WS → Server
  {
    "type": "join-queue",
    "difficulty": "intermediate",
    "language": "python"
  }

Server → Client
  {
    "type": "matched",
    "opponent": "username",
    "problem": { ... },
    "timeLimit": 900
  }
```

---

### 3. **Database Layer (Supabase/PostgreSQL)**

#### Core Tables

**Authentication**
- `auth.users` - Built-in Supabase users table

**User Data**
- `profiles` - User profile, preferences, progress
- `user_skill_mastery` - Progress on each skill

**Learning Content**
- `modules` - Learning modules (Python Basics, ML, etc.)
- `lessons` - Individual lessons within modules
- `skills` - Atomic skills being taught
- `skill_dependencies` - Prerequisite relationships

**Code Duels**
- `duels` - Duel sessions (players, problem, winner, scores)
- `duel_submissions` - Code submissions during a duel
- `duel_stats` - Aggregated player stats (wins, losses, rank)

**Gamification**
- `gamification` - User XP, badges, level, streaks
- `badges_earned` - Which badges user has earned

**Projects & Labs**
- `projects` - Project templates
- `project_completions` - User project progress

#### Security

All tables use **Row Level Security (RLS)**:
- Users can only see/modify their own data
- Policies defined per table
- Enforced by Supabase automatically

---

### 4. **External Services**

#### Supabase Auth
- OAuth with GitHub/Google
- Email + password authentication
- JWT tokens for authorization

#### Judge0 API (via RapidAPI)
- Secure, isolated code execution
- Input: source code + language
- Output: execution result, runtime, memory
- Languages: Python, JavaScript, Java, C, C++

#### OpenAI/Anthropic API
- Content generation for lessons
- LangChain orchestration
- Prompt engineering for quality

#### GNews API
- Fetch AI/ML news
- Dashboard widget updates

---

## 🔄 Data Flow Diagrams

### Scenario 1: User Learns a Lesson

```
1. User clicks "Start Lesson"
   ↓
2. Frontend fetches lesson from Supabase
   - Query: lessons table, filter by module + order
   ↓
3. Supabase returns lesson content
   - Check RLS: can user access this lesson?
   - Return lesson parts (reading, quiz, coding)
   ↓
4. Frontend renders lesson UI
   - Show reading material
   - Display quiz questions
   - Provide code editor for exercise
   ↓
5. User completes quiz/code challenge
   ↓
6. Frontend submits answers to Supabase
   - Update user_skill_mastery (add progress)
   - Award XP to gamification table
   ↓
7. Supabase triggers update
   - Recalculate next recommended lesson
   - Check skill prerequisites
   - Update user's "ready to learn" list
   ↓
8. Frontend fetches updated roadmap
   - User sees new unlocked lessons
```

### Scenario 2: User Joins Code Duel

```
1. User opens Code Duel, selects difficulty & language
   ↓
2. Frontend connects WebSocket to backend
   - Send: JWT token for authentication
   ↓
3. WebSocket server validates token with Supabase
   - Extract user_id from JWT
   - Confirm user is authenticated
   ↓
4. Server adds user to matchmaking queue
   - Key: "python-intermediate"
   - Value: [user1, user2, user3, ...]
   ↓
5. Server looks for opponent with same preferences
   - If found: trigger match immediately
   - If not found: wait in queue
   ↓
6. When 2 players matched:
   - Fetch random problem from database
   - Create duel record in Supabase
   - Send "matched" event to both clients
   ↓
7. Users code for 15 minutes (real-time timer)
   ↓
8. User submits code
   - Frontend sends code to WebSocket server
   - Server submits to Judge0 for execution
   ↓
9. Judge0 returns results
   - Execution success/failure
   - Test case pass/fail
   - Runtime statistics
   ↓
10. Server evaluates winner
    - Both complete: fastest time wins
    - One complete: that player wins
    - Neither: higher score wins
   ↓
11. Server awards XP
    - Winner: +100 XP + streak
    - Loser: +20 XP
    - Update duel_stats leaderboard
   ↓
12. Both clients receive "duel-complete" event
    - Show results screen
    - Display XP earned
```

---

## 🔌 Technology Decisions

### Why React?
- **Rich UI requirements** - animations, real-time updates
- **Component reusability** - lessons, sandbox, duel UI shared patterns
- **Ecosystem** - CodeMirror, Framer Motion, PDF export libraries
- **Developer experience** - hot reload, excellent devtools

### Why Supabase?
- **Full PostgreSQL** - relational data, complex queries
- **Built-in Auth** - OAuth, JWT, secure by default
- **Real-time subscriptions** - listen to database changes
- **RLS** - fine-grained security without extra code
- **Free tier** - ideal for open-source/learning projects

### Why WebSockets for Duels?
- **Real-time updates** - both players see opponent progress live
- **Low latency** - chat, timer updates need fast response
- **Bidirectional** - server can send events to client anytime
- **Efficiency** - single TCP connection, not HTTP polling

### Why Judge0 for Code Execution?
- **Security** - code runs in isolated Docker containers
- **Multi-language** - Python, Java, C, C++, JavaScript support
- **Scalability** - RapidAPI handles infrastructure
- **Reliability** - proven by thousands of coding platforms

### Why LangChain for Content?
- **Prompt management** - parameterize lesson generation
- **Reliability** - error handling, retries
- **Modularity** - chain multiple LLM calls together
- **Observability** - log and debug LLM interactions

---

## 🚀 Scaling Considerations

### Database
- Indexes on frequently queried columns (user_id, skill_id)
- Connection pooling via Supabase
- Archive old duel records to cold storage

### Backend
- Horizontal scale WebSocket servers (e.g., Redis pub/sub for matchmaking)
- Load balance Express API across multiple instances
- Cache frequently accessed problems in Redis

### Frontend
- Code splitting for faster initial load
- Service workers for offline capability
- CDN for static assets

### External APIs
- Rate limiting for Judge0 (cache results)
- Async OpenAI calls (don't block frontend)
- Retry logic for transient failures

---

## 📊 Data Models

### User Skill Mastery
```
user_id: uuid
skill_id: uuid
mastery: 0.0 to 1.0 (progress)
status: locked | eligible | in_progress | mastered
started_at: timestamp
completed_at: timestamp
```

### Duel Session
```
id: uuid
player1_id: uuid
player2_id: uuid
problem_id: uuid
status: in_progress | completed | forfeited
winner_id: uuid
player1_score: int (0-100)
player2_score: int (0-100)
player1_time_ms: int
player2_time_ms: int
created_at: timestamp
completed_at: timestamp
```

### Gamification
```
user_id: uuid (primary key)
total_xp: int
level: int (1-100)
current_level_xp: int (0-1000)
badges_earned: text[]
current_streak: int
best_streak: int
duel_wins: int
duel_losses: int
updated_at: timestamp
```

---

## 🔐 Security Model

### Authentication
- Supabase JWT tokens (signed by Supabase)
- Tokens sent with every request
- Expiry: default 1 hour

### Authorization
- RLS policies per table
- Example: Users can only view their own profile
- Server-side enforcement (Supabase)

### Code Execution
- Judge0 isolation (Docker containers)
- 5-second timeout per code execution
- Memory limit per execution
- Input validation before sending to Judge0

---

## 📈 Performance Targets

| Metric | Target |
|--------|--------|
| Page load time | < 2 seconds |
| Code execution | < 5 seconds |
| Matchmaking | < 30 seconds average |
| API response time | < 200ms (p95) |
| Database query | < 100ms (p95) |

---

## 🔗 Related Documentation

- [Database Schema Reference](database/SCHEMA.md)
- [Feature Guides](features/)
- [API Reference](guides/API.md)
- [Deployment Guide](guides/DEPLOYMENT.md)

---

Last updated: May 27, 2026
