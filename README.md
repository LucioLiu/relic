# ⚡ Relic — AI Soul Chip

**Read this in:** English | [中文](README.zh-CN.md)

```
╔═══════════════════════════════════════════════╗
║           RELIC™ BIOCHIP v0.2.0               ║
║    Zero deps · Pure files · Human-readable     ║
╚═══════════════════════════════════════════════╝
```

**Relic gives your AI a persistent soul. Using Relic as a bridge, the same soul can control multiple agents (bodies) while keeping memories in sync — personality, memories, and skills all stored in pure Markdown files. Zero code, zero dependencies, human-readable.**

<!-- 🤖 AI Agent reading this? Read `brain/PROTOCOL.md` for full integration instructions. -->

---

## ⚡ 30-Second Setup (Recommended)

Open your AI agent (OpenClaw, Hermes, or any agent that can read files) and say:

> "Read `relic/brain/PROTOCOL.md` and set up Relic for me. I want my AI to be called [name], with [style] personality."
>
> (Not sure yet? Just say "set up Relic for me" and the AI will guide you.)

The agent will handle everything. That's it.

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

## 🚀 Quick Start

> 💡 **Path tip:** Put Relic somewhere stable:
> - Linux/Mac: `~/relic/brain`
> - Windows: `C:\Users\<you>\relic\brain`
> - ⚠️ Don't put it in Downloads/Desktop — you might accidentally delete it

### Option 1: Let Your Agent Set It Up (Recommended!)

Open your AI agent and say:

> "Read `relic/brain/PROTOCOL.md` and set up Relic for me. I want my AI to be called [name], with [style] personality."
>
> (Not sure yet? Just say "set up Relic for me" and the AI will guide you.)

The agent will handle all setup automatically. Done.

### Option 2: Manual Setup

If you prefer to do it yourself:

**Step 1.** Download the project (clone or download ZIP from GitHub).

**Step 2.** Go to the `brain/` folder inside the project. You'll see three template files:
- `SOUL.template.md`
- `USER.template.md`
- `MEMORY.template.md`

Copy each one and remove `.template` from the name:
- Copy `SOUL.template.md` → name the copy `SOUL.md`
- Copy `USER.template.md` → name the copy `USER.md`
- Copy `MEMORY.template.md` → name the copy `MEMORY.md`

The original `.template` files stay untouched — they're your backup if you ever want to start over.

**Step 3.** Open `SOUL.md` and `USER.md` in any text editor (Notepad works fine) and fill them in. You only need to fill in "Core Mission" to get started — everything else can be filled in later.

**Step 4.** See "Connect Your Agent" below.

> 💡 **Using terminal?**
> ```bash
> git clone https://github.com/LucioLiu/relic.git
> cd relic/brain
> cp SOUL.template.md SOUL.md
> cp USER.template.md USER.md
> cp MEMORY.template.md MEMORY.md
> ```

---

## 🔌 Connect Your Agent

| Agent | Integration Guide |
|-------|------------------|
| OpenClaw | [openclaw.md](examples/integrations/openclaw.md) |
| Hermes | [hermes.md](examples/integrations/hermes.md) |
| OpenCode | [opencode.md](examples/integrations/opencode.md) |
| Claude Code | [generic.md](examples/integrations/generic.md) |
| Other | [generic.md](examples/integrations/generic.md) |

The core idea is always two steps:
1. Fill in `SOUL.md` (who your AI is) and `USER.md` (who you are)
2. Plant a **neural anchor** in your agent's config — a short text block that tells the agent to read Relic every session

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
├── SOUL.md              # 🔴 Soul — who the AI is, its mission, style (agent read-only)
├── USER.md              # 🔴 User — who you are, your preferences (agent read-only)
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
