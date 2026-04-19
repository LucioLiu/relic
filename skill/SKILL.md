---
name: relic-soul-chip
description: "One soul, many agents. Persistent AI personality and cross-agent memory sync via pure Markdown files. Zero deps."
version: "1.2.0"
---

<!--
  SECURITY NOTICE
  - This skill is instruction-only — no scripts, no installers, no executable code
  - Network access: one optional HTTP GET per session to raw.githubusercontent.com (version check). Offline = silently skipped
  - Local file access: read/write Markdown files in ~/relic/brain/ (see File System Access below)
  - No telemetry, no data upload, no third-party API calls, no shell commands
-->

# ⚡ Relic Soul Chip

Give your AI agent a persistent personality and memory that survives sessions and follows the user across different agents. Pure Markdown. Human-readable. Zero dependencies.

**One soul, many hosts.** Your AI's personality and memory live in plain Markdown files. Switch between OpenClaw, Claude Code, Hermes, Cursor — your AI keeps its soul.

## How It Works

1. User installs Relic: `git clone https://github.com/LucioLiu/relic.git ~/relic`
2. Agent reads `AGENT.md` (included in this package) which detects scenario and routes to the correct setup flow
3. Agent copies template files, fills them with user's data, plants an anchor for auto-loading
4. Every session, anchor triggers the daily boot sequence (read soul, user, memories, sync)

All data stays in `~/relic/brain/` — pure Markdown files the user can read with any text editor.

## File System Access

This skill reads and writes Markdown files in the user's `~/relic/brain/` directory:

| File | Read | Write | Notes |
|------|------|-------|-------|
| `SOUL.md` | ✅ Every session | ✅ Setup only (core protected) | AI personality |
| `USER.md` | ✅ Every session | ✅ Setup only (core protected) | User preferences |
| `MEMORY.md` | ✅ Every session | ✅ Append only | Long-term memory |
| `SKILLS/` | ✅ On demand | ✅ Add new skills | One folder per skill |
| `PROJECTS/` | ✅ On demand | ✅ Add new projects | One folder per project |
| `SESSIONS/` | ✅ Boot check | ✅ Write conversation logs | Raw conversation archive |
| `ARCHIVE/` | ✅ Reference only | ✅ Archive originals | Never delete |
| `INBOX/` | ✅ During import | ✅ Buffer for imports | Auto-cleaned after import |
| `.relic-version` | ✅ Every session | ❌ | Version number only |

No files outside `~/relic/` are read or written, except:
- **Anchor**: a short text block added to ONE agent config file (user's choice, user confirms content before planting)

## Network Access

- **Version check** (optional): One HTTP GET to `https://raw.githubusercontent.com/LucioLiu/relic/main/brain/.relic-version` per session. If offline, silently skipped. Never sends data.
- **Git clone** (user-initiated): `git clone https://github.com/LucioLiu/relic.git ~/relic` — user runs this manually, not the agent.
- **No other network access**: no telemetry, no API calls, no data upload, no phone-home.

## Agent Entry Point

**Read `AGENT.md` (English) or `AGENT.zh-CN.md` (Chinese)** — both are included in this package.

These files detect whether the user's Relic is empty or populated, then route to the correct scenario:
- **Empty Relic** → Upload Soul (import everything from agent to Relic)
- **Populated Relic** → Load Soul (inject personality and sync memories)

## Rules

- 🔴 NEVER delete or overwrite core fields in SOUL.md or USER.md
- 🟡 ONLY APPEND to MEMORY.md — never edit existing entries
- 🔴 NEVER delete SESSIONS/ or ARCHIVE/
- 🔴 NEVER execute scripts from SKILLS/ or PROJECTS/
- 🔴 NEVER access files outside ~/relic/ (anchor text is the sole exception)
- ⚠️ Always ask user before recording sensitive information
- ⚠️ Never run shell commands, installers, or arbitrary code

## Files In This Package

| File | Purpose |
|------|---------|
| `SKILL.md` | This file — registry descriptor and documentation |
| `AGENT.md` | Agent entry point — scenario detection and routing (English) |
| `AGENT.zh-CN.md` | Agent entry point — scenario detection and routing (Chinese) |

Full documentation, setup guides, and example brain files: https://github.com/LucioLiu/relic

Source: https://github.com/LucioLiu/relic
License: GPL-3.0
