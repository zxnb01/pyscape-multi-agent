# Scripts & Utilities

This directory contains utility scripts for maintenance, debugging, and database operations.

## 📋 Directory Structure

```
scripts/
├── maintenance/    # Database checks and repairs
└── migrations/     # Migration runners
```

## 🔧 Maintenance Scripts

Use these to inspect and fix database issues:

### `check_db.js`
Verify database connectivity and schema integrity.

```bash
node scripts/maintenance/check_db.js
```

### `checkLessons.js`
Audit lessons for completeness and issues.

```bash
node scripts/maintenance/checkLessons.js
```

### `checkModules.js`
Validate module structure and content.

```bash
node scripts/maintenance/checkModules.js
```

### `checkQuizzes.js`
Verify quiz questions and answers.

```bash
node scripts/maintenance/checkQuizzes.js
```

### `applyQuizFix.js`
Fix common quiz data issues.

```bash
node scripts/maintenance/applyQuizFix.js
```

### `cleanupAll.js`
Run all maintenance checks and repairs.

```bash
node scripts/maintenance/cleanupAll.js
```

## ⚙️ Migration Scripts

### `runMigration.js`
Apply database migrations in order.

```bash
node scripts/migrations/runMigration.js
```

This runs all SQL files in `migrations/` sequentially.

### `runMigration015.js`
Apply generation queue migration specifically.

```bash
node scripts/migrations/runMigration015.js
```

### `runGamificationMigrations.js`
Apply gamification-related migrations.

```bash
node scripts/migrations/runGamificationMigrations.js
```

### `runQuizMigrations.js`
Apply quiz table migrations.

```bash
node scripts/migrations/runQuizMigrations.js
```

## ⚠️ Safety Notes

- **Back up database** before running scripts
- **Test on dev** database first
- **Read script code** before executing
- **Have database access** (admin role)

## 🚀 Common Tasks

### Fresh Database Setup

```bash
# 1. Run all migrations
npm run migrate

# 2. Seed initial data (optional)
npm run migrate-queue

# 3. Verify setup
node scripts/maintenance/check_db.js
```

### Fix Data Issues

```bash
# 1. Check what's wrong
node scripts/maintenance/checkLessons.js

# 2. Fix detected issues
node scripts/maintenance/applyQuizFix.js

# 3. Verify fixes
node scripts/maintenance/checkLessons.js
```

### Regular Maintenance

```bash
# Daily check
node scripts/maintenance/check_db.js

# Weekly full audit
node scripts/maintenance/cleanupAll.js
```

---

**Note:** These are internal tools. Not needed for normal use.
