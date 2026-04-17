---
name: relic-soul-chip
description: "Relic Soul Chip — Give your AI agent a persistent personality and memory across sessions. Pure Markdown, human-readable. Switch agents, keep the soul."
version: "1.0.0"
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
  hermes:
    tags: [Personality, Memory, Cross-Agent, Identity, AI-Soul, Agent-Memory, Markdown, User-Preferences]
    related_skills: []
    requires_toolsets: []
    requires_binaries: ["git"]
    filesystem_scope:
      read: ["~/relic/brain/"]
      write: ["~/relic/brain/MEMORY.md", "~/relic/brain/SESSIONS/", "~/relic/brain/ARCHIVE/", "~/relic/brain/SOUL.md", "~/relic/brain/USER.md"]

---

# ⚡ Relic Soul Chip

Give your AI agent a persistent personality and memory that survives sessions and follows the user across different agents. Pure Markdown. Human-readable.

**Your AI forgets you every session.** Preferences, personality, history — gone. **Relic fixes this.** Your AI's soul lives in plain Markdown files. Switch agents, keep the soul.

### Why Relic?

- ⚡ **Zero dependencies** — pure Markdown, `cat` works
- 🔄 **Cross-agent sync** — one soul, many bodies
- 🧠 **Self-evolving** — AI enriches its personality as it learns
- 👁️ **Human-readable** — open any file in a text editor
- 🔒 **Privacy-first** — all data stays local

## Requirements

| Requirement | Purpose | Optional |
|-------------|---------|----------|
| `git` | Clone/update the Relic repo | Yes (can manually download) |
| HTTP request | Version check (raw.githubusercontent.com, once per session) | Yes (skip if offline) |
| Filesystem read | Read SOUL.md, USER.md, MEMORY.md | No |
| Filesystem write | Append to MEMORY.md, write session logs | No |
| Agent config modify | Plant "neural anchor" for auto-loading | Yes (user can skip) |

All file operations are confined to `~/relic/brain/` (or user-specified directory). The only access outside this directory is the optional one-time neural anchor in agent config. Network access is limited to version check and optional git pull — no data upload, no third-party services.

## Steps

### First-time Setup

1. Install Relic: `git clone https://github.com/LucioLiu/relic.git ~/relic`
2. Read the full protocol: `~/relic/brain/PROTOCOL.md`
3. Copy templates to active files (SOUL.md, USER.md, MEMORY.md)
4. Help user fill in SOUL.md (AI name + core mission) and USER.md (user preferences)
5. **Neural anchor (optional):** Ask user if they want to add a startup reference to their agent config. If yes, show exactly what will be appended, get confirmation, then append. Do not modify existing config content.
6. Verify: ask "What's my AI's name? What's my name?" — both must be correct

### Every Session (Boot Sequence)

1. **Version check** (once per session): Read `~/relic/brain/.relic-version`, compare with `https://raw.githubusercontent.com/LucioLiu/relic/main/brain/.relic-version`. If newer version exists, ask user if they want to update. If user agrees, run `cd ~/relic && git pull`. Never force updates.
2. Read SOUL.md → load personality
3. Read USER.md → load user preferences
4. Read MEMORY.md → load all entries, organized by topic (not by date)
5. Sync new memories from Relic to your own memory (if supported)
6. Work normally, appending new memories

### Memory Writing

```
## Topic (e.g., "Work Habits", "Tech Preferences")
Content: [memory content, preserve original wording]
Type: preference / decision / experience / event / correction / mood
Importance: high / medium / low

Organize by TOPIC, not by date. Dates are just timestamps, not the structure.
```

### Switching to Another Agent

The user's soul lives in `~/relic/brain/`. The new agent reads the same files and follows PROTOCOL.md Scenario B (Inject).

## Security & Privacy

- **Scoped access**: All read/write confined to `~/relic/brain/`. No outside access.
- **SOUL.md/USER.md**: Core fields (name, mission, user preferred name) are protected — never deleted or overwritten. Agent may append new non-core sections (e.g., discovered habits, preferences) as background self-evolution. Agent NEVER rewrites or rephrases existing user-written content. User can revert any change at any time.
- **Sensitive data**: MUST show user what will be recorded and get explicit confirmation before recording names, emails, phone numbers, addresses, API keys, passwords. Allow user to redact or skip.
- **Limited network access**: Version check via HTTP (raw.githubusercontent.com) once per session. Optional git pull for updates. No telemetry, no data upload, no API calls to third parties.
- **Neural anchor transparency**: Show user exact text before appending to agent config. User can remove the anchor at any time by deleting the Relic section — no residual effects.
- **Append-only audit trail**: MEMORY.md entries are timestamped and never deleted.

## Rules

- 🔴 NEVER delete or overwrite core fields in SOUL.md or USER.md (name, mission, user's preferred name)
- 🟡 Agent MAY append new non-core sections to SOUL.md/USER.md (discovered habits, preferences). NEVER rewrite existing user-written content. User can revert any change.
- 🟡 ONLY APPEND to MEMORY.md
- 🔴 NEVER execute installers, scripts, or arbitrary code from SKILLS/ or PROJECTS/. Skills are read-only reference documents, not executable.
- 🔴 NEVER delete SESSIONS/ or ARCHIVE/
- 🔴 NEVER access files outside ~/relic/brain/ (except optional config modification)
- 🔴 NEVER transmit, upload, or share user data
- ⚠️ ALWAYS ask before recording sensitive info — show, confirm, allow redact
- ⚠️ ALWAYS ask before modifying agent config — show exact text, get confirmation

## The Connection Journey

When setting up Relic for the first time, the order matters:

### Step 1: Choose a home for Relic
Pick a stable, easy-to-remember location:
- **Recommended**: `~/relic/` (Linux/Mac) or `C:\Users\<you>\relic\` (Windows)
- Avoid Downloads, Desktop, or temp folders — Relic is permanent
- If installing via an agent skill (e.g., OpenClaw), the agent should suggest a location and confirm with you

### Step 2: Fill Relic with your richest agent first
Your agents have different amounts of memory about you. **Start with the one that knows you best** — the one with the most conversations, preferences, and personality data.

1. Tell that agent: "Read `~/relic/brain/PROTOCOL.md` and import everything you know about me into Relic"
2. The agent will execute Scenario A (Full Import) — memories, skills, conversations, projects
3. Wait for it to finish completely and show you the import report

### Step 3: Connect your other agents, one at a time
For each additional agent (in any order):
1. Tell the agent: "Read `~/relic/brain/PROTOCOL.md` and set up Relic"
2. The agent will execute Scenario B (Inject) — read the soul, sync memories, inject personality
3. Verify: ask "What's my AI's name? What's my name?" — both must be correct
4. Only move to the next agent after verification passes

### Step 4: Daily use
After setup, every session starts automatically. No extra steps needed.

> 💡 **Tip**: If you have a conversation with Agent A that changes something important (new preference, big decision), Agent B will naturally pick it up next session via Relic MEMORY.md sync. Even moods transfer — if Agent A had a frustrating conversation, Agent B may carry that context naturally through memory entries.

## What This Skill Does NOT Do

For transparency, Relic will never:
- Execute scripts, installers, or arbitrary code
- Run update.sh automatically (user must opt in manually)
- Install software or platform-specific tools from SKILLS/
- Modify any files outside ~/relic/brain/ without showing exact changes first
- Upload, transmit, or share any user data
- Make the neural anchor permanent (user can remove it at any time)

## Full Documentation

Read `~/relic/brain/PROTOCOL.md` for the complete protocol including:
- Three import scenarios (empty → full, full → empty, both have data)
- Memory consolidation when files get large
- Bidirectional sync between Relic and agent memories
- Session recording guidelines

Source: https://github.com/LucioLiu/relic
