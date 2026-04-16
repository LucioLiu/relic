---
name: relic
description: "Relic Soul Chip — Give your AI agent a persistent personality and memory across sessions. Pure Markdown, human-readable. Switch agents, keep the soul."
version: "0.1.1"
author: LucioLiu
license: GPL-3.0
homepage: "https://github.com/LucioLiu/relic"
compatibility:
  - "File-reading agent (any platform)"
  - "Requires: git (for clone install only), filesystem read/write in designated Relic directory"
allowed-tools:
  - "Read"
  - "Write"
  - "Bash(git clone:*)"
metadata:
  clawhub:
    tags: [personality, memory, cross-agent, soul, identity, markdown, ai-personality, agent-memory, cyberpunk]
    requires:
      binaries: ["git"]
      env: []
      filesystem:
        read:
          - "~/relic/brain/SOUL.md"
          - "~/relic/brain/USER.md"
          - "~/relic/brain/MEMORY.md"
          - "~/relic/brain/PROTOCOL.md"
          - "~/relic/brain/SESSIONS/"
          - "~/relic/brain/SKILLS/"
          - "~/relic/brain/PROJECTS/"
        write:
          - "~/relic/brain/MEMORY.md"
          - "~/relic/brain/SESSIONS/"
          - "~/relic/brain/ARCHIVE/"
          - "~/relic/brain/INBOX/"
        modify_agent_config: true
        modify_agent_config_description: "Neural anchor: appends a reference block to agent's config file (AGENTS.md/CLAUDE.md/etc) so the agent auto-loads Relic on startup. Only appends, never deletes existing content. User confirmation required before modification."

---

# ⚡ Relic Soul Chip

> *"Store a soul as a digital file. Plug it into any AI agent. Even V."*
> — Inspired by Cyberpunk 2077's Relic Biochip

## What This Skill Does

Relic gives your AI agent a **persistent soul** — personality, memories, and skills stored in plain Markdown files. No code, no dependencies beyond `git`.

When your agent reads this skill, it will learn how to:
- **Set up a soul** (`SOUL.md`) defining who the AI is — name, personality, core mission
- **Remember the user** (`USER.md`) — preferences, habits, communication style
- **Persist memories** (`MEMORY.md`) — events, decisions, lessons learned
- **Sync across agents** — the same soul works in OpenClaw, Hermes, Claude Code, Cursor, or any future agent

**Switch agents. Keep the soul.**

## When to Use

- User says "set up Relic" or "I want my AI to remember me"
- User wants persistent personality across sessions
- User switches between multiple AI agents and wants continuity
- User mentions personality, memory, identity for their AI

## Requirements

| Requirement | Purpose | Optional |
|-------------|---------|----------|
| `git` | Clone the Relic repo during install | Yes (can manually download instead) |
| Filesystem read | Read SOUL.md, USER.md, MEMORY.md | No |
| Filesystem write | Append to MEMORY.md, write session logs | No |
| Agent config modify | Plant "neural anchor" for auto-loading | Yes (user can skip this step) |

All files are confined to `~/relic/brain/` (or user-specified directory). This skill does **not** access files outside the Relic directory, except for the one-time agent config modification.

## Steps

### 1. Check if Relic already exists

Look for a `relic/brain/` directory (or wherever the user points you). If `PROTOCOL.md` exists there, Relic is already set up — just follow the boot sequence in Section 2 of PROTOCOL.md.

If no Relic exists, proceed to setup.

### 2. Install Relic

```bash
# Option A: Clone from GitHub (requires git)
git clone https://github.com/LucioLiu/relic.git ~/relic

# Option B: Manual download (no git required)
# Download and extract https://github.com/LucioLiu/relic/archive/refs/heads/main.zip
# to ~/relic/
```

The brain/ folder needs: `PROTOCOL.md`, `SOUL.template.md`, `USER.template.md`, `MEMORY.template.md`

### 3. First-time Setup

Read `relic/brain/PROTOCOL.md` Section 0 ("First-time Setup") and follow it exactly:

1. Copy templates → active files (`SOUL.md`, `USER.md`, `MEMORY.md`)
2. Help user fill in SOUL.md (at minimum: AI name + core mission)
3. Help user fill in USER.md (at minimum: preferred name + communication preferences)
4. **Neural anchor (optional, requires user confirmation):** Ask the user if they want to add a startup reference to their agent config file. If yes, append a small reference block pointing to `~/relic/brain/` to their config (AGENTS.md / CLAUDE.md / etc). Show the user exactly what will be appended before making any changes. Do not modify or delete any existing config content.
5. Verify: ask "What's my AI's name? What's my name?" — both must be correct

### 4. Every Session After Setup (Boot Sequence)

At the start of every session, execute the boot sequence from PROTOCOL.md Section 2:

1. Read SOUL.md → load your personality
2. Read USER.md → load user preferences
3. Read MEMORY.md → load recent events (last 30 entries)
4. Sync new memories from Relic to your own memory (if supported)
5. Work normally, appending new memories as needed

### 5. Memory Management

- **Write memories**: Append to `MEMORY.md` with format:
  ```
  ## YYYY-MM-DD HH:MM [AgentName]
  Content: [what happened]
  Type: preference / decision / experience / event / correction
  Importance: high / medium / low
  ```
- **Consolidate**: When MEMORY.md exceeds 200 lines, offer to consolidate (archive old entries, keep summaries)
- **Never delete**: Original memories move to ARCHIVE/, never deleted

### 6. Switching Agents

When the user switches to a different agent:
- The new agent reads the same `relic/brain/` directory
- Follow PROTOCOL.md Scenario B (Inject) — the new agent inherits the soul
- All memories from previous agents are preserved

## Security & Privacy

This skill is designed with user privacy as a priority:

- **Scoped access**: All read/write operations are confined to `~/relic/brain/` (or user-specified directory). No access to files outside this directory, except for the optional one-time agent config modification.
- **SOUL.md and USER.md are read-only**: The agent must never modify these files after initial setup. Only the user can edit them directly.
- **Sensitive information protection**: Before recording ANY user data (names, emails, phone numbers, addresses, API keys, passwords), the agent MUST:
  1. Show the user exactly what will be recorded
  2. Get explicit confirmation
  3. Allow the user to redact or skip specific items
  If the user declines, do NOT record that information.
- **Session logs**: SESSIONS/ contains conversation logs. These are for the user's reference only and should never be transmitted, uploaded, or shared.
- **Neural anchor transparency**: When modifying agent config, show the user the exact text that will be appended. The anchor is a reference block only — it does not grant elevated permissions.
- **No network access required after install**: All operations are local filesystem reads and writes. No API calls, no telemetry, no data transmission.
- **Audit trail**: All modifications to MEMORY.md are append-only with timestamps. Users can review the full history at any time.

## Important Rules

- 🔴 **NEVER** modify SOUL.md or USER.md (read-only after setup)
- 🟡 **ONLY APPEND** to MEMORY.md (never edit or delete old entries)
- 🔴 **NEVER** delete SESSIONS/ or ARCHIVE/
- 🔴 **NEVER** access files outside `~/relic/brain/` (except the optional config modification)
- 🔴 **NEVER** transmit, upload, or share conversation logs or user data
- ⚠️ **ALWAYS ask** before recording sensitive info — show what will be recorded, get confirmation
- ⚠️ **ALWAYS ask** before modifying agent config — show the exact text, get confirmation

## File Access Summary

| File | Read | Write | Purpose |
|------|------|-------|---------|
| `SOUL.md` | ✅ | ❌ (setup only) | AI personality definition |
| `USER.md` | ✅ | ❌ (setup only) | User preferences |
| `MEMORY.md` | ✅ | ✅ (append only) | Event log, memories |
| `PROTOCOL.md` | ✅ | ❌ | Protocol instructions |
| `SESSIONS/` | ✅ | ✅ (new files) | Conversation logs |
| `ARCHIVE/` | ✅ | ✅ (archive) | Archived memories |
| `INBOX/` | ✅ | ✅ (import) | Temporary import staging |
| `SKILLS/` | ✅ | ❌ | Skill definitions |
| `PROJECTS/` | ✅ | ✅ (new files) | Project tracking |
| Agent config | ❌ | ✅ (append only, one-time, user-confirmed) | Neural anchor for auto-loading |

## Configuration

Default path: `~/relic/brain/` — user can customize during setup.

Full protocol documentation: `relic/brain/PROTOCOL.md`
Source code: https://github.com/LucioLiu/relic
