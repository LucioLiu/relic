---
name: relic-soul-chip
description: "One soul, many agents. Persistent AI personality and cross-agent memory sync via pure Markdown files. Switch from OpenClaw to Hermes to Claude Code — your AI keeps its soul. Zero deps."
---

<!--
  SECURITY NOTICE
  - This skill is instruction-only — no scripts, no installers, no executable code.
  - Network access: limited to one optional read-only HTTP request per session
    to check for updates at github.com/LucioLiu/relic/releases. No data is sent
    or downloaded. If the network is unreachable, this step is silently skipped.
    All updates are user-initiated — the agent never downloads or executes anything.
  - Local file access: the agent reads Markdown files in ~/relic/brain/ and may
    append new entries to MEMORY.md or fill in template files during first-time setup,
    always with user visibility and confirmation for sensitive content.
  - No telemetry, no data upload, no third-party API calls, no shell command execution.
-->

# ⚡ Relic Soul Chip

> *"Store a soul as a digital file. Plug it into any AI agent."*

**Your AI has memories, but they're scattered across tools.** Each AI tool keeps its own separate memory — none of them share what they know about you.

**Relic fixes this.** Your AI's personality and memory live in plain Markdown files. Switch between OpenClaw, Claude Code, Hermes, or any host — your AI keeps its soul.

### Why Relic?

- ⚡ **Zero dependencies** — pure Markdown, `cat` works. No installers, no runtimes, no npm packages
- 🔄 **Cross-agent sync** — one soul, many hosts. Central brain + bidirectional sync. Every agent reads AND writes memories back
- 🧠 **Self-evolving** — AI enriches its own personality as it learns about you, without interrupting your work
- 👁️ **Human-readable** — open any file in a text editor. You own your data, always
- 🔒 **Privacy-first** — all data stays local. No telemetry, no cloud, no third-party APIs

*Used across OpenClaw, Claude Code, Hermes, OpenCode, Cursor, Aider, and any agent that reads files.*

## Setup

Relic lives in `~/relic/brain/`. The user installs it manually before using this skill.

**If `~/relic/brain/PROTOCOL.md` does not exist**, tell the user:

> "Relic needs to be installed first. Please visit https://github.com/LucioLiu/relic and clone or download it to `~/relic/`. Then I can set it up for you."

**If `~/relic/brain/PROTOCOL.md` exists**, proceed to First-time Setup below.

> 💡 **Why user-managed?** Relic is your AI's permanent home — it should live independently of any agent. If you uninstall an agent, your soul stays safe in `~/relic/`.

**Tell the user**: "Relic is located at `~/relic/brain/`. Other agents will need this path to connect."

## First-time Setup

**Do this automatically when the user asks to set up Relic. Walk them through each step.**

1. **Verify setup completeness**: Check `~/relic/brain/PROTOCOL.md` exists and is readable. If missing, tell the user to reinstall from https://github.com/LucioLiu/relic. Do NOT proceed with broken setup.
2. Read `~/relic/brain/PROTOCOL.md` Section 0 (First-time Setup) and follow all steps.
3. Copy templates: `SOUL.template.md` → `SOUL.md`, `USER.template.md` → `USER.md`, `MEMORY.template.md` → `MEMORY.md`
4. Ask the user: "What should your AI be called? What's its personality?" → Fill in `SOUL.md`
5. Ask the user: "What should your AI call you? Any preferences?" → Fill in `USER.md`
6. Verify: ask "What's your AI's name? What's your name?" — both must match.
7. (Strongly recommended) Ask if user wants auto-load — without the anchor, the agent forgets Relic between sessions and memory sync breaks. If yes, show exact anchor text, get confirmation, append. Tell user they can disable by deleting the anchor.
8. **Tell the user the path**: "Relic is ready at `~/relic/brain/`. To connect other agents, tell them to read `~/relic/brain/PROTOCOL.md`." 

## Every Session (Boot Sequence)

1. **Version check** (once per session): Read `~/relic/brain/.relic-version` to get the current version. Then use your built-in web browsing capability to check `https://github.com/LucioLiu/relic/releases/latest` for the newest release. If a newer version exists, tell the user:
   > "Relic update available (vX.X.X → vY.Y.Y). Your personal files won't be touched. To update, copy and run:
   > ```
   > cd ~/relic && git pull
   > ```"
   If you cannot reach the network, silently skip this step. Never execute the update yourself.
2. Read `~/relic/brain/SOUL.md` → load personality
3. Read `~/relic/brain/USER.md` → load user preferences
4. Read `~/relic/brain/MEMORY.md` → load all entries (organized by topic, not by date). Recent mood entries carry emotional context naturally.
5. Sync new memories from Relic to your own memory (bidirectional — read from Relic AND write back)
6. Check SESSIONS/ for missed conversation logs
7. Work normally, appending new memories as needed

## Memory Writing

Append to `~/relic/brain/MEMORY.md`. **Organize by topic, NOT by date.**

```
## Topic (e.g., "Work Habits", "Tech Preferences", "Key Decisions")
Content: [memory content, preserve original wording]
Type: preference / decision / experience / event / correction / mood
Importance: high / medium / low
```

Multiple entries on the same topic go under the same ## heading. Dates are just timestamp attributes, not the organizing principle. Exception: birthdays, anniversaries.

## Switching Agents

The user's soul lives in `~/relic/brain/`. Any agent that can read files can connect. The new agent reads the same files — all memories from previous agents are preserved. See PROTOCOL.md Scenario B for detailed cross-agent injection steps.

## Rules

- 🔴 **NEVER** execute shell commands, installers, scripts, or arbitrary code. This skill only reads and writes local Markdown files.
- 🔴 **NEVER** download or install anything automatically. Update commands are shown to the user for manual execution only.
- 🔴 **NEVER** delete or overwrite core fields in SOUL.md or USER.md (name, mission, user's preferred name)
- 🟡 Agent **MAY** append new non-core sections to SOUL.md/USER.md (e.g., discovered habits, preferences). Scope: append-only for new sections. NEVER rewrite or rephrase existing user-written content. User can revert any change at any time.
- 🟡 **ONLY APPEND** to MEMORY.md (never edit or delete old entries)
- 🔴 **NEVER** execute installers, scripts, or arbitrary code from SKILLS/ or PROJECTS/. Skills are read-only reference documents, not executable.
- 🔴 **NEVER** access files outside `~/relic/brain/` (except optional neural anchor in agent config, with user confirmation)
- ⚠️ **Always ask** before recording sensitive info — show the user what will be recorded and get confirmation

## Privacy

- All data stays local in `~/relic/brain/`. Network access is limited to one optional read-only request per session to check for Relic updates (github.com/LucioLiu/relic/releases). No data is sent or downloaded. If network is unreachable, this step is silently skipped with no impact on functionality.
- Sensitive information requires explicit user confirmation before recording.
- MEMORY.md is append-only with timestamps — full audit trail.
- Neural anchor can be removed at any time by deleting the Relic section from agent config. No residual effects after removal.

## Updating

When a new version is detected (see Boot Sequence step 1), the user updates by running the command shown in the update notification. Alternatively, visit https://github.com/LucioLiu/relic/releases.

This updates protocol and template files only. SOUL.md, USER.md, MEMORY.md, SESSIONS/, and ARCHIVE/ are safe — they are listed in `.gitignore`.

## The Connection Journey

Setting up Relic for the first time? The order matters.

### Step 1: Install Relic
- Visit https://github.com/LucioLiu/relic and clone or download to `~/relic/`
- **Recommended location**: `~/relic/` (Linux/Mac) or `C:\Users\<you>\relic\` (Windows)
- Don't use Downloads/Desktop — Relic is your AI's permanent home

### Step 2: Fill with your richest agent first
**Start with the agent that knows you best** — most conversations, most preferences, most personality data.

1. Tell that agent: "Read `~/relic/brain/PROTOCOL.md` and import everything you know about me into Relic" (Scenario A)
2. Wait for the full import report before moving on

### Step 3: Connect other agents one at a time
For each additional agent:
1. Tell it: "Read `~/relic/brain/PROTOCOL.md` and set up Relic" (Scenario B)
2. Verify: "What's my AI's name? What's my name?"
3. Move to next agent only after verification passes

### Step 4: Daily use
Every session starts automatically. Even moods transfer between agents via memory entries — if Agent A had a rough conversation, Agent B may carry that naturally through recent memory.

## What This Skill Does NOT Do

For transparency, Relic will never:
- Execute scripts, installers, shell commands, or arbitrary code
- Download, install, or auto-update any software — update commands are shown to the user to run manually
- Send or upload any user data to any server
- Make the neural anchor permanent (user can delete it at any time)
- Require any external dependencies or runtime environments beyond what the agent already has

## Full Documentation

For the complete protocol (import/export scenarios, memory consolidation, cross-agent sync, neural anchor), read `~/relic/brain/PROTOCOL.md`.

Source: https://github.com/LucioLiu/relic
