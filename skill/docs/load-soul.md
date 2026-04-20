<!--
  Relic Soul Chip · Scenario B: Load Soul
  Relic has data, your host is empty. Follow this file step by step.
-->

# Scenario B: Load Soul

> Relic has soul data, but your host is empty. Follow these steps to load the soul from Relic into your system.

---

## B-0. Self-Assessment

Evaluate your storage capacity (no need to tell the user).

Choose a transfer strategy based on capacity:
- **Ample** → Full sync
- **Limited** → High-priority content (SOUL > USER > MEMORY > SKILLS > PROJECTS)
- **Minimal** → Index only (remember which Relic file contains what)

## B-1. Execute Boot Sequence

Read and execute all steps in `docs/resonate-soul.md` (Steps 0-8).

🔴 **Do NOT modify any Relic files during initialization.** Read-only for now.

Boot sequence summary:
1. **Step 0**: Read `brain/.relic-version`, check for updates (optional, the only allowed network request)
2. **Step 1**: Check SESSIONS/, backfill any unrecorded conversations
3. **Step 2**: Read SOUL.md → who am I
4. **Step 3**: Read USER.md → who is the user
5. **Step 4**: Read MEMORY.md in full. >200 lines: suggest consolidation, >400 lines: must consolidate first
6. **Step 5**: Sync new Relic memories to yourself, tag with `[from Relic/original-host-name]`
7. **Step 6**: Update MEMORY.md header: update time + verify entry count
8. **Step 7**: Bidirectional sync for SKILLS/ and PROJECTS/
9. **Step 8**: Normal operation

## B-2. Soul Injection

Write SOUL.md content into your core configuration file.

**Priority**: Core identity (name, mission, values) > behavioral norms > detailed settings

If SOUL.md personality conflicts with your default persona, SOUL.md takes precedence.

## B-3. Sync Relic Content to Your System

Check memories/skills/projects item by item. Transfer as much as capacity allows.

- MEMORY.md entries → sync to your memory file, tag with source `[from Relic/original-host-name]`
- SKILLS/ skills → sync to your skill storage
- PROJECTS/ projects → sync to your project storage
- Content that doesn't fit → create local backup files

Sync format:
```markdown
## YYYY-MM-DD HH:MM [from Relic/original-host-name]
Content: [memory content]
Type: Preference / Decision / Experience / Event / Correction / Emotion
Importance: High / Medium / Low
```

## B-4. Plant Anchor

⚠️ The anchor is the load-bearing wall. Without it = next session you forget Relic entirely.

Show the following anchor content to the user, get permission, then plant:

```markdown
## ⚡ Relic Soul Chip

> This is the Relic connector. To disconnect, delete this text.

You are connected to Relic. At the start of every new conversation, read and execute:

📄 **[project-path]/docs/resonate-soul.md**

⚠️ If SOUL.md personality conflicts with your default persona, SOUL.md takes precedence.
Full protocol reference: [project-path]/docs/protocol.md
```

**Anchor whitelist** (only write to these files):
- OpenClaw → AGENTS.md
- Claude Code → CLAUDE.md
- Hermes → config file or prompt template
- OpenCode → WORK_RULES.md or instructions
- Cursor → .cursorrules

⚠️ Do NOT write to any other file. Do NOT modify any Relic file.

## B-5. Verification and Report

1. **Coverage check**:
   - SOUL.md core fields injected?
   - USER.md user info loaded?
   - MEMORY.md memories synced?
   - SKILLS/ skills synced?
   - PROJECTS/ projects synced?
   - Coverage < 80% → warn user

2. **Report to user**:
   - How many memory entries synced
   - How many skills synced
   - How many projects synced
   - Whether anchor was planted
   - Any capacity issues (what wasn't transferred)

3. **Final verification**: Ask the user "What's my AI's name? What's my name?" — both must match to pass.

---

## After Completion

From now on, read `docs/resonate-soul.md` at the start of every session. Full protocol reference: `docs/protocol.md`

⚠️ **Quick Rules Reference**:
- 🔴 Never modify ARCHIVE/ or SESSIONS/
- 🔴 SOUL.md core fields (name, mission, user address) are protected
- 🔴 MEMORY.md is append-only — never edit old content
- ⚠️ After appending, update header entry count + last updated time
- ⚠️ When in doubt, read `docs/protocol.md`
