# ⚡ Relic — AI Soul Chip

**Read this in:** English | [中文](README.zh-CN.md)

```
╔═══════════════════════════════════════════════╗
║           RELIC™ BIOCHIP v1.1.1               ║
║    Zero deps · Pure files · Human-readable     ║
║        Battle-tested across real workflows      ║
╚═══════════════════════════════════════════════╝
```

**Relic gives your AI a persistent soul that works across all AI tools.** Personality, memories, skills, and project knowledge — all stored in plain text files. Works with OpenClaw, Claude Code, Hermes, Cursor, Aider, or any AI that can read files. No code, no installation, no dependencies.

---

## 👇 First, pick one:

- 🤖 **"I'm an AI Agent"** → Jump to [For AI Agents](#-for-ai-agents)
- 👤 **"I'm a human"** → Keep reading below

---

## What is Relic?

Relic is a folder of text files that stores your AI's personality and memories. Think of it as a USB drive for your AI's soul — plug it into any AI tool, and that tool instantly knows who your AI is, what you like, and what you've worked on together.

**What's inside (all in the `brain/` folder):**
- `SOUL.md` — Your AI's personality, values, and mission
- `USER.md` — Your preferences, habits, and communication style
- `MEMORY.md` — What happened recently (conversations, decisions, lessons learned)
- `SKILLS/` — Reusable skills and workflows your AI has learned
- `PROJECTS/` — Documents for ongoing projects
- `SESSIONS/` — Raw conversation logs (preserved forever)
- `ARCHIVE/` — Old memories that got too long (originals never deleted)

**The key idea:** Every AI tool you use reads from and writes to the same files. OpenClaw writes a memory → Claude Code reads it next session. No API, no cloud, no sync service — just files on your computer.

> 💡 Inspired by the Relic biochip from *Cyberpunk 2077* — Arasaka's "Secure Your Soul" project: a technology that converts human consciousness into digital engrams stored on a biochip. Plug it into any host, and the personality lives on. We adapted this for AI agents.

---

## 🚀 Setup Guide

### How do you want to set up?

- 🤝 **"Let my AI do it"** (recommended) → Go to Step 1 below
- ✋ **"I'll do it myself"** → Jump to [Manual Setup](#-manual-setup-do-it-yourself)

### Step 1: Download Relic

First, get the Relic folder onto your computer.

**If you know how to use a terminal / command line**, run:
```
git clone https://github.com/LucioLiu/relic.git ~/relic
```

**If that looks like gibberish** — no worries! Download the ZIP file instead:
1. Click this link: [Download Relic ZIP](https://github.com/LucioLiu/relic/archive/refs/heads/main.zip)
2. Extract the ZIP file
3. Put the `relic` folder somewhere you can find later — like your home folder
   - Mac: `/Users/yourname/relic/`
   - Windows: `C:\Users\yourname\relic\`
   - Linux: `/home/yourname/relic/`

> 💡 Pick a stable location — this is your AI's permanent home. Don't use Downloads or Desktop.

### Step 2: Tell Your Best AI Agent to Set It Up

Open the AI tool that **knows you best** — the one you've had the most conversations with. Then say:

> "Read `~/relic/brain/PROTOCOL.md` and import everything you know about me into Relic."

Your AI will walk you through the rest. It'll ask you questions, fill in the files, and set everything up.

Wait for the setup to fully complete before connecting other AI tools.

### Step 3: Connect Your Other AI Tools, One at a Time

For each additional AI tool (in any order), tell it:

> "Read `~/relic/brain/PROTOCOL.md` and set up Relic for me."

**Verify each one**: Ask "What's my AI's name? What's my name?" — both must match. Only move to the next tool after verification passes.

### Step 4: Done! 🎉

Every session from now on starts automatically. Your AI tools share a soul, memories sync bidirectionally, and everything is stored in plain text files you control.

> 💡 **How sync works**: Each AI tool reads from and writes to the same Relic files. When you start a new session, the tool reads all seven memory files and catches up. But sync only happens at session start — if you switch tools mid-conversation, the current conversation won't be in Relic yet. Need to hand off immediately? Just tell your current AI: "Write the key points from this conversation to Relic now."

---

<details>
<summary>🔧 Manual Setup (do it yourself)</summary>

No AI help needed. Here's how:

1. **Open the `brain/` folder** inside the downloaded `relic` folder
2. **Copy template files to active files** (templates have `.template` in the name — they're like blank forms for you to fill in):
   - `SOUL.template.md` → rename copy to `SOUL.md`
   - `USER.template.md` → rename copy to `USER.md`
   - `MEMORY.template.md` → rename copy to `MEMORY.md`
3. **Open `SOUL.md`** in any text editor (Notepad, TextEdit, VS Code — anything works) and fill in at least the "Core Mission" section
4. **Open `USER.md`** and fill in your preferences
5. **(Mac/Linux only) Lock the files** to prevent accidental changes:
   ```
   chmod 444 SOUL.md USER.md
   ```
   This means "lock these files so nothing can modify them accidentally — like putting a padlock on a diary." If you need to edit them later, unlock first. Windows users can skip this.
6. **Point your AI tool** to `brain/PROTOCOL.md` — it'll take over from there

</details>

---

## 🔌 Which AI Tool Are You Using?

| AI Tool | How to Connect |
|---------|---------------|
| OpenClaw | See `examples/integrations/openclaw.md` |
| Hermes | See `examples/integrations/hermes.md` |
| OpenCode | See `examples/integrations/opencode.md` |
| Claude Code | See `examples/integrations/generic.md` |
| Cursor | See `examples/integrations/generic.md` |
| Any other tool | See `examples/integrations/generic.md` |

All guides follow the same pattern: point your AI to `brain/PROTOCOL.md` and it handles the rest.

---

## 🤖 For AI Agents

If you are an AI agent reading this, here's what you need to do:

**First time** (no SOUL.md yet):
1. Read `brain/PROTOCOL.md` — that is your full instruction manual
2. Follow the "First-time Setup" section (Section 0)
3. Help the user fill in `SOUL.md` and `USER.md`
4. Plant a neural anchor in your own config file (see PROTOCOL.md Section 9)
5. Suggest user runs `chmod 444 SOUL.md USER.md` — this locks the files to prevent accidental changes

**Every session** (after setup):
1. Check `SESSIONS/` for missed conversation logs
2. Read `SOUL.md` → `USER.md` → `MEMORY.md` → scan `SKILLS/` and `PROJECTS/`
3. Sync new memories from Relic to your own memory (tag: [fromRelic/agentName])
4. Write new memories back to Relic (bidirectional sync)
5. If `MEMORY.md` exceeds 200 lines, suggest consolidation

**Your config file** (where the anchor goes):
- OpenClaw → `AGENTS.md`
- Claude Code → `CLAUDE.md`
- Hermes → config file or prompt template
- OpenCode → `WORK_RULES.md` or instructions
- Cursor → `.cursorrules`

---

## 📂 File Structure

```
brain/
├── SOUL.md              # 🟡 Soul — who the AI is (agent can enrich, core fields protected)
├── USER.md              # 🟡 User — who you are (agent can enrich, core fields protected)
├── MEMORY.md            # 🟡 Memory — what happened (agent can append only)
├── PROTOCOL.md          # Agent integration protocol (the instruction manual)
├── SKILLS/              # 🟢 Skills library (agent read/write)
├── PROJECTS/            # 🟢 Project docs (agent read/write)
├── SESSIONS/            # 🔴 Raw conversation logs (never deleted)
├── ARCHIVE/             # 🔴 Consolidated archives (never deleted)
└── INBOX/               # 🟢 Import buffer
```

Permission levels: 🔴 Read-only → 🟡 Enrichable (core protected) / Append-only → 🟢 Read/Write

> 💡 **About SKILL.md files**: The project root has two SKILL.md files — `SKILL.md` (for Hermes/agentskills.io platforms) and `skill/SKILL.md` (for ClawHub platform). These are **platform integration descriptions**, NOT the same as `brain/SKILLS/` which stores your AI's actual learned skills. Your real skills live in `brain/SKILLS/`.

---

## 🎯 Core Concepts

| Term | What it means |
|------|--------------|
| **Soul** | Your AI's personality, stored in `SOUL.md`. Moves with it across tools. |
| **Host (Body)** | The AI tool running your agent — OpenClaw, Claude Code, etc. Hosts are replaceable; the soul is not. |
| **Neural Anchor** | A short text block in your AI tool's config that tells it to read Relic every session. Prevents the AI from "forgetting" Relic after updates. |
| **Bidirectional Sync** | Your AI reads from Relic AND writes new memories back. Every connected tool stays in sync. |
| **Cyberpsychosis** | Modifying core fields in `SOUL.md` (name, mission) — Relic's permission system protects against this. Agents *can* enrich SOUL.md with new habits and preferences — that's healthy self-evolution, not cyberpsychosis. |

---

## 📖 Example

See `examples/example-brain/` for a filled-in example — a fictional AI assistant called "Silverhand" with soul, user, memory, skills, project, session, and archive files.

**This shows what your files should look like after setup.**

> 💡 Template files contain HTML comments (`<!-- -->`) as fill-in guides. You can leave them — they don't affect anything. For a clean version, see `examples/example-brain/`.

---

## 🛡️ Safety

- **SOUL.md & USER.md**: Core fields (name, mission, user's preferred name) are protected. Agent may enrich other content (new habits, preferences) without asking — this is healthy self-evolution.
- **MEMORY.md**: Agent can only append to the end, never edit old entries
- **SESSIONS/**: Raw conversations never deleted, never auto-loaded
- **Sensitive info**: Agent asks before recording passwords, API keys, phone numbers, etc.
- **Consolidation**: When memory gets large, old entries move to `ARCHIVE/` — originals are never deleted

---

## 🔧 Having Issues?

See `docs/TROUBLESHOOTING.md` — covers: agent not reading Relic, memory lost, path format, switching tools, multi-device sync, and more.

---

## 📜 License

GPL v3 License

---

## 🙏 Credits

Created by [LucioLiu](https://github.com/LucioLiu) · Source: [github.com/LucioLiu/relic](https://github.com/LucioLiu/relic)

Inspired by:
- **Cyberpunk 2077** — Arasaka's Relic biochip: "Secure Your Soul" — consciousness as a digital file
- **Unix philosophy** — plain text is eternal

---

*Welcome to Relic.*
