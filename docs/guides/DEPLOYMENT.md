# Deployment Guide

How to deploy PyScape to production.

---

## 🚀 Pre-Deployment Checklist

- [ ] All tests passing (`npm test`)
- [ ] Build succeeds (`npm run build`)
- [ ] Environment variables documented
- [ ] Database migrations applied
- [ ] No console errors in dev
- [ ] Accessible on mobile
- [ ] Code reviewed

---

## 📦 Build for Production

```bash
# Build optimized production bundle
npm run build

# Output: ./build/ folder
# ~500 KB gzipped (React app)
```

---

## 🌐 Deployment Options

### Option 1: Vercel (Recommended)

**Best for:** Easiest, fastest, free tier available

#### Steps:
1. **Push code to GitHub**
2. **Go to [vercel.com](https://vercel.com)**
3. **Import Git repository**
4. **Add environment variables** (from `.env`)
5. **Deploy**

**Deployment time:** < 1 minute  
**Cost:** Free tier (~3 projects)

#### Environment Variables in Vercel:
```
REACT_APP_SUPABASE_URL=https://...
REACT_APP_SUPABASE_ANON_KEY=...
REACT_APP_GNEWS_API_KEY=...
REACT_APP_RAPIDAPI_KEY=...
```

---

### Option 2: Netlify

**Best for:** Static hosting, easy CI/CD

#### Steps:
1. **Push code to GitHub**
2. **Go to [netlify.com](https://netlify.com)**
3. **Click "New site from Git"**
4. **Select your repository**
5. **Set build command:** `npm run build`
6. **Set publish directory:** `build/`
7. **Add environment variables**
8. **Deploy**

**Deployment time:** < 2 minutes  
**Cost:** Free tier (~3 projects)

---

### Option 3: Azure App Service

**Best for:** Enterprise, integration with Azure ecosystem

#### Steps:
```bash
# 1. Create Azure resource group
az group create --name pyscape-rg --location eastus

# 2. Create App Service plan
az appservice plan create \
  --name pyscape-plan \
  --resource-group pyscape-rg \
  --sku B1 --is-linux

# 3. Create web app
az webapp create \
  --resource-group pyscape-rg \
  --plan pyscape-plan \
  --name pyscape-app \
  --runtime "NODE|18-lts"

# 4. Configure and deploy
# (See Azure docs for Git deployment)
```

**Cost:** ~$12-50/month depending on tier

---

### Option 4: Docker + Any Host

**Best for:** Maximum control, run anywhere

#### Create Dockerfile:
```dockerfile
FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci --only=production

COPY . .
RUN npm run build

EXPOSE 3000

CMD ["npm", "run", "start"]
```

#### Build & Push:
```bash
docker build -t pyscape:latest .
docker run -p 3000:3000 pyscape:latest
```

---

## 🔐 Environment Variables

### Production Variables

Create `.env.production` (don't commit to git):

```env
# Supabase (production project)
REACT_APP_SUPABASE_URL=https://prod-project.supabase.co
REACT_APP_SUPABASE_ANON_KEY=prod-anon-key

# APIs
REACT_APP_GNEWS_API_KEY=prod-gnews-key
REACT_APP_RAPIDAPI_KEY=prod-rapidapi-key

# Optional
REACT_APP_LOG_LEVEL=info
REACT_APP_API_URL=https://api.pyscape.io
```

### How to Add to Hosting:

**Vercel:**
- Settings → Environment Variables → Add

**Netlify:**
- Site settings → Build & deploy → Environment → Edit variables

**Docker:**
```bash
docker run -e REACT_APP_SUPABASE_URL=... pyscape:latest
```

---

## 🗄️ Database for Production

### Option A: Supabase Hosting (Recommended)

1. Create new Supabase project (production)
2. Run migrations:
   ```sql
   -- Copy/paste migrations/001_create_core_tables.sql
   -- Copy/paste migrations/002_create_duel_tables.sql
   -- ... (all other migrations)
   ```
3. Seed data (if needed):
   ```sql
   -- Run migrations/005_seed_python_skills.sql
   ```
4. Get production API keys
5. Add to `.env.production`

### Option B: Self-Hosted PostgreSQL

1. Set up PostgreSQL server
2. Run migrations on prod database
3. Update `REACT_APP_SUPABASE_URL` to point to self-hosted
4. Ensure SSL/TLS enabled
5. Set up daily backups

### Option C: Amazon RDS / Azure Database

Similar to self-hosted but managed service.

---

## 🎯 Backend Deployment (Code Duels)

If deploying Code Duel WebSocket server:

### Option 1: Railway

```bash
# Install Railway CLI
npm install -g @railway/cli

# Login
railway login

# Deploy
railway init
railway up
```

### Option 2: Render

1. Go to [render.com](https://render.com)
2. Create new Web Service
3. Connect GitHub repo
4. Set build command: `cd backend && npm install`
5. Set start command: `node duel-server.js`
6. Add environment variables
7. Deploy

### Option 3: AWS EC2

```bash
# 1. Launch EC2 instance
# 2. SSH into instance
ssh -i key.pem ubuntu@instance.ip

# 3. Install Node.js
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
sudo apt-get install -y nodejs

# 4. Clone repo and run
git clone https://github.com/yourusername/pyscape-multi-generation.git
cd pyscape-multi-generation/backend
npm install
npm run start:duel

# 5. Setup reverse proxy (Nginx)
# (See Nginx docs for WebSocket proxying)
```

---

## 📊 Monitoring

### Application Monitoring

```bash
# Option 1: Vercel Analytics
# Built-in with Vercel deployment

# Option 2: Sentry Error Tracking
npm install @sentry/react
# Initialize in src/index.js

# Option 3: LogRocket Session Replay
npm install logrocket
```

### Database Monitoring

Monitor in Supabase dashboard:
- Database stats
- Query performance
- Storage usage
- Realtime connections

---

## 🔄 CI/CD Pipeline

### GitHub Actions Example

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Vercel

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18
      - run: npm install
      - run: npm test
      - run: npm run build
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v25
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
```

---

## 🚨 Post-Deployment

### Verify Deployment

```bash
# 1. Check frontend loads
curl https://your-deployed-app.com

# 2. Test login
# (Try signing up in production)

# 3. Check APIs
# (Open DevTools, try creating an action)

# 4. Check database
# (Verify data saves correctly)

# 5. Monitor errors
# (Check Sentry, browser console)
```

### Setup Monitoring

1. **Error tracking**: Sentry
2. **Performance**: Vercel/Netlify analytics
3. **Uptime**: Pingdom or similar
4. **Logs**: Datadog or CloudWatch

### Backup Database

```bash
# Automated daily backups on Supabase
# (Check backup settings in Supabase)

# Manual backup:
pg_dump $DATABASE_URL > backup.sql
```

---

## 🔒 Security Checklist

- [ ] HTTPS enforced (redirect http → https)
- [ ] Environment variables never hardcoded
- [ ] Sensitive data never in Git history
- [ ] CORS configured correctly
- [ ] Rate limiting enabled on APIs
- [ ] Supabase RLS policies enabled
- [ ] Database encrypted
- [ ] Backups automated and tested

---

## 📈 Scaling

### As Traffic Grows:

1. **Frontend**: CDN (Vercel/Netlify provides)
2. **Backend**: Add load balancer, scale instances
3. **Database**: 
   - Increase Supabase plan
   - Add read replicas
   - Archive old duels

4. **Cache**: Redis for frequently accessed data

---

## 🆘 Troubleshooting

### "Deployment fails"

1. Check build logs
2. Verify all dependencies installed
3. Check environment variables set
4. Test locally: `npm run build && npm start`

### "App works locally but not production"

1. Check environment variables
2. Check database accessible from prod
3. Check API keys valid in prod
4. Check CORS settings

### "Database connection fails in prod"

1. Verify IP whitelisting
2. Check connection string format
3. Verify SSL/TLS settings
4. Check firewall rules

---

## 📚 More Resources

- [Vercel Docs](https://vercel.com/docs)
- [Netlify Docs](https://docs.netlify.com)
- [Supabase Deployment](https://supabase.com/docs/guides/deployment)
- [Node.js Production](https://nodejs.org/en/docs/guides/nodejs-docker-webapp/)

---

Last updated: May 27, 2026
