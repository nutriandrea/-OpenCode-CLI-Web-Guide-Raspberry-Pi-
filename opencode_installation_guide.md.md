# 🧠 OpenCode Installation & Usage Guide (Raspberry Pi / Linux)

This guide walks you through installing and using OpenCode step-by-step on Raspberry Pi or Linux.

---

## 1️⃣ Update Your System

Before installing new software, update your system packages.

```bash
sudo apt-get update
sudo apt-get upgrade
```

---

## 2️⃣ Install Essential Development Tools

These are required to download code and build dependencies.

```bash
sudo apt install -y git curl build-essential
```

---

## 3️⃣ Install Node.js (Required)

OpenCode requires Node.js.

```bash
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```

---

## 4️⃣ Verify Node.js Installation

```bash
node --version
npm --version
```

---

# 📦 Install OpenCode

## Recommended Method (Install Script)

```bash
curl -fsSL https://opencode.ai/install | bash
```

---

## Alternative Methods

### Using Node.js (npm)

```bash
npm install -g opencode-ai
```

---

### Using Homebrew (macOS / Linux)

```bash
brew install anomalyco/tap/opencode
```

👉 Recommended over `brew install opencode` because it’s more up to date.

---

### Arch Linux

```bash
sudo pacman -S opencode        # Stable
paru -S opencode-bin           # Latest (AUR)
```

---

### Windows (Recommended: WSL)

```bash
choco install opencode
```

or

```bash
scoop install opencode
```

or

```bash
npm install -g opencode-ai
```

---

### Docker

```bash
docker run -it --rm ghcr.io/anomalyco/opencode
```

---

# ⚙️ Configure OpenCode

OpenCode works with multiple LLM providers via API keys.

## Connect your provider

Inside OpenCode:

```
/connect
```

### Steps

1. Select **opencode (recommended)**
2. Open: [https://opencode.ai/auth](https://opencode.ai/auth)
3. Sign in
4. Add billing details
5. Copy your API key
6. Paste it into the terminal

👉 If you’re new, use **OpenCode Zen** (curated models)

---

# 🚀 Initialize a Project

Navigate to your project:

```bash
cd /path/to/project
opencode
```

Then run:

```
/init
```

### What happens

* OpenCode analyzes your codebase
* Creates an `AGENTS.md` file
* Learns your project structure

👉 Important: commit `AGENTS.md` to Git

---

# 💻 Usage

You can now use OpenCode to interact with your codebase.

---

## Ask Questions

```
How is authentication handled in @packages/functions/src/api/index.ts
```

👉 Tip: use `@` to search files

---

## Add Features (Recommended Workflow)

### 1. Switch to Plan Mode

Press:

```
TAB
```

---

### 2. Describe the feature

```
When a user deletes a note, flag it as deleted in the database.
Then create a screen showing recently deleted notes.
Allow restore or permanent deletion.
```

---

### 3. Iterate on the plan

```
Use this UI as a reference [Image]
```

👉 You can drag & drop images into the terminal

---

### 4. Build the feature

Press again:

```
TAB
```

Then:

```
Go ahead and implement the changes
```

---

## Direct Changes

```
Add authentication to /settings using logic from @notes.ts
```

---

## Undo / Redo

```
/undo
/redo
```

---

## Share Conversations

```
/share
```

👉 Generates a shareable link

---

# ⚡ Tips

* Treat OpenCode like a junior developer
* Give clear instructions and context
* Use Plan mode for complex features
* Iterate before building

---

# 🧠 What You Can Do With OpenCode

* Generate code
* Refactor projects
* Understand large codebases
* Build features automatically
* Create AI-driven dev workflows

---

# ⚡ Raspberry Pi Recommendations

* Prefer Raspberry Pi 5
* Avoid heavy local models
* Use API-based LLMs
* Keep system lightweight

---

# ⭐ Support

If you found this guide helpful:

* ⭐ Star the repository
* Share it with others
* Contribute improvements

