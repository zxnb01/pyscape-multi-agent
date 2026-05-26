# Getting Started with PyScape

A complete step-by-step guide to get PyScape running on your local machine.

## ⏱️ Time Required: 10-15 minutes

## 📋 Prerequisites Checklist

Before starting, ensure you have:

- [ ] **Node.js** 16+ ([Download](https://nodejs.org/))
- [ ] **npm** or **yarn** (usually comes with Node.js)
- [ ] **Git** ([Download](https://git-scm.com/))
- [ ] **GitHub Account** (for cloning the repo)
- [ ] **Supabase Account** (free tier at [supabase.com](https://supabase.com))
- [ ] **RapidAPI Account** (free tier at [rapidapi.com](https://rapidapi.com))

### Verify Installations

Open your terminal and run:

```bash
node --version  # Should be v16 or higher
npm --version   # Should be v7 or higher
git --version   # Should show a version
```

---

## 🚀 Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/pyscape-multi-generation.git
cd pyscape-multi-generation
```

---

## 📦 Step 2: Install Frontend Dependencies

```bash
npm install
```

This may take 2-3 minutes. Wait for it to complete.

---

## 🔧 Step 3: Set Up Supabase

### 3.1 Create a Supabase Account
1. Go to [supabase.com](https://supabase.com)
2. Sign up with GitHub (recommended) or email
3. Create a new project (any name, any region)
4. Wait for project initialization (2-3 minutes)

### 3.2 Get Your Credentials
In your Supabase dashboard:
1. Go to **Settings** → **API**
2. Copy your **Project URL** (under "API URL")
3. Copy your **Anon Public Key** (under "anon key")

### 3.3 Run Database Migrations
In Supabase dashboard:
1. Go to **SQL Editor**
2. Create a new query
3. Copy the migration SQL from `migrations/001_create_core_tables.sql`
4. Paste and execute

Repeat for:
- `migrations/002_create_duel_tables.sql`
- `migrations/004_create_roadmap_tables.sql`
- `migrations/005_seed_python_skills.sql`
- And all other migrations in order

> **Tip:** Or use the migration runner (see Step 5)

---

## 🔑 Step 4: Configure Environment Variables

### 4.1 Create `.env` File

In the root directory, create a file named `.env`:

```bash
# Windows (PowerShell)
New-Item .env

# macOS/Linux (Terminal)
touch .env
```

### 4.2 Add API Keys

Open `.env` in your editor and add:

```env
# Supabase (required)
REACT_APP_SUPABASE_URL=https://YOUR-PROJECT.supabase.co
REACT_APP_SUPABASE_ANON_KEY=YOUR-ANON-KEY

# News API (required for AI news dashboard)
REACT_APP_GNEWS_API_KEY=YOUR-GNEWS-KEY

# Judge0 API (required for code execution)
REACT_APP_RAPIDAPI_KEY=YOUR-RAPIDAPI-KEY
```

### 4.3 Get the API Keys

#### Supabase Keys
- Already copied in Step 3.2 ✓

#### GNews API Key
1. Go to [gnews.io](https://gnews.io)
2. Sign up for free account
3. Copy your API key
4. Add to `.env` as `REACT_APP_GNEWS_API_KEY`

#### RapidAPI Key (for Judge0)
1. Go to [RapidAPI Judge0](https://rapidapi.com/judge0-official/api/judge0-ce/)
2. Sign up (free tier available)
3. Click **Subscribe to Test**
4. Copy your **X-RapidAPI-Key**
5. Add to `.env` as `REACT_APP_RAPIDAPI_KEY`

---

## 🏃 Step 5: Start Development Server

```bash
npm start
```

This will:
- Start React development server
- Open [http://localhost:3000](http://localhost:3000) automatically
- Show hot reload on file changes

You should see the PyScape login page. 🎉

---

## ⚔️ Step 6: (Optional) Set Up Code Duel Backend

For real-time code duels, start the WebSocket server:

```bash
cd backend
npm install
npm run dev:duel
```

The server will run on `ws://localhost:8080`.

> **Note:** You can use PyScape without this, but code duels won't work.

---

## ✅ Step 7: Verify Everything Works

1. **Frontend loads** - See login page at http://localhost:3000
2. **Can sign up** - Create a test account
3. **Database connected** - Try selecting topics (if connected, they'll save)
4. **Code Duel backend** (optional) - Check terminal shows "WebSocket server listening"

---

## 🐛 Troubleshooting

### npm install fails
```bash
# Clear npm cache
npm cache clean --force

# Try again
npm install
```

### "Cannot find module" errors after npm install
```bash
# Delete node_modules and reinstall
rm -r node_modules package-lock.json
npm install
```

### ".env file not found" or API key errors
1. Ensure `.env` file is in the **root directory** (not `src/`)
2. Verify no spaces around `=` signs
3. Restart development server after editing `.env`

### Supabase connection failed
1. Verify `REACT_APP_SUPABASE_URL` starts with `https://`
2. Ensure project is not paused (check Supabase dashboard)
3. Check database migrations were run successfully

### Port 3000 already in use
```bash
# macOS/Linux - kill process on port 3000
lsof -ti:3000 | xargs kill -9

# Windows - find and kill the process
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

---

## 📚 Next Steps

- ✅ [Run database migrations](../migrations/)
- 📖 [Read architecture overview](ARCHITECTURE.md)
- 🎮 [Explore features](features/)
- 🤝 [Setup contributions](contributing/GUIDE.md)

---

## 💬 Need Help?

- 📖 [Full troubleshooting guide](guides/TROUBLESHOOTING.md)
- 🐛 [Report issues on GitHub](https://github.com/yourusername/pyscape-multi-generation/issues)
- 💡 [Start a discussion](https://github.com/yourusername/pyscape-multi-generation/discussions)

---

**Happy learning! 🚀**
