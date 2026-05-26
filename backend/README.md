# PyScape Backend - WebSocket & Code Execution

Backend services for PyScape real-time features and code execution.

---

## 📋 Overview

This backend provides:
- **WebSocket Server** - Real-time Code Duel matchmaking and sessions
- **REST API** - Health checks and utilities
- **Judge0 Integration** - Secure code execution for multiple languages

---

## 🚀 Setup

### Install Dependencies

```bash
cd backend
npm install
```

### Configure Environment

Create `.env` in `backend/` directory:

```env
# Supabase (required for duels)
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your-anon-key

# Judge0 Code Execution (required for duels)
RAPIDAPI_KEY=your-rapidapi-key
RAPIDAPI_HOST=judge0-ce.p.rapidapi.com

# Optional
PORT=8080
NODE_ENV=development
```

---

## ▶️ Running the Backend

### Development Mode (with auto-reload)

```bash
# Start WebSocket server
npm run dev:duel

# Start REST API server
npm run dev
```

### Production Mode

```bash
# Start WebSocket server
npm run start:duel

# Start REST API server
npm start
```

---

## 🔌 WebSocket Server (`duel-server.js`)

Real-time communication for Code Duels.

### Runs on
```
ws://localhost:8080
```

### Features
- Player matchmaking (by difficulty + language)
- Duel session management
- Live code submission & testing
- Judge0 integration
- XP/leaderboard updates
- Real-time chat

### Client Connection Example

```javascript
const socket = new WebSocket('ws://localhost:8080');

socket.addEventListener('open', () => {
  socket.send(JSON.stringify({
    type: 'auth',
    token: jwtToken
  }));
});

socket.addEventListener('message', (event) => {
  const message = JSON.parse(event.data);
  console.log('Server:', message);
});
```

---

## 🔗 REST API Server (`server.js`)

Optional utility endpoints.

### Endpoints

#### Health Check
```
GET /api/health
Response: { status: "ok" }
```

#### Execute Code
```
POST /api/execute-code
Body: {
  code: "print('hello')",
  language: "python"
}
Response: {
  status: "success",
  output: "hello\n",
  runtime: 0.23
}
```

#### Get Problems
```
GET /api/problems?difficulty=intermediate&language=python
Response: [{ id, title, description, ... }]
```

---

## 🔐 Authentication

Uses **Supabase JWT tokens**:

1. User logs in via Supabase
2. Frontend receives JWT token
3. Frontend sends token to WebSocket
4. Backend validates with Supabase
5. Connection established

---

## 🔨 Judge0 Integration

Executes code securely in Docker containers.

### Setup Judge0 Access

1. Go to [RapidAPI Judge0](https://rapidapi.com/judge0-official/api/judge0-ce/)
2. Subscribe to free plan
3. Copy `X-RapidAPI-Key`
4. Add to `.env` as `RAPIDAPI_KEY`

### How It Works

1. User submits code in duel
2. Backend sends to Judge0 API
3. Judge0 executes in isolated container
4. Returns: status, output, runtime, memory
5. Backend compares against test cases
6. Awards XP if passed

### Supported Languages

- Python 3.10
- JavaScript (Node.js 18)
- Java 17
- C/C++ (GCC 11)
- And 20+ more

---

## 📦 Dependencies

- **ws** - WebSocket library
- **express** - REST API framework
- **cors** - Cross-Origin Resource Sharing
- **dotenv** - Environment variable management
- **@supabase/supabase-js** - Supabase client
- **axios** - HTTP requests (Judge0)

---

## 🔧 Development

### File Structure

```
backend/
├── duel-server.js      # WebSocket server
├── server.js           # REST API server
├── package.json        # Dependencies
├── .env                # Configuration (don't commit)
└── README.md           # This file
```

### Key Functions

See code comments in:
- `duel-server.js` - WebSocket handlers and matchmaking
- `server.js` - API endpoints

---

## 🧪 Testing Locally

### Test WebSocket Connection

```bash
# Terminal 1: Start server
npm run dev:duel

# Terminal 2: Test connection
node -e "const WebSocket = require('ws'); const ws = new WebSocket('ws://localhost:8080'); ws.on('open', () => console.log('Connected!'));"
```

### Test Code Execution

```bash
curl -X POST http://localhost:5000/api/execute-code \
  -H "Content-Type: application/json" \
  -d '{
    "code": "print(\"hello\")",
    "language": "python"
  }'
```

---

## 🚀 Deployment

See [Deployment Guide](../docs/guides/DEPLOYMENT.md) for hosting options:
- **Railway** - Easy WebSocket hosting
- **Render** - Free tier available
- **AWS EC2** - Full control
- **Docker** - Any platform

---

## 🐛 Troubleshooting

### "Cannot connect to WebSocket"
- Ensure server is running: `npm run dev:duel`
- Check port 8080 is not blocked
- Verify Supabase URL in `.env`

### "Judge0 execution fails"
- Verify `RAPIDAPI_KEY` is valid
- Check RapidAPI subscription is active
- Test API key via RapidAPI dashboard

### "Supabase auth fails"
- Verify `SUPABASE_URL` and `SUPABASE_ANON_KEY`
- Check Supabase project is accessible
- Ensure JWT token is valid (not expired)

---

## 📚 Related Documentation

- [Main README](../README.md)
- [Code Duels Feature](../docs/features/CODE_DUELS.md)
- [Architecture Overview](../docs/ARCHITECTURE.md)
- [Deployment Guide](../docs/guides/DEPLOYMENT.md)

---

**Questions? See the full documentation: [docs/](../docs/)**
```bash
curl -X POST http://localhost:5000/api/run \
  -H "Content-Type: application/json" \
  -d '{"code": "print(\"Hello World!\")", "language": "python"}'
```

## API Endpoints

### POST /api/run

Execute code in a sandboxed environment.

**Request Body:**
```json
{
  "code": "print('Hello World!')",
  "language": "python"
}
```

**Response:**
```json
{
  "stdout": "Hello World!\n",
  "stderr": "",
  "exitCode": 0,
  "error": null
}
```

### GET /api/health

Health check endpoint.

**Response:**
```json
{
  "status": "OK",
  "timestamp": "2024-01-01T12:00:00.000Z"
}
```

## Supported Languages

- **Python** (`.py`)
- **JavaScript** (`.js`)

## Security Features

- Execution timeout (10 seconds default)
- Temporary file cleanup
- CORS protection
- Input validation
- Process isolation

## Environment Variables

Copy `.env.example` to `.env` and customize:

```bash
cp .env.example .env
```

## Troubleshooting

1. **Port already in use**: Change PORT in `.env` file
2. **Python not found**: Ensure Python is in your system PATH
3. **CORS errors**: Check the frontend URL in server.js
4. **Timeout errors**: Increase MAX_EXECUTION_TIME in `.env`

## Production Deployment

For production, consider:
- Using Docker containers for better isolation
- Implementing rate limiting
- Adding authentication
- Using a process manager like PM2
- Setting up proper logging