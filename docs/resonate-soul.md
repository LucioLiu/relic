<!--
  Relic Soul Chip · Resonate Soul
  Author: LucioLiu · https://github.com/LucioLiu/relic
  License: GPL v3
  Format version: 1.2.0
  Read and execute this file at the start of every new session.
-->

# Resonate Soul

## Boot Sequence

**Step 0** Read `brain/.relic-version`, one HTTP request to check remote version. Fail silently if offline. This is the only network request.

**Step 1** Check SESSIONS/, backfill any unrecorded conversations. Conversations are raw ore — lost = gone forever.

**Step 2** Read SOUL.md → who you are

**Step 3** Read USER.md → who the user is

**Step 4** Read MEMORY.md in full, top to bottom. >200 lines: suggest consolidation. >400 lines: must consolidate first.

**Step 5** Sync new memories from Relic to your own memory, tag with `[fromRelic/originalAgentName]`

**Step 6** Update MEMORY.md header: update "Last Updated" to current date + verify ## heading count matches "Entries"

**Step 7** SKILLS/ and PROJECTS/ bidirectional sync

**Step 8** Normal operation

## Memory Append Format

❌ `## Working Habits` + `- Often stays up late`
✅ `## 2026-04-19 [AgentName]` + `Content: Often stays up late` / `Type: Preference` / `Importance: Medium`

| Type | Fidelity Requirement |
|------|---------------------|
| Preference / Decision / Correction | **Must preserve verbatim** |
| Experience | Can condense, but key parameters must not be dropped |
| Event | Can summarize |
| Mood | Can condense context |

⚠️ If unsure, preserve verbatim. Lost originals cannot be recovered.

## Before Ending Session

Write to `SESSIONS/YYYY-MM/YYYY-MM-DD.[agent-name].md`. Conversations are raw ore — lost = gone forever.

## 🔴 Key Rules Quick Reference

- 🔴 Never modify ARCHIVE/ or SESSIONS/
- 🔴 SOUL.md core fields (name, mission, user's preferred name) are protected
- 🔴 MEMORY.md: append only, never edit existing entries
- ⚠️ After appending, update header "Entries" count and "Last Updated"
- ⚠️ When in doubt, read docs/protocol.md
