# Troubleshooting Guide

Solutions to common issues when using PyScape.

---

## 🔧 Setup Issues

### "Cannot find module" errors

**Problem:** After `npm install`, getting module not found errors

**Solutions:**
```bash
# 1. Clear npm cache
npm cache clean --force

# 2. Delete lock files and reinstall
rm package-lock.json node_modules
npm install

# 3. If using npm 8+, try npm ci instead
npm ci
```

### ".env file not found" or missing API keys

**Problem:** Environment variables not loading, blank API keys in app

**Solutions:**
1. Ensure `.env` file is in **root directory** (not in `src/`)
2. Verify no spaces around `=` sign:
   ```env
   ✅ CORRECT:
   REACT_APP_SUPABASE_URL=https://xyz.supabase.co
   
   ❌ WRONG:
   REACT_APP_SUPABASE_URL = https://xyz.supabase.co
   ```
3. Restart development server after editing `.env`:
   ```bash
   # Kill the running server
   Ctrl+C
   
   # Start again
   npm start
   ```

### Port 3000 already in use

**Problem:** "Port 3000 is already in use" error

**Solutions:**
```bash
# macOS/Linux:
lsof -ti:3000 | xargs kill -9

# Windows (PowerShell):
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Or use a different port:
PORT=3001 npm start
```

### Node version mismatch

**Problem:** "Node version 12 is not supported"

**Solution:**
```bash
# Check your Node version
node --version

# Should be v16 or higher
# If not, download from https://nodejs.org/
```

---

## 🗄️ Database Issues

### "Connection refused" to Supabase

**Problem:** Cannot connect to database, all features broken

**Solutions:**
1. **Verify credentials** in `.env`:
   ```bash
   echo $REACT_APP_SUPABASE_URL
   echo $REACT_APP_SUPABASE_ANON_KEY
   ```

2. **Check Supabase project status**:
   - Go to [supabase.com](https://supabase.com)
   - Project paused? Resume it
   - Project deleted? Create new one

3. **Verify network connection**:
   - Can you ping Supabase domain?
   - Firewall blocking? Check corporate network

4. **Check URL format**:
   ```env
   ✅ CORRECT:
   REACT_APP_SUPABASE_URL=https://YOUR-PROJECT.supabase.co
   
   ❌ WRONG (missing https, .co):
   REACT_APP_SUPABASE_URL=YOUR-PROJECT.supabase.com
   ```

### "RLS policy violation" or permission denied errors

**Problem:** Can read but not write to database

**Solutions:**
1. **Check Row Level Security (RLS)** is enabled correctly:
   - Supabase Dashboard → SQL Editor
   - Run: `SELECT * FROM information_schema.tables`
   - Verify RLS is on for your table

2. **Verify RLS policies** allow your user:
   - Test with authenticated user, not anon key
   - Check policies include your user ID

3. **Run migrations** if table was just created:
   ```bash
   npm run migrate
   ```

### Migrations fail to run

**Problem:** Database migrations fail with SQL errors

**Solutions:**
1. **Check migration files exist**:
   ```bash
   ls migrations/
   ```

2. **Run migrations individually**:
   - Go to Supabase SQL Editor
   - Copy/paste each migration file
   - Execute one at a time to find which fails

3. **Check for syntax errors**:
   - Look for typos in SQL
   - Verify table/column names match

---

## 🔐 Authentication Issues

### "Cannot sign up" or sign-up fails

**Problem:** Sign-up button doesn't work, infinite loading

**Solutions:**
1. **Verify Supabase Auth is enabled**:
   - Supabase Dashboard → Authentication → Providers
   - Email/Password provider is enabled

2. **Check for network errors**:
   - Open browser DevTools (F12)
   - Go to Network tab
   - Try signing up again
   - Look for failed requests to Supabase

3. **Clear browser cache**:
   ```javascript
   // In browser console:
   localStorage.clear()
   sessionStorage.clear()
   location.reload()
   ```

4. **Try incognito mode**:
   - Browser extensions sometimes interfere
   - Test in private/incognito window

### "Not authorized" or permissions denied

**Problem:** Signed in but getting permission errors

**Solutions:**
1. **Sign out and sign in again**:
   - Refresh auth token
   - Clear browser storage

2. **Check Supabase auth is configured**:
   - Correct API keys in `.env`
   - Correct Supabase project selected

3. **Verify user exists** in Supabase:
   - Go to Supabase Dashboard
   - Authentication → Users
   - Your account should be listed

---

## 🎮 Code Sandbox Issues

### "Code execution timeout"

**Problem:** Code runs forever, execution times out (5+ seconds)

**Solutions:**
1. **Find infinite loops**:
   ```python
   # ❌ BAD: Infinite loop
   while True:
       print("hello")
   
   # ✅ GOOD: Add exit condition
   for i in range(10):
       print("hello")
   ```

2. **Optimize slow code**:
   ```python
   # ❌ BAD: O(n²) complexity
   for i in range(1000000):
       for j in range(1000000):
           pass
   
   # ✅ GOOD: Optimize algorithm
   # Use appropriate data structures
   ```

3. **Break into smaller pieces**:
   - Test one function at a time
   - Narrow down the slow part

### "Memory exceeded" error

**Problem:** Code uses > 256 MB memory

**Solutions:**
1. **Avoid loading large datasets**:
   ```python
   # ❌ BAD: Loads 1M rows into memory
   data = [i for i in range(1000000)]
   
   # ✅ GOOD: Use generator (lazy evaluation)
   data = (i for i in range(1000000))
   ```

2. **Process in chunks**:
   ```python
   # ✅ GOOD: Process batch by batch
   for batch in get_batches(1000000, batch_size=1000):
       process(batch)
   ```

3. **Use smaller data**:
   ```python
   # For testing, use small dataset
   test_data = list(range(1000))  # Not 1,000,000
   ```

### "Import error" - module not found

**Problem:** `ImportError: No module named 'tensorflow'`

**Solutions:**
1. **Use only pre-installed packages**:
   ```python
   # ✅ WORKS:
   import numpy, pandas, matplotlib, requests
   
   # ❌ DOESN'T WORK (not installed):
   import tensorflow
   import pytorch
   ```

2. **See available packages**:
   - Check [Python sandbox docs](../features/ML_SANDBOX.md)
   - List of 100+ pre-installed packages

3. **Use pip install alternative**:
   - Sandbox doesn't support `pip install`
   - Use only built-in and pre-installed packages

### "Plot not showing" in Matplotlib

**Problem:** `plt.plot()` doesn't show visualization

**Solutions:**
```python
# ✅ CORRECT: Use plt.show()
import matplotlib.pyplot as plt
plt.plot([1, 2, 3])
plt.show()  # ← REQUIRED

# ✅ ALSO WORKS: Return figure
# (Will display automatically)
```

---

## ⚔️ Code Duel Issues

### "Cannot connect to WebSocket server"

**Problem:** Can't join duels, WebSocket connection fails

**Solutions:**
1. **Ensure backend is running**:
   ```bash
   cd backend
   npm install
   npm run dev:duel
   ```
   Look for: `WebSocket server listening on ws://localhost:8080`

2. **Check backend `.env`**:
   ```env
   SUPABASE_URL=your-url
   SUPABASE_ANON_KEY=your-key
   RAPIDAPI_KEY=your-key
   ```

3. **Verify ports**:
   - Frontend: http://localhost:3000
   - Backend: ws://localhost:8080
   - Check firewall isn't blocking

4. **Try in different browser**:
   - WebSocket might be blocked by extension
   - Test in incognito mode

### "Code execution failed" during duel

**Problem:** Code execution returns error, can't test

**Solutions:**
1. **Check RapidAPI key**:
   - `REACT_APP_RAPIDAPI_KEY` in `.env`
   - Valid? Not expired?
   - Restart frontend after adding key

2. **Verify Judge0 subscription**:
   - Go to [RapidAPI Judge0](https://rapidapi.com)
   - Check subscription is active
   - Check usage limit not exceeded

3. **Check code syntax**:
   ```python
   # ✅ CORRECT syntax
   def solve(x):
       return x * 2
   
   # ❌ SYNTAX ERROR
   def solve(x)  # Missing :
       return x * 2
   ```

4. **Test locally first**:
   - Verify code runs in sandbox
   - Then submit in duel

### "Stuck in queue" - waiting 5+ minutes

**Problem:** Matchmaking doesn't find opponent

**Solutions:**
1. **Check off-hours**:
   - More players online during peak hours (evenings)
   - Try at different time

2. **Lower difficulty**:
   - Beginner has more matches
   - Switch from Advanced to Intermediate

3. **Try different language**:
   - Python is most popular
   - Try JavaScript or Java if queue is empty

4. **Test connection**:
   - Ping pyscape.io
   - Check internet speed

5. **Refresh**:
   - Leave queue and rejoin
   - Sometimes resolves stale connections

### "Opponent disconnected" mid-duel

**Problem:** Opponent disconnects, duel ends

**Solutions:**
1. **Not your problem!** You still get XP
2. **Reconnect** - Go back to dashboard, rejoin queue
3. **Technical issues**:
   - Check your internet
   - If frequent, restart browser

---

## 🎨 UI/UX Issues

### "Lesson doesn't load"

**Problem:** Clicking lesson shows loading spinner forever

**Solutions:**
1. **Refresh page**:
   ```
   Press F5 or Ctrl+R
   ```

2. **Clear browser cache**:
   - Chrome: DevTools → Application → Clear Storage
   - Firefox: Preferences → Privacy → Clear History

3. **Check database connection**:
   - Can you see other pages loading?
   - If nothing loads, likely database issue

4. **Try different browser**:
   - Browser extension issue?
   - Test in Chrome, Firefox, Safari

### "Skills locked when should be unlocked"

**Problem:** Skill shows as locked but prerequisites are complete

**Solutions:**
1. **Refresh browser**:
   ```
   Hard refresh: Ctrl+Shift+R (or Cmd+Shift+R on Mac)
   ```

2. **Wait for sync**:
   - Database updates can take 1-2 seconds
   - Refresh after 2 seconds

3. **Check prerequisites**:
   - Go to Roadmap
   - Verify prerequisites actually show "mastered"
   - Check database didn't lose progress

---

## 📊 Performance Issues

### "App is slow" or sluggish

**Problem:** Clicking buttons takes long, animations stutter

**Solutions:**
1. **Check Network tab**:
   - DevTools → Network
   - Are API calls slow?
   - Is database slow?

2. **Reduce open tabs**:
   - Too many tabs = less RAM
   - Close unnecessary tabs

3. **Restart browser**:
   - Clears memory
   - Refreshes connections

4. **Check internet**:
   - Run speed test
   - Low bandwidth = slow app

5. **Use lighter browser**:
   - Chrome faster than Firefox for most
   - Safari fastest on Mac

---

## 🆘 Getting More Help

### Still stuck?

1. **Check docs**:
   - [Architecture](../ARCHITECTURE.md)
   - [Feature guides](../features/)
   - [API reference](API.md)

2. **Search GitHub issues**:
   - Similar problem already reported?
   - Solutions in comments?

3. **Create an issue**:
   - Include error message
   - Steps to reproduce
   - Your environment (OS, browser, Node version)
   - Screenshots

4. **Start discussion**:
   - Ask question in Discussions
   - Get help from community

5. **Contact maintainers**:
   - Comment on related issue
   - Email: [maintainer email]

---

## 📝 Providing Good Bug Reports

### Great bug report includes:

```markdown
## Environment
- OS: Windows 11
- Browser: Chrome 120
- Node version: v18.0.0

## Steps to Reproduce
1. Sign in as user@example.com
2. Click "Learn" → "Variables"
3. Click "Next" button
4. See error

## Expected
Lesson loads successfully

## Actual
Error: "Cannot read property..."

## Screenshot
[image of error]

## Browser Console Error
Error stack trace...
```

---

**Having trouble? Let us know! 💬**

Last updated: May 27, 2026
