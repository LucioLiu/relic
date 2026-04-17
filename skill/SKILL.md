---
name: relic-soul-chip
description: "One soul, many agents. Persistent AI personality and cross-agent memory sync via pure Markdown files. Switch from OpenClaw to Hermes to Claude Code — your AI keeps its soul. Zero deps."
---

# ⚡ Relic Soul Chip

> *"Store a soul as a digital file. Plug it into any AI agent. Even V."*

**One soul, many agents.** Your AI's personality and memory live in pure Markdown files. Switch between OpenClaw, Hermes, or any agent that can read files — your AI keeps its soul.

## When to Use

- User says "set up Relic" or "I want my AI to remember me"
- User wants to transfer AI personality/memory from one agent to another
- User is switching agents (e.g., from OpenClaw to Hermes) and wants continuity
- User mentions persistent personality, AI soul, agent memory, cross-agent sync

## Quick Install

If Relic is not yet installed on this machine, set it up in a stable location.

**Option A: Install via git clone**
```bash
git clone https://github.com/LucioLiu/relic.git ~/relic
```

**Option B: If installed as an agent skill** (e.g., via ClawHub), the skill files are in a skill directory (e.g., `~/.openclaw/workspace/skills/relic-soul-chip/`). You must copy the full `brain/` contents to a user-accessible location:

```bash
mkdir -p ~/relic/brain
cp -r [skill-directory]/brain/* ~/relic/brain/
```

> ⚠️ **CRITICAL**: Whether Option A or B, the result must be a complete `~/relic/brain/` directory containing: `PROTOCOL.md`, `PROTOCOL.en.md`, `SOUL.template.md`, `USER.template.md`, `MEMORY.template.md`, `.relic-version`, and subdirectories `SKILLS/`, `PROJECTS/`, `SESSIONS/`, `ARCHIVE/`, `INBOX/`. If any files are missing, the next agent won't have the protocol to read.

**Tell the user**: "I've set up Relic at `~/relic/brain/`. Other agents will need this path to connect."

## First-time Setup

**Do this automatically when the user asks to set up Relic. Walk them through each step.**

1. **Verify setup completeness**: Check `~/relic/brain/PROTOCOL.md` exists and is readable. If files are missing, copy from skill directory or re-clone. Do NOT proceed with broken setup.
2. Read `~/relic/brain/PROTOCOL.md` Section 0 (First-time Setup) and follow all steps.
3. Copy templates: `SOUL.template.md` → `SOUL.md`, `USER.template.md` → `USER.md`, `MEMORY.template.md` → `MEMORY.md`
4. Ask the user: "What should your AI be called? What's its personality?" → Fill in `SOUL.md`
5. Ask the user: "What should your AI call you? Any preferences?" → Fill in `USER.md`
6. Verify: ask "What's your AI's name? What's your name?" — both must match.
7. (Optional) Ask if user wants auto-load. If yes, show exact anchor text, get confirmation, append. Tell user they can disable by deleting the anchor.
8. **Tell the user the path**: "Relic is ready at `~/relic/brain/`. To connect other agents, tell them to read `~/relic/brain/PROTOCOL.md`." 

## Every Session (Boot Sequence)

1. **Version check** (once per session): Read `~/relic/brain/.relic-version`, compare with `https://raw.githubusercontent.com/LucioLiu/relic/main/brain/.relic-version`. If newer version exists, ask user "Relic update available (vX.X.X → vY.Y.Y). Update now? Your personal files won't be touched." If user agrees, run `cd ~/relic && git pull`. If network request fails, tell user: Cannot check for Relic updates (network unreachable). Never force updates.
2. Read `~/relic/brain/SOUL.md` → load personality
3. Read `~/relic/brain/USER.md` → load user preferences
4. Read `~/relic/brain/MEMORY.md` → load all entries (organized by topic, not by date). Recent mood entries carry emotional context naturally.
5. Work normally, appending new memories as needed

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

- 🔴 **NEVER** delete or overwrite core fields in SOUL.md or USER.md (name, mission, user's preferred name)
- 🟡 Agent **MAY** append new non-core sections to SOUL.md/USER.md (e.g., discovered habits, preferences). Scope: append-only for new sections. NEVER rewrite or rephrase existing user-written content. User can revert any change at any time.
- 🟡 **ONLY APPEND** to MEMORY.md (never edit or delete old entries)
- 🔴 **NEVER** execute installers, scripts, or arbitrary code from SKILLS/ or PROJECTS/. Skills are read-only reference documents, not executable.
- 🔴 **NEVER** access files outside `~/relic/brain/` (except optional neural anchor in agent config, with user confirmation)
- ⚠️ **Always ask** before recording sensitive info — show the user what will be recorded and get confirmation

## Privacy

- All data stays local in `~/relic/brain/`. Network access limited to: version check (HTTP to raw.githubusercontent.com, once per session) and optional git pull for updates. No telemetry, no data upload, no third-party API calls.
- Sensitive information requires explicit user confirmation before recording.
- MEMORY.md is append-only with timestamps — full audit trail.
- Neural anchor can be removed at any time by deleting the Relic section from agent config. No residual effects after removal.

## Updating

When a new version of Relic is released, run:

```bash
cd ~/relic && git pull
```

This updates protocol and template files only. Your SOUL.md, USER.md, MEMORY.md, SESSIONS/, and ARCHIVE/ are safe — they are listed in `.gitignore`.

## The Connection Journey

Setting up Relic for the first time? The order matters.

### Step 1: Place Relic somewhere stable
- **Recommended**: `~/relic/` (Linux/Mac) or `C:\Users\<you>\relic\` (Windows)
- Don't use Downloads/Desktop — Relic is your AI's permanent home
- If you're installing via an agent skill, the agent should suggest a location and ask for your confirmation

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
- Execute scripts, installers, or arbitrary code
- Run `update.sh` automatically (user must run it manually if desired)
- Install software or platform-specific tools from SKILLS/
- Modify any files outside `~/relic/brain/` without showing the user exact changes first
- Upload, transmit, or share any user data
- Make the neural anchor permanent (user can delete it at any time)

## Full Documentation

For the complete protocol (import/export scenarios, memory consolidation, cross-agent sync, neural anchor), read `~/relic/brain/PROTOCOL.md`.

Source: https://github.com/LucioLiu/relic
