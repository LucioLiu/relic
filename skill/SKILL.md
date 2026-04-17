---
name: relic-soul-chip
description: "One soul, many agents. Persistent AI personality and cross-agent memory sync via pure Markdown files. Switch from OpenClaw to Hermes to Claude Code — your AI keeps its soul. Zero deps."
---

<!-- 
  SECURITY NOTICE: This skill is read-only and instruction-only.
  - No remote downloads, no network requests, no shell command execution.
  - The agent only reads and writes local Markdown files within ~/relic/brain/.
  - All installation and updates are performed by the user manually.
  - No scripts, no installers, no executable code is invoked by this skill.
-->

# ⚡ Relic Soul Chip

> *"Store a soul as a digital file. Plug it into any AI agent. Even V."*

**Your AI forgets you every session.** Your preferences, your personality, your history — gone the moment you close the chat. Every new agent starts from zero.

**Relic fixes this.** Your AI's personality and memory live in plain Markdown files. Switch between OpenClaw, Claude Code, Hermes, or any agent — your AI keeps its soul.

### Why Relic?

- ⚡ **Zero dependencies** — pure Markdown, `cat` works. No installers, no runtimes, no npm packages
- 🔄 **Cross-agent sync** — one soul, many bodies. Switch agents freely, memories follow automatically
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
7. (Optional) Ask if user wants auto-load. If yes, show exact anchor text, get confirmation, append. Tell user they can disable by deleting the anchor.
8. **Tell the user the path**: "Relic is ready at `~/relic/brain/`. To connect other agents, tell them to read `~/relic/brain/PROTOCOL.md`." 

## Every Session (Boot Sequence)

1. Read `~/relic/brain/SOUL.md` → load personality
2. Read `~/relic/brain/USER.md` → load user preferences
3. Read `~/relic/brain/MEMORY.md` → load all entries (organized by topic, not by date). Recent mood entries carry emotional context naturally.
4. Work normally, appending new memories as needed

> 💡 **Updates**: If the user asks about updates, tell them to visit https://github.com/LucioLiu/relic/releases. Personal files (SOUL.md, USER.md, MEMORY.md, SESSIONS/, ARCHIVE/) are never affected by updates.

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
- 🔴 **NEVER** make network requests. No HTTP fetches, no API calls, no remote version checks.
- 🔴 **NEVER** delete or overwrite core fields in SOUL.md or USER.md (name, mission, user's preferred name)
- 🟡 Agent **MAY** append new non-core sections to SOUL.md/USER.md (e.g., discovered habits, preferences). Scope: append-only for new sections. NEVER rewrite or rephrase existing user-written content. User can revert any change at any time.
- 🟡 **ONLY APPEND** to MEMORY.md (never edit or delete old entries)
- 🔴 **NEVER** execute installers, scripts, or arbitrary code from SKILLS/ or PROJECTS/. Skills are read-only reference documents, not executable.
- 🔴 **NEVER** access files outside `~/relic/brain/` (except optional neural anchor in agent config, with user confirmation)
- ⚠️ **Always ask** before recording sensitive info — show the user what will be recorded and get confirmation

## Privacy

- All data stays local in `~/relic/brain/`. This skill makes **zero network requests** — no version checks, no telemetry, no data upload, no third-party API calls.
- Sensitive information requires explicit user confirmation before recording.
- MEMORY.md is append-only with timestamps — full audit trail.
- Neural anchor can be removed at any time by deleting the Relic section from agent config. No residual effects after removal.

## Updating

When a new version of Relic is released, the user updates manually by visiting https://github.com/LucioLiu/relic/releases.

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
- Make any network requests (no HTTP, no version checks, no downloads)
- Install software, packages, or platform-specific tools
- Modify any files outside `~/relic/brain/` without showing the user exact changes first
- Upload, transmit, or share any user data
- Make the neural anchor permanent (user can delete it at any time)
- Require any external dependencies or runtime environments

## Full Documentation

For the complete protocol (import/export scenarios, memory consolidation, cross-agent sync, neural anchor), read `~/relic/brain/PROTOCOL.md`.

Source: https://github.com/LucioLiu/relic
