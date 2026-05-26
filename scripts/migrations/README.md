# Database Migrations

Migration scripts for setting up and updating the PyScape database schema.

---

## 📁 Files

- `runMigration.js` - Apply all migrations in order
- `runMigration015.js` - Apply generation queue migration
- `runGamificationMigrations.js` - Apply gamification migrations
- `runQuizMigrations.js` - Apply quiz migrations

---

## 🚀 Running Migrations

### Apply All Migrations

```bash
npm run migrate
```

This runs all SQL files in `migrations/` sequentially:
- 001_create_core_tables.sql
- 002_create_duel_tables.sql
- 003_seed_dummy_problem.sql
- 004_create_roadmap_tables.sql
- 005_seed_python_skills.sql
- ... (and so on)

### Apply Specific Migration

```bash
cd migrations
# Or run individual SQL files via Supabase dashboard
```

---

## 📊 Migration Files Reference

| File | Purpose |
|------|---------|
| 001 | Core tables (profiles, modules, lessons, skills) |
| 002 | Duel tables (duels, submissions, stats) |
| 003 | Sample problem data |
| 004 | Roadmap & skill dependency tables |
| 005 | Python skills seed data |
| 006 | RLS policy disabling (debugging only) |
| 007 | Modules & lessons seed data |
| 008 | Projects seed data |
| 009 | Quiz table creation |
| 010 | Lesson content seed data |
| 011 | Lesson sublevel structure |
| 012 | Visualizer tutorials |
| 013 | Lesson generation tracking |
| 015 | Generation queue system |
| 016 | Fix escaped content |
| 017 | Module/lesson queue entries |
| 018 | Complete gamification system |
| 019 | Quiz tables creation |
| 020 | Additional quiz columns |
| 021 | Quiz RPC functions |
| 022 | Gamification permissions |
| 023 | Gamification functions verification |
| 024 | Foreign key fixes |
| 025 | Lesson part progress tracking |
| 026 | Lesson ordering fixes |
| 027 | Lesson level XP source fixes |
| 028 | Profiles table fixes |
| 029 | Lesson badge counting |

---

## ⚠️ Important Notes

1. **Order matters** - Run migrations sequentially (001 → 029)
2. **Idempotent** - Safe to run multiple times (uses `IF NOT EXISTS`)
3. **Reversible** - But no built-in rollback (always backup first)
4. **Connection required** - Must have Supabase credentials in `.env`

---

## 🔄 Workflow

### Fresh Setup

```bash
# 1. Clone repo
git clone ...
cd pyscape-multi-generation

# 2. Install dependencies
npm install

# 3. Create .env with Supabase credentials
# (See docs/GETTING_STARTED.md)

# 4. Run migrations
npm run migrate

# 5. Start dev server
npm start
```

### After Database Reset

```bash
# 1. Delete all tables in Supabase
# (Go to Supabase dashboard → Danger zone)

# 2. Re-run migrations
npm run migrate

# 3. Verify
node scripts/maintenance/check_db.js
```

---

## 🔧 Manual Migration (Supabase Dashboard)

If migration script fails:

1. Go to **Supabase Dashboard**
2. Click **SQL Editor**
3. Open migration file (e.g., `migrations/001_create_core_tables.sql`)
4. Copy entire content
5. Create new query in dashboard
6. Paste content
7. Click **Run**

---

## ❌ Troubleshooting

### "Migration fails"

1. Check file exists: `ls migrations/001_*`
2. Check SQL syntax (missing commas, etc.)
3. Try via Supabase dashboard manually
4. Check Supabase project is accessible

### "Table already exists error"

- Migrations use `IF NOT EXISTS` - safe to re-run
- If error persists, check table name spelling

### "Permission denied"

- Check `.env` credentials
- Verify account has admin access to Supabase project
- Try with different API key

---

## 📚 Related

- [Getting Started](../../docs/GETTING_STARTED.md)
- [Database Schema](../../docs/database/SCHEMA.md)
- [Troubleshooting](../../docs/guides/TROUBLESHOOTING.md)

---

**Questions? Check the full documentation: docs/database/SCHEMA.md**
