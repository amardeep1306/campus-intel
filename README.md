
#  Campus Intelligence Dashboard

A unified campus dashboard that brings together **Library**, **Cafeteria**, **Events**, and **Academics** data into one clean interface — powered by an MCP-style architecture and an AI assistant router.

**Live Demo → [https://campus-intel.onrender.com](https://campus-intel.onrender.com)**

---

## ✨ Features

-  **Library** — Book availability, study room status
-  **Cafeteria** — Daily menu, nutrition info, timings
-  **Events** — Workshops, club activities, campus events
-  **Academics** — Deadlines, course info, faculty details
-  **AI Assistant** — Ask anything in plain language, routed to the right source
-  **MCP Map** — Visual architecture of how data flows

---

##  Project Structure

```
campus-intelligence-dashboard/
├── public/                  # Frontend (HTML, CSS, JS)
│   ├── index.html
│   ├── styles.css
│   └── app.js
├── src/
│   ├── data/                # JSON data files
│   │   ├── academics.json
│   │   ├── cafeteria.json
│   │   ├── events.json
│   │   └── library.json
│   ├── mcp/                 # MCP source servers
│   │   ├── academics.js
│   │   ├── cafeteria.js
│   │   ├── events.js
│   │   ├── library.js
│   │   ├── registry.js
│   │   └── shared.js
│   ├── server/              # Backend logic
│   │   ├── assistantRouter.js
│   │   ├── http.js
│   │   └── mcpRuntime.js
│   └── server.js            # Main entry point
├── tests/
│   └── smoke.mjs            # Basic smoke tests
├── .env.example             # Environment variable template
├── .gitignore
├── package.json
└── README.md
```

---

##  Local Setup — Step by Step

### Prerequisites

Make sure these are installed on your computer:

| Tool | Version | Download |
|------|---------|----------|
| Node.js | v18 or higher | [nodejs.org](https://nodejs.org) |
| Git | Any | [git-scm.com](https://git-scm.com) |

Check if already installed:
```bash
node --version
git --version
```

---

### Step 1 — Clone the Repository

```bash
git clone https://github.com/YOUR-USERNAME/campus-intel.git
```

```bash
cd campus-intel
```

---

### Step 2 — Install Dependencies

```bash
npm install
```

---

### Step 3 — Create `.env` File

Create a `.env` file in the root folder of the project:

```bash
# Windows (Command Prompt)
copy .env.example .env

# Mac / Linux
cp .env.example .env
```

Or create the `.env` file manually and add the following:

```dotenv
PORT=4173
CAMPUS_NAME=Northstar Institute of Technology
```

---

### Step 4 — Start the Server

```bash
npm start
```

You should see this in the terminal:

```
Campus Intelligence Dashboard running at http://localhost:4173
```

---

### Step 5 — Open in Browser

Open your browser and go to:

```
http://localhost:4173
```

 **The dashboard is now running locally!**

---

##  Running Tests

```bash
npm test
```

This runs `tests/smoke.mjs` and checks all basic API endpoints.

---

##  API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/health` | Server health check |
| `GET` | `/api/dashboard` | Full dashboard snapshot |
| `POST` | `/api/assistant` | AI assistant query |
| `GET` | `/mcp/:source` | MCP source info |
| `POST` | `/mcp/:source` | MCP tool call |

### Example — Assistant Query

```bash
curl -X POST http://localhost:4173/api/assistant \
  -H "Content-Type: application/json" \
  -d '{"message": "Is an AI book available in the library?"}'
```

### Example — Dashboard Data

```bash
curl http://localhost:4173/api/dashboard
```

---

## ☁️ Deployment (Render.com)

### Step 1 — Push to GitHub

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/campus-intel.git
git push -u origin main
```

### Step 2 — Render Setup

1. Go to [render.com](https://render.com) → **New → Web Service**
2. Connect your GitHub repository
3. Use the following settings:

| Field | Value |
|-------|-------|
| Runtime | `Node` |
| Build Command | `npm install` |
| Start Command | `npm start` |
| Instance Type | `Free` |

4. Add the following Environment Variable:

| Key | Value |
|-----|-------|
| `CAMPUS_NAME` | `Northstar Institute of Technology` |

>  Do **not** add `PORT` — Render sets this automatically.

5. Click **Create Web Service** → Live in 3–5 minutes!

---

##  Updating Your Code After Deployment

Whenever you make changes locally, just run these 3 commands:

```bash
git add .
git commit -m "describe your change"
git push
```

Render will automatically detect the changes and redeploy.

---

##  Common Issues & Fixes

| Problem | Solution |
|---------|----------|
| `node: command not found` | Install Node.js from nodejs.org |
| `PORT already in use` | Change PORT in `.env` (e.g. 3000) |
| `Cannot find module` | Run `npm install` again |
| Site slow on first load | Free tier sleep mode — normal, wait ~50 seconds |
| Data not loading | Check `/api/health` in your browser |

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | Vanilla HTML, CSS, JavaScript |
| Backend | Node.js (no framework) |
| Architecture | MCP-style source routing |
| Hosting | Render.com |
| Data | Static JSON files |

---

## 📝 Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `PORT` | `4173` | Server port (local development only) |
| `CAMPUS_NAME` | — | Display name of the campus |

---

## 👤 Author

Built for **Problem Statement 1** — Amardeep Kumar

---

https://github.com/user-attachments/assets/29b69d3a-215e-4b6c-b9d0-d1c997c4e2e6


## 📄 License

MIT License — free to use and modify.
