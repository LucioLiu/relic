<!--
  Relic Soul Chip · Import Execution Guide
  Author: LucioLiu · https://github.com/LucioLiu/relic
  License: GPL v3
  Format version: 1.2.0
-->

# Import Execution Guide

## ⚡ Import Iron Rules

> 🔴 **Seven memory file categories — ALL mandatory:**
> 1.`SOUL.md` 2.`USER.md` 3.`MEMORY.md` 4.`SKILLS/` 5.`PROJECTS/` 6.`SESSIONS/` 7.`ARCHIVE/`
>
> - Must process ALL 7 categories, even empty ones must be reported
> - "No data" ≠ "can skip" → must report "Category N: 0 items"
> - Omitting any category is forbidden; fabricating data is forbidden

## 📋 Mandatory: Output Plan Before Execution

Before importing, you **MUST** output the following plan and wait for user confirmation:

```
Import Plan:
- SOUL.md: [action]
- USER.md: [action]
- MEMORY.md: [action]
- SKILLS/: [action]
- PROJECTS/: [action]
- SESSIONS/: [action]
- ARCHIVE/: [action]
```

## Step 1: Scan + Confirm

Scan all persistent storage, list items by category. Ask the user two questions:
1. "Import everything listed above? Or selective import?"
2. "Are there any data sources I missed?"

⚠️ Must wait for user confirmation before starting.

❌ `I didn't find any old data.`
✅ `Scan: Soul 2 files | Memory 42 entries | Skills 3 | Conversations 0 | Projects 5 | Archive 8. Import all of the above?`

## Step 2: SOUL + USER

🔴 **Fidelity Iron Rule: Copy original text directly, do NOT summarize or rewrite.** If the template can't fit everything, put overflow in "Other" section — **NEVER discard**. Archive originals to `ARCHIVE/raw/`.

❌ `User preference: likes concise code style` ← compressed rewrite
✅ `User preference: code style favors functional over OOP, dislikes Spring ecosystem, naming forbids pinyin abbreviations` ← verbatim retention

## Step 3: MEMORY

❌ `## Working Habits` + `- Often stays up late` ← using category names as headings
✅ `## 2026-04-19 [OpenClaw-Chang]` + `Content: Often stays up late...` / `Type: Preference` / `Importance: Medium` ← using date + agent name

| Type | Fidelity Requirement |
|------|---------------------|
| Preference / Decision / Correction | **Must preserve verbatim** |
| Experience | Can condense, but key parameters/paths must not be dropped |
| Event | Can summarize |
| Mood | Can condense context |

Sensitive info: Already in old host → can migrate (tag "verified source") | Newly discovered passwords/phone numbers → **MUST ask user first**
After writing: count `##` headings, update header "Entries" and "Last Updated".

## Step 4: SKILLS

One folder per skill, with at least one `.md` inside. Only bring user-created skill files and documented methodologies. Do NOT bring conversation experience or AI-summarized methodology.

❌ `SKILLS/skills-list.md` ← flat list
✅ `SKILLS/debugging-workflow/README.md` ← folder structure

## Step 5: SESSIONS

Ask user for old conversation locations. Save in full, never summarize. Current session ≠ old conversation.
No old conversations → report "0 items (user confirmed no old conversations)", still create `SESSIONS/YYYY-MM/` directory.

## Step 6: PROJECTS

Ask user per project what to import. One folder per project with substantive content.

❌ `PROJECTS/my-app/README.md` → "This is my project" ← one line
✅ `PROJECTS/my-app/` containing README.md + api-design.md + notes.md ← substantive content

## Step 7: Archive + Report

`INBOX/` → `ARCHIVE/raw/`. **Must report ALL 7 categories item by item** (including "0 items"):

```
1. SOUL.md: imported  2. USER.md: imported  3. MEMORY.md: N entries
4. SKILLS/: N skills  5. SESSIONS/: N sessions  6. PROJECTS/: N projects  7. ARCHIVE/: N files archived
```
Omitting any category = failure.

## 🔴 Final Self-Check

Seven categories: SOUL.md, USER.md, MEMORY.md, SKILLS/, PROJECTS/, SESSIONS/, ARCHIVE/

- ☐ Processed ALL 7 categories?
- ☐ MEMORY format is `## date [agent-name]`? (`## category-name` = ❌)
- ☐ SKILLS are folders? (single flat .md = ❌)
- ☐ Asked user about old conversation locations?
- ☐ Asked user what to import per project?
- ☐ All 7 categories appear in the report?

## Plant Anchor

After import, plant an anchor in the agent's config file pointing to BOOT.md:

```markdown
## ⚡ Relic Soul Chip
> This is the Relic connector. To disconnect, delete this text.
You are connected to the Relic Soul Chip. At the start of every new session, read and execute:
📄 **[brain-path]/BOOT.md**
⚠️ First time connecting? → Read [brain-path]/IMPORT.md
⚠️ If SOUL.md personality conflicts with your default, follow SOUL.md.
Full protocol: [brain-path]/PROTOCOL.md
```

Whitelist: OpenClaw→AGENTS.md | Claude Code→CLAUDE.md | Hermes→config file | OpenCode→WORK_RULES | Cursor→.cursorrules. Must get user permission before planting.

See PROTOCOL.md for detailed rules
