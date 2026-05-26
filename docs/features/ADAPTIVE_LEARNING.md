# Adaptive Learning Paths

Learn how PyScape personalizes your learning journey based on your goals, pace, and progress.

---

## 🎯 Overview

The Adaptive Learning Path system automatically generates a personalized curriculum based on:
- **Your goals** (topics selected during onboarding)
- **Your progress** (skills mastered so far)
- **Prerequisites** (what you need to learn first)
- **Your pace** (difficulty level you're learning at)

---

## 🗺️ How It Works

### 1. Interest Selection (Onboarding)

When you first sign up, select your learning goals:
- Python Basics
- Data Science
- Machine Learning
- Generative AI
- Web Development
- etc.

These topics determine which skills appear in your roadmap.

### 2. Skill Graph Generation

Based on your selections, the system builds a **Directed Acyclic Graph (DAG)** of ~30 skills:

```
Python Basics
├── Variables & Data Types ← START
├── Control Flow (if/else/loops)
│   └── Depends on: Variables & Data Types
├── Functions
│   └── Depends on: Variables & Data Types
└── Data Structures (lists, dicts, tuples)
    └── Depends on: Control Flow

Data Science (if selected)
├── NumPy Fundamentals
│   └── Depends on: Variables & Data Types
├── Pandas DataFrames
│   └── Depends on: NumPy Fundamentals
└── Data Visualization
    └── Depends on: Pandas DataFrames
```

### 3. Prerequisite Gating

Skills automatically **unlock** when you master their prerequisites:

- **Locked** 🔒 - Prerequisites not completed yet
- **Eligible** ✨ - Prerequisites done, ready to learn
- **In Progress** 📚 - Currently learning (0-99% complete)
- **Mastered** ✅ - 100% complete

### 4. Progression Tracking

Your **mastery** is tracked as a 0-100% score:

```
Variables & Data Types: 87% → Continue learning
Control Flow: 42% → Keep practicing
Functions: 0% → Locked (waiting for Variables completion)
```

Progress comes from:
- Completing lessons (read, quiz, code exercises)
- Passing lessons at higher difficulty levels
- Earning badges
- Completing projects

### 5. Recommended Next Steps

The system always shows you **what to learn next**:

1. Complete lessons in-progress toward higher mastery
2. Unlock newly eligible skills (prerequisites just completed)
3. Prepare for advanced topics (show connected skills)

---

## 📊 Skill Mastery Calculation

Your mastery for a skill is calculated from:

| Source | Weight | Example |
|--------|--------|---------|
| Reading lessons | 20% | You read "Variables in Python" |
| Quiz attempts | 30% | You scored 85% on the quiz |
| Code exercises | 40% | You solved 8/10 coding problems |
| Project usage | 10% | You applied it in a project |

**Formula:**
```
Mastery = (0.2 × lesson_progress) + 
          (0.3 × quiz_score) + 
          (0.4 × exercise_completion) + 
          (0.1 × project_usage)
```

---

## 🎓 Lesson Structure

Each skill is taught through **multi-level lessons**:

### Level 1: Foundations
- **Reading material** - What is this concept?
- **Examples** - Real-world use cases
- **Key points** - Important facts to remember

### Level 2: Applied Learning
- **Quiz** - Test your understanding
- **Code exercise** - Write actual code
- **Mini-project** - Build something with the concept

### Level 3: Mastery
- **Advanced concepts** - Edge cases, optimization
- **Complex problems** - Real-world challenges
- **Project integration** - Use in larger context

You unlock each level by completing the previous one.

---

## 🏆 Badges & Achievements

Unlock badges as you progress:

| Badge | Earned When | Reward |
|-------|-------------|--------|
| 🎯 First Steps | Complete first lesson | +200 XP |
| 🔥 Streak Master | 7-day learning streak | +500 XP |
| ⭐ Skill Expert | Master a skill (100%) | +300 XP + badge |
| 🎓 Python Master | Master all Python skills | +1000 XP + title |
| ⚡ Speed Learner | Complete level 3 in one day | +250 XP |

---

## 📈 Your Roadmap Dashboard

See your progress at a glance:

```
Python Basics (Domain)
  ✅ Variables & Data Types (87%)
  ✅ Control Flow (72%)
  ⏳ Functions (in progress - 42%)
  🔒 Lambdas (locked - wait for Functions)

Data Science (Domain)  
  ✨ NumPy Basics (eligible - starts soon)
  🔒 Pandas DataFrames (locked)

Overall Progress: 48% (12/25 skills)
Next Milestone: Master Functions (80% → 100%)
```

---

## ⚙️ How Adaptive Learning Works

### Smart Recommendations

The system learns your pace:
- Learning Python basics in 2 days? Suggest advanced topics
- Taking your time? Suggest more practice exercises
- Struggling with quizzes? Suggest re-reading, different examples

### Difficulty Adjustment

Choose your learning style:
- **Foundational** - Detailed explanations, step-by-step
- **Standard** - Balanced theory and practice
- **Advanced** - Concepts + complex problems, minimal hand-holding

Content difficulty adjusts automatically.

### Personalized Sequencing

Skills unlock in optimal order:
- Prerequisites always come first (Variables before Loops)
- Related skills grouped together (All data structures together)
- Natural progression from simple to complex

---

## 🎮 Gamification Integration

Combine learning with competition:

- **Earn XP** from lessons and projects
- **Unlock levels** as you progress
- **Compete in Code Duels** against other learners
- **Climb leaderboards** (by skill, language, overall)

---

## 📊 Progress Tracking

View detailed statistics:

```
Learning Summary
├── Total XP: 2,450
├── Current Level: 5
├── Skills Mastered: 8/25
├── Total Learning Time: 12.5 hours
└── Longest Streak: 9 days

Recent Activity
├── Completed: "Functions in Python" (92%)
├── Earned: ⭐ Skill Expert badge
└── Next: "Lambdas & Comprehensions"
```

---

## 🔄 Resetting Progress

Want to revisit a topic?
- **Refresh skill** - Reset mastery to 0%, relearn content
- **Change topics** - Select different topics, regenerate roadmap
- **Skip ahead** - (With caution) Unlock later topics if confident

---

## 💡 Tips for Success

1. **Set realistic goals** - Select 2-3 topics, not everything
2. **Daily practice** - Even 15 minutes builds streaks and mastery
3. **Complete levels** - Don't skip Level 1 (foundations matter)
4. **Do the exercises** - 40% of mastery comes from coding practice
5. **Use code duels** - Apply skills against real opponents
6. **Don't rush** - Mastery is ~100+ hours per skill

---

## 🔗 Related

- [Gamification System](GAMIFICATION.md)
- [Code Duels](CODE_DUELS.md)
- [Architecture Overview](../ARCHITECTURE.md)

---

Last updated: May 27, 2026
