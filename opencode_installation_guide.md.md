# ⚙️ OpenCode CLI & Web Guide (Raspberry Pi / Linux)

This guide explains how to use **OpenCode via CLI, automation, and web interface**, optimized for Raspberry Pi setups.

---

## 1️⃣ Basic Usage

Run OpenCode without arguments:

```bash
opencode
```

👉 This starts the **interactive TUI (Terminal UI)**

---

## 2️⃣ CLI Mode (Non-interactive)

You can run OpenCode directly from the command line.

### Example

```bash
opencode run "Explain how closures work in JavaScript"
```

👉 Ideal for:

* scripting
* automation
* pipelines

---

## 3️⃣ Common Flags

```bash
opencode --model anthropic/claude-sonnet-4-5
```

### Useful flags

* `-c` → continue last session
* `-s` → specify session
* `--fork` → fork session
* `--agent` → use custom agent
* `--prompt` → initial prompt

---

## 4️⃣ Automation (Core Feature)

### Run with files

```bash
opencode run "Refactor this file" -f app.py
```

---

### JSON output (for integrations)

```bash
opencode run "Explain this code" --format json
```

👉 Useful for:

* Make.com
* Python scripts
* AI pipelines

---

## 5️⃣ Headless Server (Key Feature)

Run OpenCode as a persistent backend:

```bash
opencode serve
```

👉 Starts a local HTTP server

---

### Attach to the server

```bash
opencode run --attach http://localhost:4096 "Explain async/await"
```

### Why this matters

* avoids cold starts
* keeps context alive
* improves performance

---

## 6️⃣ Web Interface

Launch OpenCode in your browser:

```bash
opencode web
```

👉 Automatically opens a web UI

---

### Access from other devices

```bash
opencode web --hostname 0.0.0.0 --port 4096
```

Then open:

```
http://YOUR_RPI_IP:4096
```

---

### Security (IMPORTANT)

```bash
OPENCODE_SERVER_PASSWORD=yourpassword opencode web
```

---

## 7️⃣ TUI + Web Together

Run both interfaces simultaneously:

```bash
# Terminal 1
opencode web --port 4096

# Terminal 2
opencode attach http://localhost:4096
```

👉 Shared sessions and state

---

## 8️⃣ Agents

### List agents

```bash
opencode agent list
```

---

### Create agent

```bash
opencode agent create
```

👉 Guided setup for custom AI agents

---

## 9️⃣ MCP (Model Context Protocol)

### Add MCP server

```bash
opencode mcp add
```

---

### List MCP servers

```bash
opencode mcp ls
```

👉 Used for integrating:

* external tools
* APIs
* databases

---

## 🔟 Authentication

```bash
opencode auth login
```

---

### List providers

```bash
opencode auth ls
```

---

## 1️⃣1️⃣ Models

```bash
opencode models
```

Filter by provider:

```bash
opencode models anthropic
```

---

## 1️⃣2️⃣ Sessions

### List sessions

```bash
opencode session list
```

---

### Export session

```bash
opencode export
```

---

### Import session

```bash
opencode import session.json
```

---

## 1️⃣3️⃣ Usage Stats

```bash
opencode stats
```

👉 Shows:

* token usage
* costs
* model breakdown

---

## 1️⃣4️⃣ GitHub Automation

Install GitHub agent:

```bash
opencode github install
```

👉 Sets up GitHub Actions automation

---

## 1️⃣5️⃣ Environment Variables

### Disable auto updates

```bash
export OPENCODE_DISABLE_AUTOUPDATE=true
```

---

### Custom config path

```bash
export OPENCODE_CONFIG=/path/to/config.json
```

---

### Secure server

```bash
export OPENCODE_SERVER_PASSWORD=yourpassword
```

---

## ⚡ 1️⃣6️⃣ Recommended Raspberry Pi Setup

Best practice setup:

* run `opencode serve` continuously
* use `opencode run --attach` for scripts
* use web UI for monitoring/debugging

---

## 🧠 1️⃣7️⃣ Advanced Architecture

Example setup:

```
Raspberry Pi
 ├── OpenCode serve (AI backend)
 ├── Custom agents
 ├── Python / automation scripts
 └── Web UI
```

---

### Example workflow

1. User uploads file
2. Script runs:

```bash
opencode run --attach http://localhost:4096 "Analyze this code"
```

3. OpenCode responds
4. Pipeline continues

---

## 🚀 1️⃣8️⃣ Advanced Use Cases

With this setup you can:

* build a local AI coding assistant
* orchestrate multiple agents
* automate refactoring
* create modular AI pipelines
* integrate with external systems (e.g. cloud APIs)

---

## 🔥 TL;DR

The 3 most important commands:

```bash
opencode run     # automation
opencode serve   # backend
opencode web     # interface
```

---

## ⭐ Support

If this guide helped you:

* ⭐ star the repository
* share it with others
* contribute improvements

---

If you want, next step we can design a **full multi-agent system on Raspberry Pi using OpenCode**, tailored to your current projects.
