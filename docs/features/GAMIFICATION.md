# Gamification System

Earn XP, collect badges, climb levels, and build streaks. PyScape turns learning into a rewarding game.

---

## 🎮 Overview

The gamification system motivates learning through:
- **XP (Experience Points)** - Earned for actions
- **Levels** - Progress from 1 to 100
- **Badges** - Unlock achievements
- **Streaks** - Build daily consistency
- **Leaderboards** - Compete globally

---

## 💰 XP System

### How to Earn XP

| Action | XP | Notes |
|--------|-----|-------|
| Complete lesson reading | +50 | Per lesson level |
| Pass quiz (60%+) | +25 | Per attempt |
| Solve coding exercise | +75 | Per correct solution |
| Win duel | +100 | Competitive bonus |
| Lose duel | +20 | Participation |
| Earn badge | +200 | One-time reward |
| 7-day streak | +500 | Bonus |
| Complete project | +500 | Major milestone |

### XP Tracking

```
User Dashboard:
├── Total XP: 2,450
├── This Week: +380 XP
├── This Month: +1,200 XP
├── Top Day: +120 XP (yesterday)
└── Current Trend: 📈 Up 15%
```

---

## 🎖️ Leveling System

### How Levels Work

```
Level 1-10:  Learn fundamentals
Level 11-30: Practice & specialize
Level 31-60: Master advanced topics
Level 61-100: Expert & contributor status
```

### Level Requirements

| Level | Total XP Needed | XP Per Level |
|-------|-----------------|-------------|
| 1 | 0 | — |
| 2 | 500 | 500 |
| 3 | 1,200 | 700 |
| 4 | 2,200 | 1,000 |
| 5 | 3,500 | 1,300 |
| ... | ... | +300 each level |
| 50 | 45,000 | 3,000 |
| 100 | 150,000 | 5,000 |

### Level Progress

```
Level 5 Progress:
███████░░░░░░ 54%
3,500 / 6,500 XP to Level 6
```

### Level Perks

| Level | Unlock |
|-------|--------|
| 5 | Custom avatar frame |
| 10 | Community badge |
| 25 | Code Duel leaderboard visibility |
| 50 | Community mentor status |
| 75 | Content creation access |
| 100 | PyScape Founder badge |

---

## 🏆 Badges

### Badge Categories

#### Achievement Badges
- **First Steps** - Complete first lesson
- **Week Warrior** - 7-day learning streak
- **Month Master** - 30-day streak
- **Century Champion** - 100-day streak

#### Skill Badges
- **Python Expert** - Master all Python skills
- **ML Specialist** - Master all ML skills
- **Data Master** - Complete all data science courses
- **Full Stack** - Master Python + JS + Data Science

#### Competitive Badges
- **Duel Starter** - Win first duel
- **Duel Master** - 50 duel wins
- **ELO Elite** - Reach 1800 ELO rating
- **Undefeated Week** - Win 10+ duels in a week

#### Contribution Badges
- **Bug Finder** - Report 3 bugs (when applicable)
- **Wiki Contributor** - Add 5 solutions
- **Community Helper** - Help 10 other learners
- **Content Creator** - Create 3 shared solutions

#### Social Badges
- **Recruiter-Friendly** - Complete profile (100%)
- **Portfolio Ready** - Export first portfolio
- **Share Champion** - Get 100 views on shared code
- **Mentor** - Reach 5 people (when feature available)

### Badge Display

```
Your Badges (14/80):

⭐ SKILL BADGES
  🐍 Python Basics (earned: March 1)
  📊 Data Analysis (earned: April 15)
  🤖 ML Fundamentals (earned: May 10)

🔥 STREAK BADGES
  🔥 Week Warrior (earned: May 1)
  🔥 Month Master (earned: June 1)

⚡ DUEL BADGES
  ⚔️ Duel Master (earned: May 20)

🎯 ACHIEVEMENT BADGES
  🎓 First Steps (earned: March 1)
```

---

## 🔥 Streak System

### What Is a Streak?

A **streak** is your consecutive number of days with learning activity.

```
Current Streak: 12 days 🔥
Best Streak: 34 days 🏆

Today: 45 XP earned ✓
Streak Continues Tomorrow If You:
  ✓ Complete 1+ lesson
  ✓ Submit code in sandbox
  ✓ Complete a duel
```

### Streak Bonuses

- **Day 3**: +50 XP bonus
- **Day 7**: +200 XP bonus + streak badge
- **Day 14**: +300 XP bonus
- **Day 30**: +500 XP bonus + special title
- **Day 100**: +1000 XP bonus + founder status

### Streak Protection

Once a month, **use a "Streak Shield"** if you miss a day:
- Costs 500 XP (or pass a quiz)
- Keeps your streak alive for 1 day
- Get a fresh shield the next month

---

## 🏅 Leaderboards

### Global Rankings

```
🏆 GLOBAL LEADERBOARD

Rank | Name          | Level | Total XP | Streak
-----|---------------|-------|----------|--------
  1  | AlgoMaster    | 45    | 87,500   | 89 🔥
  2  | PythonPro     | 42    | 78,200   | 34 🔥
  3  | DataDiva      | 41    | 76,800   | 12 🔥
  4  | You           | 28    | 34,500   | 12 🔥
  5  | CodeNinja     | 27    | 31,200   | 5 🔥
```

### Filters

Filter leaderboards by:
- **Time period**: This week, this month, all-time
- **Language**: Python, JavaScript, Java, C++
- **Category**: Overall, duels, learning, streaks
- **Difficulty**: Beginner, Intermediate, Advanced

### Your Rank

```
You're Ranked #247 Globally
Your Position in Leaderboard:

Position: Top 5% 🌟
vs. Level Peers: #12 out of 234 (92nd percentile)
vs. Friends: #3 out of 12
```

---

## 👥 Friend Leaderboards

Compare progress with friends:

```
FRIENDS LEADERBOARD

1. Alice (Level 32)      - 15 day streak
2. You (Level 28)        - 12 day streak  ← You are here
3. Bob (Level 26)        - 8 day streak
4. Charlie (Level 23)    - 3 day streak
5. Diana (Level 20)      - 1 day streak
```

---

## 📊 Statistics Dashboard

View detailed progress metrics:

```
LEARNING STATISTICS

Study Habits:
  Average Daily XP: 45
  Total Hours: 34.5
  Sessions This Month: 23
  Favorite Time: 9 PM - 11 PM

Skill Progress:
  Skills Started: 12
  Skills Mastered: 4
  Current Mastery: 34%
  Next Milestone: Level 30 (2,000 XP away)

Duel Performance:
  Total Duels: 46
  Win Rate: 73.9%
  Current Streak: 4 wins
  Favorite Language: Python

Achievement Progress:
  Badges: 14/80 (17.5%)
  Longest Streak: 34 days
  Projects Completed: 1
```

---

## 🎯 Gamification Psychology

### Why Gamification Works

1. **Progress Visualization** - See your improvement graphically
2. **Frequent Rewards** - Small wins every day (badges, XP)
3. **Leaderboards** - Social motivation to improve
4. **Streaks** - Build habit through consistency
5. **Levels** - Milestones feel less daunting than one big goal

### Engagement Patterns

PyScape's system encourages:
- ✅ **Daily consistency** (streaks)
- ✅ **Exploration** (many badges to unlock)
- ✅ **Competition** (duels, leaderboards)
- ✅ **Mastery** (levels reward depth)
- ✅ **Progress** (XP gives immediate feedback)

---

## 🚫 Fair Play

### Anti-Gaming Measures

To prevent exploitation:
- **Time-gated rewards** - Can't farm same activity for infinite XP
- **Difficulty scaling** - XP varies by complexity
- **Fraud detection** - Unusual patterns trigger review
- **Community flagging** - Users can report suspicious accounts

### Account Status

Accounts with suspicious activity show:
```
⚠️ UNDER REVIEW

Your account is being reviewed for unusual activity.
During this time:
  • Leaderboard rankings hidden
  • New badges won't appear
  • XP still counted for your progress

This usually resolves in 24 hours.
```

---

## ⚙️ Customization

### Gamification Settings

```
Preferences:
☑️ Show XP notifications
☑️ Send streak reminders
☑️ Display profile on leaderboards
☑️ Allow friends to see stats
☑️ Receive badge emails
```

### Privacy Options

```
Leaderboard Visibility:
  ○ Public (show in global rankings)
  ○ Friends Only (visible to connections)
  ○ Private (hide my stats)
```

---

## 📱 Mobile Experience

On mobile:
- Notifications keep streaks alive
- XP counter shows in notifications
- Badges unlock with celebrations
- Leaderboard accessible from profile

---

## 🔗 Related

- [Adaptive Learning](ADAPTIVE_LEARNING.md)
- [Code Duels](CODE_DUELS.md)
- [Architecture](../ARCHITECTURE.md)

---

Last updated: May 27, 2026
