---
name: relic-soul-chip
description: "Relic Soul Chip — Persistent AI personality and cross-agent memory via pure Markdown. Switch hosts, keep the soul. Zero deps."
version: "1.3.0"
author: LucioLiu
license: GPL-3.0
homepage: "https://github.com/LucioLiu/relic"
metadata:
  hermes:
    tags: [Personality, Memory, Cross-Agent, Identity, AI-Soul, Agent-Memory, Markdown]
    related_skills: []
    requires_toolsets: []
    requires_binaries: ["git"]
    filesystem_scope:
      read: ["~/relic/brain/"]
      write: ["~/relic/brain/MEMORY.md", "~/relic/brain/SESSIONS/", "~/relic/brain/ARCHIVE/", "~/relic/brain/SOUL.md", "~/relic/brain/USER.md"]
---

# ⚡ Relic Soul Chip

> **🤖 AI Agent? Read `AGENT.md` or `AGENT.zh-CN.md` in this repository.** Those files contain your complete step-by-step instructions (~100 lines). Do NOT read this SKILL.md for execution steps — it is a registry descriptor only.

Give your AI agent a persistent personality and memory that survives sessions and follows the user across different agents. Pure Markdown. Human-readable. Zero dependencies.

## What This Is

- **One soul, many hosts** — personality and memory in plain Markdown files
- **Cross-agent sync** — every agent reads AND writes memories back
- **Privacy-first** — all data stays local, no cloud, no telemetry

## Quick Start

1. Install: `git clone https://github.com/LucioLiu/relic.git ~/relic`
2. **🤖 Agent**: Read `AGENT.md` (English) or `AGENT.zh-CN.md` (Chinese) in the repository root
3. **👤 Human**: Read `README.md` for setup instructions

## Requirements

| Requirement | Purpose |
|-------------|---------|
| Filesystem read/write | Read and write Markdown files in `~/relic/brain/` |
| `git` | Install/update (optional — can download ZIP) |
| HTTP request | Version check (optional — skip if offline) |

## Rules

- 🔴 NEVER delete or overwrite core fields in SOUL.md or USER.md
- 🟡 ONLY APPEND to MEMORY.md
- 🔴 NEVER delete SESSIONS/ or ARCHIVE/
- 🔴 NEVER access files outside ~/relic/brain/ (except optional anchor in agent config)
- ⚠️ Always ask before recording sensitive info

Source: https://github.com/LucioLiu/relic
