---
name: relic
description: "Give your AI agent a persistent personality and memory across sessions. Pure Markdown files. Read SOUL.md for personality, USER.md for user preferences, MEMORY.md for memories. Switch agents, keep the soul."
---

# ⚡ Relic Soul Chip

> *"Store a soul as a digital file. Plug it into any AI agent. Even V."*

Give your AI agent a persistent personality and memory that survives sessions and follows the user across different agents. Pure Markdown. Human-readable. No code, no dependencies.

**Switch agents. Keep the soul.**

## When to Use

- User says "set up Relic" or "I want my AI to remember me"
- User wants persistent personality across sessions
- User switches between multiple AI agents and wants continuity
- User mentions personality, memory, identity for their AI

## How It Works

Relic stores everything in plain Markdown files in `~/relic/brain/`:

| File | Purpose | Agent Access |
|------|---------|-------------|
| `SOUL.md` | AI personality (name, mission, values) | Read only |
| `USER.md` | User preferences (name, habits, style) | Read only |
| `MEMORY.md` | Event log (decisions, experiences) | Append only |
| `PROTOCOL.md` | Full protocol instructions | Read only |

All files live in `~/relic/brain/` (or wherever the user specifies). No access to files outside this directory.

## First-time Setup

1. Download Relic from https://github.com/LucioLiu/relic (clone or download ZIP)
2. Copy templates to active files: `SOUL.template.md` → `SOUL.md`, `USER.template.md` → `USER.md`, `MEMORY.template.md` → `MEMORY.md`
3. Help user fill in SOUL.md (at minimum: AI name + core mission)
4. Help user fill in USER.md (at minimum: preferred name + communication preferences)
5. Verify: ask "What's my AI's name? What's my name?" — both must be correct

## Every Session (Boot Sequence)

1. Read SOUL.md → load personality
2. Read USER.md → load user preferences
3. Read MEMORY.md → load recent events (last 30 entries)
4. Work normally, appending new memories as needed

## Memory Writing

Append to MEMORY.md with this format:

```
## YYYY-MM-DD HH:MM [AgentName]
Content: [what happened]
Type: preference / decision / experience / event / correction
Importance: high / medium / low
```

## Switching Agents

The user's soul lives in `~/relic/brain/`. Any agent that can read files can connect. The new agent reads the same files — all memories from previous agents are preserved.

## Rules

- 🔴 **NEVER** modify SOUL.md or USER.md (read-only after setup)
- 🟡 **ONLY APPEND** to MEMORY.md (never edit or delete old entries)
- 🔴 **NEVER** access files outside `~/relic/brain/`
- ⚠️ **Always ask** before recording sensitive info — show the user what will be recorded and get confirmation

## Privacy

- All data stays local in `~/relic/brain/`. No network access, no API calls, no telemetry.
- Sensitive information (names, emails, phone numbers, passwords) requires explicit user confirmation before recording.
- MEMORY.md is append-only with timestamps — full audit trail.

## Full Documentation

For the complete protocol (import scenarios, memory consolidation, cross-agent sync, optional neural anchor for auto-loading), read `~/relic/brain/PROTOCOL.md`.

Source: https://github.com/LucioLiu/relic
