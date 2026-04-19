# Manual Setup Guide

No AI help needed. Do it yourself.

## Steps

1. **Open the `brain/` folder** inside the downloaded `relic` folder

2. **Copy template files to active files** (templates have `.template` in the name — they're blank forms):
   - `SOUL.template.md` → rename copy to `SOUL.md`
   - `USER.template.md` → rename copy to `USER.md`
   - `MEMORY.template.md` → rename copy to `MEMORY.md`

3. **Open `SOUL.md`** in any text editor (Notepad, TextEdit, VS Code — anything works) and fill in at least the "Core Mission" section

4. **Open `USER.md`** and fill in your preferences

5. **(Mac/Linux only) Lock the files** to prevent accidental changes:
   ```
   chmod 444 SOUL.md USER.md
   ```
   This locks the files against accidental modification. Unlock first if you need to edit later. Windows users skip this.

6. **Point your AI tool** to `AGENT.md` (English) or `AGENT.zh-CN.md` (Chinese) — it'll take over from there

## The Seven Files

| File | Purpose |
|------|---------|
| `SOUL.md` | AI's soul — name, personality, mission, style |
| `USER.md` | Your info — preferred name, preferences, habits |
| `MEMORY.md` | Long-term memory — preferences, decisions, experiences (extracted knowledge, not raw chat) |
| `SKILLS/` | Skills — learned capabilities, one folder per skill |
| `PROJECTS/` | Projects — documentation for things worked on |
| `SESSIONS/` | Conversation logs — full raw chat transcripts with the AI |
| `ARCHIVE/` | Archive — old memories moved here when too long, never deleted |

## Connect Your AI Tool

| AI Tool | How to Connect |
|---------|---------------|
| OpenClaw | See `examples/integrations/openclaw.md` |
| Hermes | See `examples/integrations/hermes.md` |
| Claude Code | See `examples/integrations/generic.md` |
| Cursor | See `examples/integrations/generic.md` |
| Other | See `examples/integrations/generic.md` |

All tools follow the same pattern: tell the AI to read `AGENT.md`, it handles the rest.

Having issues? See `docs/TROUBLESHOOTING.md`.
