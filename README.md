# 👤 Relic — AI Soul Chip (For Humans)

> **🤖 Are you an AI Agent?** → This file is not for you. Read [`AGENT.md`](AGENT.md)

**Read this in:** English | [中文](README.zh-CN.md)

```
╔═══════════════════════════════════════════════╗
║           RELIC™ BIOCHIP v1.2.0               ║
║    Zero deps · Pure files · Human-readable     ║
╚═══════════════════════════════════════════════╝
```

**Relic gives your AI a persistent soul that works across all AI tools.** Personality, memories, skills, and project knowledge — all stored in plain text files. Works with OpenClaw, Claude Code, Hermes, Cursor, Aider, or any AI that can read files. No code, no installation, no dependencies.

> 💡 Inspired by the Relic biochip from *Cyberpunk 2077* — store a soul as a digital file, plug it into any host.

---

## What does it do?

**Every time you switch AI tools, you have to teach your AI who you are all over again.** OpenClaw knows one version of you, Hermes knows another.

**Relic fixes this.** One folder of text files. All your AI tools share the same soul and memories. No cloud service, no API — just Markdown files on your computer.

## What's inside (all in the `brain/` folder)

- `SOUL.md` — Your AI's personality, values, and mission
- `USER.md` — Your preferences, habits, and communication style
- `MEMORY.md` — Structured long-term memory (preferences, decisions, experiences — extracted knowledge, not raw chat)
- `SKILLS/` — Reusable skills and workflows your AI has learned
- `PROJECTS/` — Documents for ongoing or completed plans
- `SESSIONS/` — Full raw conversation transcripts with the user (preserved forever)
- `ARCHIVE/` — Archived memories when files get too long (originals never deleted)

---

## 🚀 Setup Guide

### How do you want to set up?

- 🤝 **"Let my AI do it"** (recommended) → Read on below
- ✋ **"I'll do it myself"** → Jump to [`docs/manual-setup.md`](docs/manual-setup.md)

### Step 1: Download Relic

**If you know how to use a terminal:**
```
git clone https://github.com/LucioLiu/relic.git ~/relic
```

**Otherwise:** [Download ZIP](https://github.com/LucioLiu/relic/archive/refs/heads/main.zip), extract it, put it somewhere stable (like your home folder). Don't use Downloads or Desktop.

### Step 2: Tell Your Best AI Agent to Set It Up

Open the AI tool that **knows you best**. Then say:

> "Read `AGENT.md` and import everything you know about me into Relic."

Your AI will walk you through the rest. Wait for it to fully complete before connecting other tools.

### Step 3: Connect Your Other AI Tools, One at a Time

For each additional AI tool, tell it:

> "Read `AGENT.md` and set up Relic for me."

The AI will automatically determine the scenario: if Relic is empty it performs a full import; if Relic already has data it performs an injection (reads the soul, syncs memories, plants anchor).

**Verify each one**: Ask "What's my AI's name? What's my name?" — both must match.

### Step 4: Done! 🎉

Every session from now on starts automatically. Your AI tools share a soul, memories sync bidirectionally.

---

## 🔌 Which AI Tool Are You Using?

| AI Tool | How to Connect |
|---------|---------------|
| OpenClaw | `examples/integrations/openclaw.md` |
| Hermes | `examples/integrations/hermes.md` |
| Claude Code | `examples/integrations/generic.md` |
| Cursor | `examples/integrations/generic.md` |
| Other | `examples/integrations/generic.md` |

---

## 🛡️ Safety

- SOUL.md & USER.md: Core fields protected — AI can never delete them
- MEMORY.md: Append only — AI can never edit old entries
- SESSIONS/: Raw conversations never deleted
- Sensitive info: AI asks before recording passwords, phone numbers, etc.
- All data stays local — nothing uploaded anywhere
- **Known limitation**: Skill files may not be directly portable across platforms due to different tool formats. Relic syncs skill descriptions, not platform-specific implementations.

---

## 📖 More

- [Manual Setup Guide](docs/manual-setup.md)
- [Troubleshooting](docs/TROUBLESHOOTING.md)
- [Full Protocol Reference](docs/protocol.md) (for AI agents, but curious humans welcome)

## 📜 License

GPL v3 · Created by [LucioLiu](https://github.com/LucioLiu) · Source: [GitHub](https://github.com/LucioLiu/relic)

---

*Welcome to Relic.*
