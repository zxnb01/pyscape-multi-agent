# Code Duels

Compete in real-time 1v1 coding battles. Race to solve problems, earn XP, and climb the leaderboard.

---

## ⚔️ What Are Code Duels?

Code Duels are **live, real-time competitive coding matches** where:

- **You and an opponent** face the same programming problem
- **Race to finish** within 15 minutes
- **Real-time updates** - see opponent's progress live
- **Instant feedback** - code execution results immediately
- **Earn XP & leaderboard points** - build your ranking

---

## 🎮 How Code Duels Work

### 1. Join the Queue

Select your preferences:
- **Difficulty**: Beginner, Intermediate, Advanced
- **Language**: Python, JavaScript, Java, C++

```
┌─────────────────────────────┐
│ Join Code Duel Queue        │
├─────────────────────────────┤
│ Difficulty: [●] Intermediate│
│ Language:   [Python ▼]      │
│                             │
│          [JOIN QUEUE]       │
└─────────────────────────────┘

Queue Position: #2
Waiting time: ~30 seconds
```

### 2. Get Matched

System pairs you with an opponent:
- Same difficulty preference (usually)
- Same language preference (usually)
- Similar skill rating (ELO)

Once matched, duel starts immediately.

### 3. Duel Begins

Both players see:
- **Problem statement** - Description and input/output format
- **Code editor** - Full IDE with syntax highlighting
- **Test cases** - Example inputs and expected outputs
- **Timer** - 15-minute countdown (both players see same timer)
- **Opponent status** - "Coding", "Testing", "Completed", etc.

```
┌──────────────────────────────────────────────────┐
│ CODE DUEL                                        │
├──────────────────────────────────────────────────┤
│ Problem: Two Sum                    ⏱️  12:45   │
│                                                  │
│ Given an array of integers, find two numbers    │
│ that add up to a target. Return their indices.  │
│                                                  │
│ Example:                                        │
│   Input: [2,7,11,15], target=9                 │
│   Output: [0,1]                                 │
│                                                  │
├──────────────────────────────────────────────────┤
│ Your Code:                  │ Opponent Status:   │
│                             │ 🔴 Still Coding   │
│ def twoSum(nums, target):  │                    │
│     for i in range(...):   │                    │
│         for j in range(...):│ Submitted: 0     │
│             if nums[i] +   │ Tests Pass: 0/10  │
│             nums[j] ==     │                    │
│             target:        │                    │
│                 return...  │                    │
│                             │                    │
│ [SUBMIT CODE] [RUN TEST]   │                    │
└──────────────────────────────────────────────────┘
```

### 4. Submit Code

While coding, you can:
- **Run tests** - Execute against sample test cases
- **Submit** - Test against hidden test cases (counts toward score)
- **Chat** - Communicate with opponent

### 5. Code Execution

When you submit:
1. Code is sent to Judge0 API
2. Executed in isolated Docker container
3. Tested against 10 hidden test cases
4. Results returned in real-time

```
SUBMISSION RESULTS:
├── Status: ✅ All tests pass
├── Score: 100/100
├── Runtime: 0.23s
├── Memory: 12 MB
└── Feedback: Optimal solution!
```

### 6. Race to Finish

Victory conditions:

| Scenario | Winner |
|----------|--------|
| Both complete | Fastest time |
| One completes | That player (100 XP) |
| Neither completes | Higher score (20 XP each) |
| One forfeits | Other player (wins by default) |

### 7. Results & Rewards

```
┌────────────────────────────────────┐
│ DUEL COMPLETE!                     │
├────────────────────────────────────┤
│                                    │
│ You:                 vs Opponent:  │
│ ✅ Completed (2:30)      🔴 Failed │
│                                    │
│ Score:   100/100        0/100      │
│ Time:    2:30           9:15       │
│                                    │
│         🎉 YOU WIN! 🎉             │
│                                    │
│      +100 XP                       │
│      +25 Rating Points             │
│      +1 Win to your stats          │
│                                    │
└────────────────────────────────────┘
```

---

## 📊 Matchmaking System

### ELO Rating

Your skill rating is calculated using **ELO** (from chess):

- **Start at**: 1200
- **Win**: +25 points
- **Loss**: -25 points
- **Skill variance**: Higher rated players gain/lose more points

### Skill-Based Pairing

Matchmaking considers:
1. **Preferred difficulty** (beginner/intermediate/advanced)
2. **Preferred language** (python/javascript/java/cpp)
3. **ELO rating** (within ±200 points)

### Queue Logic

```
Player joins queue:
  → Find opponent with exact preferences (30 second wait)
  → If not found, relax language requirement (30 sec wait)
  → If still not found, relax difficulty requirement
  → Match immediately when found
```

---

## 🏆 Leaderboards

Compete globally and locally:

### Global Rankings

```
Rank | Player        | Rating | Wins | Losses | Win%
-----|---------------|--------|------|--------|------
  1  | AlgoMaster    | 1842   | 127  | 18     | 87.6%
  2  | PythonPro     | 1721   | 94   | 23     | 80.3%
  3  | CodeNinja     | 1698   | 81   | 25     | 76.4%
  4  | You           | 1452   | 34   | 12     | 73.9%
  5  | WebDevSam     | 1401   | 28   | 20     | 58.3%
```

### By Language

Separate leaderboards for Python, JavaScript, Java, C++

### By Difficulty

Separate leaderboards for Beginner, Intermediate, Advanced

---

## 📈 Duel Statistics

View your competitive profile:

```
Code Duel Stats
├── Total Duels: 46
├── Wins: 34
├── Losses: 12
├── Win Rate: 73.9%
├── Current Streak: 4 wins
├── Best Streak: 12 wins
├── ELO Rating: 1452
├── Global Rank: 247
└── Favorite Language: Python (28 wins)
```

---

## 💻 Supported Languages

| Language | Compiler | Version | Notes |
|----------|----------|---------|-------|
| Python | CPython | 3.10 | Full stdlib: NumPy, Pandas, etc. |
| JavaScript | Node.js | 18 | ES2020+ support |
| Java | OpenJDK | 17 | Full standard library |
| C++ | GCC | 11 | `-std=c++17` |

---

## 🎯 Problem Types

Duel problems range in difficulty:

### Beginner (20-40 problems)
- Implement basic algorithms
- Array/string manipulation
- Conditional logic
- Time: 5-10 min average

Examples:
- Two Sum
- Reverse String
- FizzBuzz
- Palindrome Check

### Intermediate (40-60 problems)
- Data structure operations
- Dynamic programming basics
- Tree/graph basics
- Time: 10-15 min average

Examples:
- LeetCode Medium problems
- Merge two arrays
- BFS/DFS
- Linked list operations

### Advanced (30+ problems)
- Complex algorithms
- Advanced data structures
- Optimization challenges
- Time: 15+ min average

Examples:
- LeetCode Hard problems
- Graph algorithms
- DP optimization
- System design patterns

---

## 🛡️ Fair Play & Security

### Code Isolation
- Each submission runs in its own Docker container
- No file system access
- No network access
- 5-second timeout per submission
- Memory limit: 256 MB

### Fraud Prevention
- Submissions timestamped and logged
- Can't access previous submissions during duel
- Each duel uses fresh, random problem
- Judge0 prevents code injection

### Replay & Learning
- After duel ends, see opponent's solution
- Learn from different approaches
- No risk of cheating (solved before reveal)

---

## 🎓 Duels for Learning

Use code duels to:

1. **Apply skills** - Use what you learned in lessons
2. **Learn new approaches** - See how others solve problems
3. **Build speed** - Time pressure improves problem-solving
4. **Compete safely** - Risk-free competition with XP rewards
5. **Track growth** - Watch your ELO rating improve

---

## ⚙️ Technical Details

### WebSocket Communication

Real-time updates via WebSocket (see [Architecture](../ARCHITECTURE.md)):

```javascript
// Client sends:
{
  "type": "submit-code",
  "duelId": "duel-123",
  "code": "def solve(...):\n  ...",
  "language": "python"
}

// Server responds:
{
  "type": "submission-result",
  "status": "success",
  "score": 100,
  "testsPassed": 10,
  "testsTotal": 10,
  "runtime": 0.23,
  "opponentUpdate": {
    "status": "still-coding",
    "testsPass": 3
  }
}
```

### Judge0 Integration

See [API Reference](../guides/API.md) for details on code execution flow.

---

## 🚫 Limitations & Known Issues

- **Cold starts**: First submission takes ~2-3 seconds (Judge0 warmup)
- **Timeout**: 5-second limit per code execution (adjust if needed)
- **Queue wait**: During off-hours, queue can be 60+ seconds
- **Languages**: C/C++ performance varies by system load

---

## 🔗 Related

- [Gamification System](GAMIFICATION.md)
- [Architecture Overview](../ARCHITECTURE.md#-code-duel-flow)
- [Troubleshooting](../guides/TROUBLESHOOTING.md)

---

Last updated: May 27, 2026
