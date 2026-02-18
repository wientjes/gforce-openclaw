# OpenClaw (Local State)

This folder is the local state directory for OpenClaw. It includes your gateway configuration, workspace, agent sessions, and per-channel credentials.

OpenClaw is a personal AI assistant you run on your own devices. It answers you on the channels you already use (WhatsApp, Telegram, Slack, Discord, Google Chat, Signal, iMessage, Microsoft Teams, WebChat), plus extension channels like BlueBubbles, Matrix, Zalo, and Zalo Personal. It can speak and listen on macOS/iOS/Android and can render a live Canvas you control. The Gateway is the control plane — the product is the assistant. If you want a personal, single-user assistant that feels local, fast, and always-on, this is it.

## Links

- Website: https://openclaw.ai/
- Docs: https://docs.openclaw.ai/
- Vision: https://github.com/openclaw/openclaw/blob/main/VISION.md
- DeepWiki: https://deepwiki.com/openclaw/openclaw
- Getting Started: https://docs.openclaw.ai/start/getting-started
- Updating: https://docs.openclaw.ai/install/updating
- Showcase: https://docs.openclaw.ai/start/showcase
- FAQ: https://docs.openclaw.ai/help/faq
- Wizard: https://docs.openclaw.ai/start/wizard
- Nix: https://github.com/openclaw/nix-openclaw
- Docker: https://docs.openclaw.ai/install/docker
- Discord: https://discord.gg/clawd

(These are copied from the upstream OpenClaw README for convenience.)

## Preferred Setup (Recommended)

The recommended path is the onboarding wizard:

```bash
openclaw onboard --install-daemon
```

The wizard configures auth, gateway settings, workspace defaults, and optional channels, and works on macOS, Linux, and Windows (via WSL2).

## Quick Start (TL;DR)

Runtime: Node >= 22.

```bash
npm install -g openclaw@latest
# or: pnpm add -g openclaw@latest

openclaw onboard --install-daemon
openclaw gateway --port 18789 --verbose

# Send a message
openclaw message send --to +1234567890 --message "Hello from OpenClaw"

# Talk to the assistant
openclaw agent --message "Ship checklist" --thinking high
```

The full beginner guide is in Getting Started.

## What’s In This Directory

This directory is your OpenClaw state home (`~/.openclaw`). The core config lives at `~/.openclaw/openclaw.json`.

- `openclaw.json`: Main gateway configuration (channels, gateway settings, model/auth profiles, skills, etc.). Contains secrets.
- `openclaw.json.bak*`: Automatic backups of the config.
- `agents/`: Agent runtime state.
  - `agents/main/agent/`: Per-agent auth and profile data.
  - `agents/main/sessions/`: Session transcripts and probes (JSONL).
- `workspace/`: Agent workspace and bootstrap documents.
  - `AGENTS.md`, `USER.md`, `SOUL.md`, `TOOLS.md`, `MEMORY.md`, `IDENTITY.md`, `HEARTBEAT.md`: Local instructions, preferences, and memory used by the agent.
  - `old/`: Archived/previous versions of workspace docs.
- `credentials/`: Channel-specific allowlists/pairing data. Sensitive.
- `devices/`: Paired/pending device records for nodes/clients. Sensitive.
- `identity/`: Device identity keys and auth material. Sensitive.
- `cron/`: Scheduled jobs for the agent (`jobs.json`).
- `telegram/`: Telegram update offsets and channel bookkeeping.
- `logs/`: Local logs and audits (for example, config audits).
- `canvas/`: Canvas artifacts (local UI assets such as `index.html`).
- `completions/`: Shell completions for the `openclaw` CLI.
- `update-check.json`: Update-check metadata for the CLI.

## Security Notes

This directory contains secrets (tokens, keys, pairing data). Don’t commit it to git or share it. If you need to back up, encrypt it and keep it private.
