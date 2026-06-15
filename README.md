# Unified Campus Intelligence Dashboard

This project is a complete working implementation of the PDF problem statement:

> Build a Unified Campus Intelligence Dashboard with an embedded AI Assistant that queries independent MCP servers for campus data sources such as library, cafeteria, events, and academics.

The app runs locally with plain Node.js and does not need `npm install`. It includes a polished responsive dashboard UI, live JSON-RPC MCP-style endpoints, a natural-language assistant router, sample campus data, and a smoke test.

## Requirement Analysis

The problem statement asks for:

- Independent MCP servers for distinct campus data sources.
- An assistant that routes student questions to the correct live source.
- A unified dashboard that surfaces results from multiple systems.
- No single giant database.
- Optional personalization/authentication.
- A clear repository with setup instructions and demo-ready behavior.

This project implements the core flow by keeping each campus source in its own module and data file. The assistant does not read from one central database. It selects the relevant source tools and calls them at request time.

## Features

- Responsive campus dashboard UI for library, cafeteria, events, and academic notices.
- Embedded assistant that answers multi-source student questions.
- MCP-style JSON-RPC endpoints:
  - `POST /mcp/library`
  - `POST /mcp/cafeteria`
  - `POST /mcp/events`
  - `POST /mcp/academics`
- Source tools support `tools/list`, `tools/call`, and `source/overview`.
- Dashboard APIs:
  - `GET /api/health`
  - `GET /api/dashboard`
  - `POST /api/assistant`
- Offline demo mode with deterministic routing, so it works without API keys.
- Smoke test that verifies all main routes.

## Tech Stack

- Frontend: HTML, CSS, and browser JavaScript served by Node.
- Backend: Node.js HTTP server with ES modules.
- MCP layer: JSON-RPC 2.0 style tool endpoints.
- AI assistant layer: natural-language intent router with tool traces.
- Data: separate JSON files per source.

## Quick Start

```bash
npm start
```

Open:

```text
http://localhost:4173
```

To use a different port:

```bash
PORT=5050 npm start
```

On Windows PowerShell:

```powershell
$env:PORT=5050; npm start
```

## Test

```bash
npm test
```

The test starts the server on a test port and verifies:

- Health endpoint responds.
- Dashboard has four live sources.
- Assistant returns a routed answer.
- MCP `tools/list` works for the library source.
- MCP `tools/call` returns library search results.

## Demo Prompts

Try these in the assistant panel:

- `Is an AI book available and what workshop is today?`
- `Show vegan lunch options and upcoming tech events.`
- `What academic deadlines should I watch this week?`
- `Can I borrow a web development book and submit my project this week?`

## Architecture

```text
Browser UI
   |
   | GET /api/dashboard
   | POST /api/assistant
   v
Assistant Router
   |
   | calls source tools live
   v
MCP-style source servers
   |-- /mcp/library
   |-- /mcp/cafeteria
   |-- /mcp/events
   |-- /mcp/academics
   |
Separate JSON data files
```

## MCP Request Example

```bash
curl -X POST http://localhost:4173/mcp/library \
  -H "content-type: application/json" \
  -d "{\"jsonrpc\":\"2.0\",\"id\":1,\"method\":\"tools/call\",\"params\":{\"name\":\"search_library\",\"arguments\":{\"query\":\"AI book available\"}}}"
```

## Project Structure

```text
campus-intelligence-dashboard/
  public/
    index.html
    styles.css
    app.js
  src/
    data/
      academics.json
      cafeteria.json
      events.json
      library.json
    mcp/
      academics.js
      cafeteria.js
      events.js
      library.js
      registry.js
      shared.js
    server/
      assistantRouter.js
      http.js
      mcpRuntime.js
    server.js
  tests/
    smoke.mjs
```

## Notes for Submission

- Record the demo with the dashboard open at `http://localhost:4173`.
- Show the assistant answering at least one multi-source question.
- Show `npm test` passing.
- Push the project to GitHub and add a deployed link if hosted.
