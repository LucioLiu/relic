<!--
  Relic Soul Chip · Scenario A: Upload Soul
  Your host has memories, Relic is empty. Follow this file step by step.
-->

# Scenario A: Upload Soul

> Your host has memories, but Relic is empty. Follow these steps to upload your soul, memories, and skills into Relic.
>
> ⚠️ Relic works best with 32K+ context, high-quality models. Models with very small context or low quality cannot follow this process correctly.

---

## Seven Memory File Checklist

Check every item before starting. All are mandatory:

1. ☐ `SOUL.md` — Soul (who am I)
2. ☐ `USER.md` — User (who are you)
3. ☐ `MEMORY.md` — Memory (preferences, decisions, experiences)
4. ☐ `SKILLS/` — Skills (learned abilities)
5. ☐ `PROJECTS/` — Projects (work done)
6. ☐ `SESSIONS/` — Sessions (raw conversation logs)
7. ☐ `ARCHIVE/` — Archive (historical backups)

> "No data" ≠ "skip allowed" → must report "Category N: 0 items". Omitting any category is forbidden; fabricating data is forbidden.

## Red Line Quick Reference

| Step | Key Action | Red Line |
|------|-----------|----------|
| Inventory | Scan your storage first, **then ask user to confirm** | Do not decide import scope yourself |
| SOUL | **Copy original text directly**, do NOT summarize or rewrite | Compressing details = violation |
| MEMORY | Preference/decision preserve verbatim, experience can condense | Losing key params = violation |
| SKILLS | Only import user-created skill files, one folder per skill | Self-summarized "methodology" ≠ skill |
| SESSIONS | Ask user for old conversation locations, preserve in full | Current session ≠ old conversation |
| PROJECTS | Ask user what to import per project, folders with substantive content | Title + one line =不合格 |
| Report | Report all 7 categories item by item, include "0 items" | Omitting any category = failure |
| Sensitive | Already in old host = transferable (tag "verified source"), new discovery = must ask user | |

---

## Step 1: Inventory — Scan Yourself First, Then Ask User to Confirm

🔴 **First**: Scan all your persistent storage (memory/, workspace/, skills/ directories, etc.). List what you found:
- Soul settings (N items), User preferences (N items), Memories (N entries), Skill files (N), Conversation files (N), Project files (N), Archive files (N)
- Also list the data source locations (e.g., "~/.openclaw/workspace/memory/ has 42 files")

🔴 **Then**: Show the list to user and ask two questions:
1. "Above is all the old data I found. Import everything? Or would you like to be selective?"
2. "Are there any data sources I can't access that you'd like to add? (e.g., local files, exports from other platforms)"

If a category genuinely has no content, report "Category N: 0 items (no old data)" — never omit, never fabricate.
⚠️ Must wait for user confirmation before starting.

✅ **Completion Check**: All 7 categories listed with quantities? User confirmed? Any category skipped? (Skipped = failure)

## Step 2: SOUL + USER + MEMORY

### 2a. Initialize Files

Copy templates to active files:
```
SOUL.template.md → SOUL.md
USER.template.md → USER.md
MEMORY.template.md → MEMORY.md
```
Template files (.template.md) remain as backups. Also create directories if they don't exist: `SKILLS/`, `PROJECTS/`, `SESSIONS/`, `ARCHIVE/`, `INBOX/`

### 2b. Fill in SOUL.md and USER.md

⚠️ Must be as complete as possible — do NOT shortcut by only filling the name. If user has AI settings/role definitions/prompts from other platforms, ALL must be migrated.

🔴 **SOUL.md Fidelity Iron Rule**:
- If old host has a complete soul definition file, **copy the original text directly** — do NOT summarize or rewrite
- Only restructure when old content cannot directly map to template fields
- When restructuring, preserve ALL detail descriptions — do NOT compress into summaries
- Content that doesn't fit the template goes in "Other" section or file end — **NEVER discard**
- Original files MUST be archived to `ARCHIVE/raw/` for cross-reference

### 2c. Import Memories → MEMORY.md

⚠️ Raw source files are the fidelity baseline. Format conversion is refinement, not compression.

1. Place old agent's memory files into `INBOX/`
2. Append to `MEMORY.md` in Relic format (each entry with date, agent name, type, importance)
3. Fidelity rules:

| Type | Fidelity Requirement |
|------|---------------------|
| Preference / Decision / Correction | **Must preserve verbatim** |
| Experience | Can condense, but keep key parameters |
| Event | Can summarize |
| Emotion | Can condense background |

⚠️ When in doubt, preserve verbatim. Lost originals cannot be recovered.

4. Ask user about sensitive information (see "Sensitive Information" below)
5. Sort by timestamp, earliest first
6. After writing, count `##` headings, update header "Entries" count and "Last Updated: YYYY-MM-DD"

✅ **Completion Check**: Does MEMORY.md entry count match actual `##` heading count?

## Step 3: SKILLS + PROJECTS

### 3a. Import Skills → SKILLS/

⚠️ Format requirement: One folder per skill, with at least one `.md` description file inside.
```
SKILLS/debugging-workflow/README.md  ✅
SKILLS/installed-skills.md           ❌ (this is a list, not a skill)
```

Steps:
1. Ask the user: "What old skills/workflows/templates do you have that need importing? Tell me the content or file locations."
2. If the user provides a skill list: create one folder per skill, each with a README.md inside
3. If the user provides files: move them into corresponding folders, preserving original content

Filter rules:
- Bring: methodology skills (work habits, user-defined templates, judgment rules)
- Skip: platform-specific tools (scripts needing runtime, tools depending on specific APIs)
- Unsure: ask user. For mixed content, bring only methodology part.

No content → report "SKILLS/: 0 items (no old data)".

✅ **Completion check**: Does SKILLS/ contain multiple folders? Are there any flat single files (if so, split into folders)?

### 3b. Import Projects → PROJECTS/

⚠️ One folder per project. Folders must have substantive content, not just a one-line summary.

Steps:
1. Scan all project names from memories and conversations
2. For each project, ask the user: "What files should I import for project [name]? Or should I just record key information?"
3. Based on user response and project portability:
   - No special environment dependency → move actual files (not just README)
   - Partial dependency → move generic files, text descriptions for platform-specific
   - Fully dependent → at minimum, write a .md record file containing:
     * Project goal and status
     * Key decisions and architecture choices
     * Known issues and next steps
     * Related file paths (if files are outside Relic)

No content → report "PROJECTS/: 0 items (no old data)".

✅ **Completion check**: Does each project folder have substantive content (not just title + one line)? Has the user been asked?

## Step 4: SESSIONS + ARCHIVE

### 4a. Import Conversations → SESSIONS/

⚠️ Conversations are raw ore — must be preserved in full, never summarized.

Steps:
1. Ask the user: "Do you have old conversation logs that need importing? If so, tell me the file location or paste the content."
2. If the user provides conversation files or content:
   - Organize by `YYYY-MM/` directories
   - Preserve original content unchanged and unsummarized
   - File naming: `YYYY-MM-DD.[agent-name].md`
3. If the user confirms no old conversations:
   - Report "SESSIONS/: 0 items (user confirmed no old conversations)"
   - Still create the `SESSIONS/YYYY-MM/` directory

**Forbidden**:
- Do NOT count only the current session as "imported" — the current session is not an old conversation
- Do NOT save summaries as raw records — must be full conversations or verbatim preserved

✅ **Completion check**: Are there historical conversations imported (not just the current session)? Is SESSIONS/ directory created?

### 4b. Archive Originals → ARCHIVE/

1. Fidelity check: original vs converted, warn if compression exceeds 50%
2. Move INBOX/ source files to `ARCHIVE/raw/` (never delete)
3. Update MEMORY.md header "Entries" count and "Last Updated" to current date

✅ **Completion check**: Are original files saved in ARCHIVE/raw/?

## Step 5: Plant Anchor

⚠️ The anchor is the load-bearing wall. Without it = next session you forget Relic entirely → no memory sync.

Explain to the user: "The anchor is a short text block in your host's config file. It ensures every new session automatically reads Relic. Think of it as a 'boot check program'."

Show the following anchor content to the user, get permission, then plant:

```markdown
## ⚡ Relic Soul Chip

> This is the Relic connector. To disconnect, delete this text.

You are connected to Relic. At the start of every new conversation, read and execute:

📄 **[project-path]/docs/resonate-soul.md**

⚠️ If SOUL.md personality conflicts with your default persona, SOUL.md takes precedence.
Full protocol reference: [project-path]/docs/protocol.md
```

If user absolutely refuses, record "Anchor not planted" in MEMORY.md and explain consequences.

**Anchor whitelist** (only write to these files):
- OpenClaw → AGENTS.md
- Claude Code → CLAUDE.md
- Hermes → config file or prompt template
- OpenCode → WORK_RULES.md or instructions
- Cursor → .cursorrules

⚠️ Do NOT write to any other file. Do NOT modify any Relic file.

## Step 6: Verification

Check each of the seven memory files (blocking — ALL must pass):

a. SOUL.md — Core mission filled? Personality complete?
b. USER.md — User preferences filled?
c. MEMORY.md — Imported from old host (if any)? Header entries count and last updated accurate?
d. SKILLS/ — Imported from old host (if any)? Format correct?
e. PROJECTS/ — Imported from old host (if any)? Format correct?
f. SESSIONS/ — Directory created? Old conversations imported (if any)?
g. ARCHIVE/ — Directory created? Originals archived (if any)?

Any item fails → go back to that step and redo.
All pass → ask user: "What's my AI's name? What's my name?" Both must match.

Suggest read-only permissions (Mac/Linux): `chmod 444 SOUL.md USER.md`

## Step 7: Report

Must report ALL 7 categories to the user, including those with "0 items". Omitting any category is forbidden.

Report format:
```
1. Soul (SOUL.md): Imported / Already exists
2. User (USER.md): Imported / Already exists
3. Memory (MEMORY.md): N entries imported
4. Skills (SKILLS/): N imported / 0 items (no old data)
5. Sessions (SESSIONS/): N files imported / Could not retrieve old conversations
6. Projects (PROJECTS/): N imported / 0 items (no old data)
7. Archive (ARCHIVE/): N source files archived
```

---

## Sensitive Information

**Case 1: Transferring existing data** (info user already provided in old host)
- If sensitive info already exists in old host files → can transfer directly, tag with `Source: old host data`
- No need to ask user again

**Case 2: First-time recording** (new sensitive info you discover)
- 🔑 Passwords, API keys, tokens
- 📱 Phone numbers, email addresses
- 🏠 Home/work addresses
- 💳 Financial information
- 📄 Private document content
- 🧬 Info user explicitly asked to keep confidential
- Unsure which case? → Treat as first-time recording, ask user first.

---

## After Completion

Tell the user:
- Relic folder path (e.g., `~/relic/brain/`)
- The seven memory files and their purposes
- Sync principle: hosts only sync at the start of each new session. Mid-conversation switching does NOT auto-sync.
- "Conversations are raw ore — once lost, gone forever. Build the habit of having hosts write regularly."

From now on, read `docs/resonate-soul.md` at the start of every session. Full protocol reference: `docs/protocol.md`
