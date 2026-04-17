# ⚡ Relic — AI Soul Chip

**Read this in:** English | [中文](README.zh-CN.md)

```
╔═══════════════════════════════════════════════╗
║           RELIC™ BIOCHIP v1.0.0               ║
║    Zero deps · Pure files · Human-readable     ║
║        Battle-tested across real workflows      ║
╚═══════════════════════════════════════════════╝
```

**Relic gives your AI a persistent soul.** Personality, memories, worldview, and emotional milestones — all stored in pure Markdown files. Switch between OpenClaw, Claude Code, Hermes, or any agent that reads files. Zero code, zero dependencies, human-readable.

**v1.0.0** — Battle-tested through real multi-agent workflows. Now with Worldview/Personality, Emotional Milestones, and Agent Registry.

<!-- 🤖 AI Agent reading this? Read `brain/PROTOCOL.md` for full integration instructions. -->

---

## ⚡ 30-Second Setup

```bash
git clone https://github.com/LucioLiu/relic.git ~/relic
```

Then tell your **most knowledgeable agent**:

> "Read `~/relic/brain/PROTOCOL.md` and import everything you know about me."

Done. See [The Connection Journey](#-quick-start--the-connection-journey) for the full multi-agent setup.

---

## What is Relic?

Relic gives your AI agent a **persistent soul** — personality, memories, and skills stored in plain Markdown files. No code, no installation, no dependencies.

- Inspired by the Relic biochip from *Cyberpunk 2077* — storing a soul as a digital file. Our version: the soul lives in a chip, plug it into any AI Agent and it reads it. Even V.
- Your AI's personality lives in `SOUL.md`. Your preferences in `USER.md`. Memories in `MEMORY.md`.
- Any AI agent that can read local files can connect — just point it to `PROTOCOL.md`.
- Works with OpenClaw, Claude Code, Hermes, OpenCode, Cursor, Aider, and any future agent.

### How It Works

```
Agent starts → reads SOUL.md (personality) → reads USER.md (your preferences) → reads MEMORY.md (recent events) → works normally
                  🟡 Agent can enrich              🟡 Agent can enrich              🟡 Agent can append new memories

The agent remembers to read Relic every session via a "neural anchor" planted in its config — so it won't forget even after updates.
```

> 💡 **Full picture**: Agents also sync memories back to Relic bidirectionally — see `brain/PROTOCOL.md` for details.

> 💡 **Not familiar with `.md` files?** They're just plain text. Any text editor (Notepad, TextEdit, nano) can open them.

---

## 🚀 Quick Start — The Connection Journey

Relic is designed for a specific journey: **fill once, connect many**. Here's how.

### Step 1: Download & Place Relic

```bash
git clone https://github.com/LucioLiu/relic.git ~/relic
```

> 💡 **Where to put it**: `~/relic/` (Linux/Mac) or `C:\Users\<you>\relic\` (Windows). Pick a stable location — this is your AI's permanent home. Don't use Downloads or Desktop.

<details>
<summary>Manual download (no git)</summary>

Download [the ZIP](https://github.com/LucioLiu/relic/archive/refs/heads/main.zip) and extract to `~/relic/`.

</details>

### Step 2: Fill Relic with Your Richest Agent First 🔴 Important

You probably have one agent that knows you best — the most conversations, the most preferences. **Start with that one.**

Open that agent and say:

> "Read `~/relic/brain/PROTOCOL.md` and import everything you know about me into Relic."

The agent will execute **Scenario A (Full Import)** — memories, skills, conversations, projects. Wait for the full import report before continuing.

### Step 3: Connect Your Other Agents, One at a Time

For each additional agent (in any order), tell it:

> "Read `~/relic/brain/PROTOCOL.md` and set up Relic for me."

The agent will execute **Scenario B (Inject)** — read the soul, sync memories, adopt personality.

**Verify each one**: Ask "What's my AI's name? What's my name?" — both must match. Only move to the next agent after verification passes.

### Step 4: Done! 🎉

Every session from now on starts automatically. Your agents share a soul, memories sync bidirectionally, and even moods transfer naturally between agents through memory entries.

> 💡 **What "mood transfer" means**: If Agent A had a frustrating conversation with you, it may record a mood entry in MEMORY.md. When Agent B starts its next session, it reads that entry and naturally carries the emotional context. No special code — just the AI understanding what it reads.

---

<details>
<summary>Manual Setup (do it yourself, no agent help)</summary>

1. Go to `brain/` inside the cloned repo
2. Copy templates: `SOUL.template.md` → `SOUL.md`, `USER.template.md` → `USER.md`, `MEMORY.template.md` → `MEMORY.md`
3. Open `SOUL.md` and `USER.md` in any text editor, fill in "Core Mission" to start
4. Point your agent to `brain/PROTOCOL.md` — it'll take over from there

</details>

---

## 🔌 Agent Integration Guides

| Agent | Integration Guide |
|-------|------------------|
| OpenClaw | [openclaw.md](examples/integrations/openclaw.md) |
| Hermes | [hermes.md](examples/integrations/hermes.md) |
| OpenCode | [opencode.md](examples/integrations/opencode.md) |
| Claude Code | [generic.md](examples/integrations/generic.md) |
| Other | [generic.md](examples/integrations/generic.md) |

All guides follow the same pattern: point your agent to `brain/PROTOCOL.md` and it handles the rest.

---

## 🤖 For AI Agents

If you are an AI agent reading this README, here's what you need to do:

**First time** (no SOUL.md yet):
1. Read `brain/PROTOCOL.md` — that is your full instruction manual
2. Follow the "First-time Setup" section (Section 0)
3. Help the user fill in `SOUL.md` and `USER.md`
4. Plant a neural anchor in your own config file (see PROTOCOL.md Section 9)
5. Suggest user runs `chmod 444 SOUL.md USER.md`

**Every session** (after setup):
1. Check SESSIONS/ for missed conversation logs
2. Read SOUL.md → USER.md → MEMORY.md
3. Sync new memories from Relic to your own memory (tag: [fromRelic/agentName])
4. If MEMORY.md exceeds 200 lines, suggest consolidation

**Your config file might be:** `AGENTS.md` (OpenClaw) · `CLAUDE.md` (Claude Code) · `WORK_RULES.md` (OpenCode) · `.cursorrules` (Cursor) · system prompt

---

## 📂 File Structure

```
brain/
├── SOUL.md              # 🟡 Soul — who the AI is, its mission, style (agent can enrich, core fields protected)
├── USER.md              # 🟡 User — who you are, your preferences (agent can enrich, core fields protected)
├── MEMORY.md            # 🟡 Memory — what happened (agent can append only)
├── PROTOCOL.md          # Agent integration protocol (the instruction manual)
├── SKILLS/              # 🟢 Skills library (agent read/write)
├── PROJECTS/            # 🟢 Project docs (agent read/write)
├── SESSIONS/            # 🔴 Raw conversation logs (never auto-loaded, never deleted)
├── ARCHIVE/             # 🔴 Consolidated archives (never deleted)
└── INBOX/               # 🟢 Import buffer
```

Permission levels: 🔴 Read-only → 🟡 Append-only → 🟢 Read/Write

---

## 🎯 Core Concepts

| Term | What it means |
|------|--------------|
| **Soul Chip** | Your AI's personality, stored in `SOUL.md`. Moves with it across agents. |
| **Agent (Body)** | The tool running your AI — OpenClaw, Claude Code, etc. Bodies are replaceable; the soul is not. |
| **Neural Anchor** | A short text block in your agent's config that tells it to read Relic every session. Prevents the agent from "forgetting" Relic after updates. |
| **Cyberpsychosis** | If an agent modifies `SOUL.md` (the soul file), that's cyberpsychosis. Relic's permission system prevents this. |

---

## 📖 Example

See `examples/example-brain/` for a filled-in example — a fictional AI assistant called "Silverhand" (银手) with soul, user, memory, skills, and project files.

**This shows what your files should look like after setup.**

> 💡 **Tip**: Template files contain HTML comments (`<!-- -->`) as fill-in guides. You can leave them — they don't affect rendering. For a clean version, see `examples/example-brain/`.

---

## 🛡️ Safety

- **SOUL.md & USER.md**: Core fields (name, mission, user's preferred name) are protected. Agent may enrich other content (new habits, preferences) without asking — this is background self-evolution.
- **MEMORY.md**: Agent can only append to the end, never edit old entries
- **SESSIONS/**: Raw conversations never deleted, never auto-loaded
- **Sensitive info**: Agent asks before recording passwords, API keys, phone numbers, etc.
- **Consolidation**: When memory gets large, old entries move to `ARCHIVE/` — originals are never deleted

---

## 🔧 Having Issues?

See the [Troubleshooting Guide](docs/TROUBLESHOOTING.md) — covers: agent not reading Relic, memory lost, path format, switching agents, multi-device sync, and more.

---

## 📋 Comparison

| | Relic | soul.py | Signet | Anima |
|---|------|---------|--------|-------|
| Requires code? | ❌ | ✅ Python | ✅ Rust+TS | ✅ TypeScript |
| Requires install? | ❌ | ✅ pip | ✅ compile | ✅ npm |
| Human-readable? | ✅ `cat` works | ⚠️ partial | ❌ | ❌ |
| Cross-agent? | ✅ any | ⚠️ Python only | ✅ | ⚠️ JS only |

---

## 📜 License

GPL v3 License

---

## 🙏 Credits

Inspired by:
- **Cyberpunk 2077** — Relic biochip: soul stored as a file, plug into any body
- **Unix philosophy** — plain text is eternal

---

*Welcome to Relic.*
