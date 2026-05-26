# 🚀 PyScape - Adaptive AI Learning Platform

> **Learn Python. Master AI. Build Your First Project.**

PyScape is a **gamified, AI-powered learning platform** that guides you from Python fundamentals to building real AI applications. Features adaptive skill progression, real-time competitive code duels, interactive labs, and portfolio generation.

**Part of the PyScape Ecosystem:**  
[pyscape-basic](https://github.com/zxnb01/pyscape-basic) • [pyscape-multi-agent](https://github.com/zxnb01/pyscape-multi-agent) • [pyscape-research](https://github.com/zxnb01/pyscape-research)

---

## 🎯 What You Get

| Feature | Description |
|---------|-------------|
| **🎓 Adaptive Learning** | Personalized roadmap with 30+ Python & AI skills, auto-unlocking prerequisites |
| **⚔️ Real-time Code Duels** | Live 1v1 competitive coding battles with matchmaking and leaderboards |
| **🧠 ML Sandbox** | Execute Python, JavaScript, Java, C/C++ with instant feedback |
| **🎮 Gamification** | Earn XP, unlock badges, climb skill levels, build streaks |
| **📚 Interactive Labs** | Guided projects with step-by-step instructions |
| **📄 Portfolio Export** | PDF/Markdown portfolio showcasing completed projects |

---

## ⚡ Quick Start (5 minutes)

### Prerequisites
- Node.js 16+
- npm or yarn
- Git

### 1. Clone & Install
```bash
git clone https://github.com/zxnb01/pyscape-multi-generation.git
cd pyscape-multi-generation
npm install
```

### 2. Configure Environment
Create `.env` in the root:
```env
REACT_APP_SUPABASE_URL=your-supabase-url
REACT_APP_SUPABASE_ANON_KEY=your-anon-key
REACT_APP_GNEWS_API_KEY=your-gnews-key
REACT_APP_RAPIDAPI_KEY=your-rapidapi-key
```

[📋 Get API keys →](docs/GETTING_STARTED.md)

### 3. Start Development
```bash
npm start
```

Open [http://localhost:3000](http://localhost:3000)

**For Code Duels (optional):**
```bash
cd backend && npm install && npm run dev:duel
```

---

## 📚 Documentation

Complete guides and references:

| Guide | Purpose |
|-------|---------|
| [**Getting Started**](docs/GETTING_STARTED.md) | Step-by-step setup (10 min) |
| [**Architecture**](docs/ARCHITECTURE.md) | System design & data flow |
| [**Features**](docs/features/) | Deep dives into each feature |
| [**Database Schema**](docs/database/SCHEMA.md) | Complete data model reference |
| [**Deployment**](docs/guides/DEPLOYMENT.md) | Deploy to production |
| [**Troubleshooting**](docs/guides/TROUBLESHOOTING.md) | Common issues & solutions |
| [**Contributing**](docs/contributing/GUIDE.md) | How to contribute |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | React 18, Tailwind CSS, Framer Motion, CodeMirror |
| **Backend** | Node.js, Express, WebSockets |
| **Database** | Supabase (PostgreSQL + Auth) |
| **Real-time** | Supabase Realtime, WebSockets |
| **AI** | OpenAI/Anthropic API, LangChain |
| **Code Execution** | Judge0 API, Pyodide |

---

## 🎮 Core Features

### 1. Adaptive Learning Paths
Personalized skill graph with smart prerequisites:
- Auto-generated curriculum based on your goals
- Skills unlock as you master prerequisites
- Difficulty scales to your pace
- 30+ Python & AI topics

[Learn more →](docs/features/ADAPTIVE_LEARNING.md)

### 2. Code Duels ⚔️
Real-time competitive coding:
- 1v1 live coding battles
- Matchmaking by skill & language
- Instant code execution with test results
- XP rewards & global leaderboards

[Learn more →](docs/features/CODE_DUELS.md)

### 3. ML Sandbox
Multi-language code execution:
- **Python** - NumPy, Pandas, Matplotlib, etc.
- **JavaScript** - Browser-based, instant
- **Java** - Full standard library
- **C/C++** - GCC compiler support

[Learn more →](docs/features/ML_SANDBOX.md)

### 4. Gamification 🎮
Turn learning into a game:
- Earn XP from lessons, duels, projects
- Unlock badges for achievements
- Level progression (1-100)
- Daily streaks & leaderboards

[Learn more →](docs/features/GAMIFICATION.md)

### 5. Portfolio Export
Showcase your work professionally:
- Beautiful PDF/Markdown portfolio
- Display projects with metrics
- Shareable with GitHub, LinkedIn
- Impress recruiters

[Learn more →](docs/features/PORTFOLIO.md)

---

## 📁 Project Structure

```
pyscape-multi-generation/
├── src/                          # React frontend
│   ├── components/               # React components
│   │   ├── auth/                # Login/signup
│   │   ├── codeDuel/            # Duel system
│   │   ├── sandbox/             # Code executor
│   │   ├── roadmap/             # Skill graph
│   │   └── ...
│   ├── pages/                   # Page components
│   ├── services/                # API services
│   ├── context/                 # State management
│   └── utils/                   # Helper functions
├── backend/                      # Node.js backend
│   ├── duel-server.js           # WebSocket server
│   ├── server.js                # Express API
│   └── package.json
├── migrations/                   # Database migrations (29 files)
├── scripts/                      # Utility scripts
│   ├── maintenance/             # Database tools
│   └── migrations/              # Migration runners
├── docs/                         # 📚 Complete documentation
│   ├── GETTING_STARTED.md       # Setup guide
│   ├── ARCHITECTURE.md          # System design
│   ├── features/                # Feature guides
│   ├── database/                # Schema reference
│   ├── guides/                  # Deployment, troubleshooting
│   └── contributing/            # Contributing guide
├── public/                       # Static assets
├── package.json                  # Frontend dependencies
└── README.md                     # This file
```

---

## 🚀 Deployment

Deploy to production in minutes:

```bash
npm run build
```

See [Deployment Guide](docs/guides/DEPLOYMENT.md) for hosting options:
- **Vercel** (recommended, free tier)
- **Netlify** (easy, free tier)
- **Azure App Service** (enterprise)
- **Docker** (any platform)

---

## 🐛 Common Issues

### Cannot connect to WebSocket (Code Duels)
→ Ensure backend is running: `cd backend && npm run dev:duel`

### RapidAPI key not configured
→ Add `REACT_APP_RAPIDAPI_KEY` to `.env` and restart

### Code execution timeout
→ Check RapidAPI subscription limits

[👉 Full troubleshooting guide →](docs/guides/TROUBLESHOOTING.md)

---

## 🤝 Contributing

We welcome contributions! 

- [Contributing Guide](docs/contributing/GUIDE.md) - How to get started
- [Issues](https://github.com/yourusername/pyscape-multi-generation/issues) - Report bugs or request features
- [Discussions](https://github.com/yourusername/pyscape-multi-generation/discussions) - Ask questions, share ideas

---

## 📄 License

MIT License - see [LICENSE](LICENSE) file

---

## 🔗 Ecosystem

Part of the **PyScape Learning Platform Ecosystem:**

- **[pyscape-basic](https://github.com/yourusername/pyscape-basic)** - Foundational implementation
- **[pyscape-multi-agent](https://github.com/yourusername/pyscape-multi-agent)** - Advanced orchestration (this repo)
- **[pyscape-research](https://github.com/yourusername/pyscape-research)** - Research & experiments

---

## 💬 Support & Community

- 📖 [Documentation](docs/)
- 🐛 [Report Issues](https://github.com/zxnb01/pyscape-multi-generation/issues)
- 💡 [Discussions & Ideas](https://github.com/zxnb01/pyscape-multi-generation/discussions)
- 📧 [Contact](mailto:shaikzaiiinab@gmail.com)

---

## 🏆 Acknowledgments

Built with ❤️ for Python learners everywhere.

Thanks to:
- Supabase for database & auth
- Judge0 for code execution
- React community for amazing tools

---

**Ready to learn? [Get started →](docs/GETTING_STARTED.md)**
- Check your internet connection
- Verify your RapidAPI usage limits (150 requests/month on free plan)
- Ensure your code doesn't have infinite loops or excessive resource usage
- Try running simpler code first to test the connection

**Problem**: JavaScript code works but server-side languages don't

**Solution**:
- JavaScript runs locally, while Python/Java/C++ require RapidAPI
- Verify your RapidAPI key is correctly configured
- Check browser network tab for failed API requests
- Ensure you're subscribed to the Judge0 CE API on RapidAPI

### General Issues

**Problem**: Application won't start

**Solution**:
1. Run `npm install` to ensure all dependencies are installed
2. Check that all environment variables are set in `.env`
3. Verify Node.js version is 16 or higher
4. Clear npm cache: `npm cache clean --force`

## Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/amazing-feature`
3. Commit your changes: `git commit -m 'Add amazing feature'`
4. Push to the branch: `git push origin feature/amazing-feature`
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Acknowledgments

- Design inspiration from modern developer platforms and learning environments
- Algorithm visualizations inspired by AlgoViz and similar educational tools
