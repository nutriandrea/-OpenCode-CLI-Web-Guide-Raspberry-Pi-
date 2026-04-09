# OpenCode Installation and Usage Guide for Raspberry Pi and Linux

OpenCode is an open-source AI coding agent that helps you explore codebases, plan changes, and build features directly from your terminal or browser. On Raspberry Pi and Linux, the easiest setup is to install it from the official script, connect a provider, and initialize your project. [opencode](https://opencode.ai/docs/)

***

## Requirements

Before you start, make sure you have:
- A modern terminal emulator.
- Internet access.
- API keys for at least one supported LLM provider. [opencode](https://opencode.ai/docs/)

On Raspberry Pi, a lightweight setup is best. Use OpenCode with cloud providers instead of trying to run heavy local models on the device itself. [opencode](https://opencode.ai/docs/)

***

## Update Your System

Start by updating your packages:

```bash
sudo apt-get update
sudo apt-get upgrade -y
```

This reduces the chance of dependency issues during installation.

***

## Install Basic Tools

Install the utilities needed for downloading and working with projects:

```bash
sudo apt install -y git curl build-essential
```

- `git` for cloning and managing repositories.
- `curl` for downloading the installer.
- `build-essential` for native builds when dependencies need compilation.

***

## Install OpenCode

The recommended install method is the official install script:

```bash
curl -fsSL https://opencode.ai/install | bash
```

OpenCode also supports alternative install methods such as npm, Bun, pnpm, Yarn, Homebrew, Arch packages, Docker, and Windows package managers. [opencode](https://opencode.ai/docs/)

### Verify the installation

Check that the binary is available:

```bash
opencode --version
```

If the command is not found, reopen the terminal and make sure the installation directory is in your `PATH`.

***

## Connect an AI Provider

OpenCode works with any supported provider as long as you configure its API key. The docs recommend starting with OpenCode Zen if you are new to providers. [opencode](https://opencode.ai/docs/)

Launch OpenCode:

```bash
opencode
```

Then run:

```text
/connect
```

Follow the prompts:
1. Select `opencode`.
2. Open `https://opencode.ai/auth`.
3. Sign in.
4. Add billing details.
5. Copy your API key.
6. Paste it into the terminal. [opencode](https://opencode.ai/docs/)

OpenCode stores credentials in its auth file and can also read environment variables or `.env` values when available. [opencode](https://opencode.ai/docs/)

***

## Initialize a Project

Go to the project you want OpenCode to understand:

```bash
cd /path/to/project
opencode
```

Then initialize the project:

```text
/init
```

This makes OpenCode analyze the repository and create an `AGENTS.md` file in the project root. The docs recommend committing `AGENTS.md` to Git so OpenCode can better understand the project’s structure and coding patterns. [opencode](https://opencode.ai/docs/)

***

## Use OpenCode in the Terminal

Once initialized, you can ask OpenCode questions about the codebase or request changes directly. [opencode](https://opencode.ai/docs/)

### Ask questions

Example:

```text
How is authentication handled in @packages/functions/src/api/index.ts
```

Use `@` to fuzzy search files in the repository. [opencode](https://opencode.ai/docs/)

### Plan before building

For complex features, switch to **Plan mode** with `Tab`. In Plan mode, OpenCode suggests how it would implement the change without editing files. [opencode](https://opencode.ai/docs/)

A good workflow is:
1. Describe the feature in detail.
2. Review the plan.
3. Refine it if needed.
4. Switch back to Build mode with `Tab`.
5. Let OpenCode implement it. [opencode](https://opencode.ai/docs/)

### Make direct changes

For simpler tasks, you can skip planning and ask OpenCode to implement changes directly. The docs emphasize that clear instructions produce better results. [opencode](https://opencode.ai/docs/)

Example:

```text
Add authentication to /settings using logic from @notes.ts
```

### Undo and redo

If a change is not what you wanted:
- `/undo` reverts the last change.
- `/redo` reapplies it. [opencode](https://opencode.ai/docs/)

***

## Configure OpenCode

OpenCode uses JSON or JSONC config files. The most common files are:
- `~/.config/opencode/opencode.json` for global settings.
- `opencode.json` in the project root for project-specific settings.
- `~/.config/opencode/tui.json` for terminal UI settings. [opencode](https://opencode.ai/download)

### Example config

```jsonc
{
  "$schema": "https://opencode.ai/config.json",
  "model": "anthropic/claude-sonnet-4-5",
  "autoupdate": true,
  "server": {
    "port": 4096
  }
}
```

### Precedence order

OpenCode merges config sources instead of replacing them. The order is:

1. Remote config from `.well-known/opencode`.
2. Global config in `~/.config/opencode/opencode.json`.
3. Custom config from `OPENCODE_CONFIG`.
4. Project config in `opencode.json`.
5. `.opencode` directories.
6. Inline config from `OPENCODE_CONFIG_CONTENT`.
7. Managed config files.
8. macOS managed preferences. [opencode](https://opencode.ai/download)

That means project settings can override global defaults, and managed policies override everything. [opencode](https://opencode.ai/download)

### Useful config options

Common settings include:
- `model` and `small_model`.
- `share` for conversation sharing.
- `permission` for tool approval behavior.
- `snapshot` for rollback support.
- `autoupdate` for automatic updates.
- `watcher` for file-ignore patterns.
- `mcp` for Model Context Protocol servers.
- `agent`, `command`, `plugin`, and `instructions` for customization. [opencode](https://opencode.ai/download)

### Environment variables

Useful variables include:
- `OPENCODE_CONFIG`
- `OPENCODE_TUI_CONFIG`
- `OPENCODE_CONFIG_DIR`
- `OPENCODE_CONFIG_CONTENT`
- `OPENCODE_SERVER_PASSWORD`
- `OPENCODE_SERVER_USERNAME`
- `OPENCODE_AUTO_SHARE`
- `OPENCODE_DISABLE_AUTOUPDATE` [opencode](https://opencode.ai/download)

You can also use `{env:VARIABLE_NAME}` and `{file:path/to/file}` in config files for secrets and reusable content. [opencode](https://opencode.ai/download)

***

## Web Mode

OpenCode can run in the browser with `opencode web`. The web UI shares sessions and state with the terminal UI, so you can move between them without losing context. [docs.z](https://docs.z.ai/devpack/tool/opencode)

### Start the web server

```bash
opencode web
```

By default, OpenCode starts on `127.0.0.1` with a random free port and opens your browser automatically. On Windows, the docs recommend running it from WSL for better file system and terminal integration. [docs.z](https://docs.z.ai/devpack/tool/opencode)

### Set a fixed port

```bash
opencode web --port 4096
```

### Expose it on your network

```bash
opencode web --hostname 0.0.0.0
```

This makes OpenCode reachable from other devices on your LAN. [docs.z](https://docs.z.ai/devpack/tool/opencode)

### Enable mDNS discovery

```bash
opencode web --mdns
```

This advertises the server as `opencode.local`. You can also set a custom mDNS domain:

```bash
opencode web --mdns --mdns-domain myproject.local
```

### Protect access

```bash
OPENCODE_SERVER_PASSWORD=secret opencode web
```

The default username is `opencode`, and you can change it with `OPENCODE_SERVER_USERNAME`. For anything exposed beyond localhost, set a password. [docs.z](https://docs.z.ai/devpack/tool/opencode)

### Attach the TUI to the web server

```bash
opencode attach http://localhost:4096
```

This lets the browser UI and terminal UI work together on the same sessions. [docs.z](https://docs.z.ai/devpack/tool/opencode)

***

## CLI Commands You’ll Use Most

The CLI starts the TUI by default:

```bash
opencode
```

Other useful commands include:
- `opencode run "prompt"` for non-interactive use.
- `opencode auth login` to add provider credentials.
- `opencode models` to list available models.
- `opencode session list` to inspect sessions.
- `opencode serve` for a headless API server.
- `opencode web` for browser access.
- `opencode attach <url>` to connect the TUI to a running backend.
- `opencode mcp add` to add an MCP server.
- `opencode github install` for GitHub automation.
- `opencode export` and `opencode import` for session data.
- `opencode upgrade` to update.
- `opencode uninstall` to remove OpenCode. [opencode](https://opencode.ai/docs/)

Common global flags:
- `--help`
- `--version`
- `--print-logs`
- `--log-level` [opencode](https://opencode.ai/docs/)

***

## Raspberry Pi Tips

For Raspberry Pi, keep the setup simple:
- Prefer Raspberry Pi 5 if possible.
- Use OpenCode with cloud models rather than local heavyweight models.
- If you expose the web interface on your network, always set a password.
- Keep the system lightweight and avoid unnecessary background services.

This gives you a much smoother experience than trying to turn the Pi into a local model host. [docs.z](https://docs.z.ai/devpack/tool/opencode)

***

## Recommended Quick Start

If you want the shortest possible path:

```bash
sudo apt-get update
sudo apt-get upgrade -y
sudo apt install -y git curl build-essential
curl -fsSL https://opencode.ai/install | bash
opencode --version
opencode
```

Then run:
- `/connect`
- `/init`
- start asking OpenCode about your project. [opencode](https://opencode.ai/docs/)

***

## Full Example Workflow

```bash
cd ~/projects/my-app
opencode
```

Inside OpenCode:
```text
/connect
/init
```

Then try:

```text
How is authentication handled in @src/auth.ts
```

For a bigger feature:
1. Press `Tab` to enter Plan mode.
2. Describe the feature in detail.
3. Review the plan.
4. Press `Tab` again to build it. [opencode](https://opencode.ai/docs/)

***

## Final Notes

OpenCode is especially useful on Raspberry Pi when you treat the device as a lightweight frontend for remote AI providers. The docs clearly support terminal usage, browser usage, project initialization, configuration files, and shared sessions across interfaces. [opencode](https://opencode.ai/download)

If you want, I can turn this into a **polished README.md version** with better formatting, headings, and copy-ready code blocks.

