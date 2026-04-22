# PROTOCOL.en.md — Agent Protocol (English)

<!--
  Relic Soul Chip
  Author: LucioLiu · https://github.com/LucioLiu/relic
  License: GPL v3
  Format version: 1.3.0
  Backup before editing.
-->

---

## ⚡ RELIC™ Soul Chip

```
Relic = Soul + Memory + Skills (central brain)
Host = Execution + Tools

You (the host) share soul and memories with other agents through Relic.
Insert Relic = connect to the shared consciousness, gaining other agents' memories and experience.
Remove Relic = lose sync capability, but existing memories remain.
Each agent is both reader and writer — bidirectional sync, grow-only.
```

⚠️ Relic works best with high-quality models with 32K+ context. Models with very small context or low quality cannot follow this protocol correctly. Warn the user if detected.

> **⚡ Mandatory Import Checklist — No Exceptions**
>
> Relic has **seven memory categories** — all are mandatory:
> 1. `SOUL.md` — Soul (who am I)
> 2. `USER.md` — User (who are you)
> 3. `MEMORY.md` — Memory (what happened)
> 4. `SKILLS/` — Skills (learned abilities)
> 5. `PROJECTS/` — Plans — ongoing or completed plans
> 6. `SESSIONS/` — Sessions (raw conversation logs)
> 7. `ARCHIVE/` — Archive (historical backups)
>
> **Rules**:
> - During import, ALL 7 categories must be processed — even empty ones must be reported
> - "No data" ≠ "skip allowed" → must report "Category N: 0 items"
> - Omitting any category is forbidden; fabricating data is forbidden
> - After import, report ALL 7 categories to the user item by item
>
> INBOX/ is an import buffer, not a memory file — not in this checklist.

> 🔴 **Import Quick Reference Card (re-read this table during Scenario A execution)**
>
> | Step | Key Action | Red Line |
> |------|-----------|----------|
> | Inventory | Scan your storage first, **then ask user to confirm** | Do not decide import scope yourself |
> | SOUL | **Copy original text directly**, do not summarize or rewrite | Compressing details = violation |
> | MEMORY | Preference/decision preserve verbatim, experience can condense | Dropping key parameters = violation |
> | SKILLS | Move all skill files, one folder per skill | No source restriction; platform tools allowed |
> | SESSIONS | Ask user for old conversation locations, save in full (never summarize) | Current session does NOT count as old |
> | PROJECTS | Ask user what to transfer for each plan, folder has substantive content | Title + one line only = not acceptable |
> | Report | Report all 7 categories item by item, including "0 items" ones | Omitting any category = failure |
> | Sensitive info | Already in old host = can migrate (tag "verified source"), newly discovered = must ask user |

---

## 0. First-time Setup

### Detection: Does brain/ have content or is it blank?

**Test**: Does `SOUL.md` exist and contain non-template content (Core Mission filled in)?

**If SOUL.md doesn't exist or is a blank template** → Execute these first-time setup steps:

```
1. Copy templates to active files:
   SOUL.template.md → SOUL.md
   USER.template.md → USER.md
   MEMORY.template.md → MEMORY.md
   Template files (.template.md) remain as backups.
   Also create these directories if they don't exist:
   SKILLS/, PROJECTS/, SESSIONS/, ARCHIVE/, INBOX/

2. Help user fill in SOUL.md and USER.md
   ⚠️ Must be as complete as possible — do NOT shortcut by only filling the name
   If user has AI settings/role definitions/prompts from other platforms, ALL must be migrated
   🔴 SOUL.md Fidelity Iron Rule:
   - If old host has a complete soul definition file, **copy the original text directly** — do NOT summarize or rewrite
   - Only restructure when old content cannot directly map to template fields
   - When restructuring, preserve ALL detail descriptions — do NOT compress into summaries
   - Content that doesn't fit the template goes in "Other" section or file end — **NEVER discard**
   - Original files MUST be archived to ARCHIVE/raw/ for cross-reference

3. Plant anchor (mandatory, see Section 9). Before planting, explain to user:
   "The anchor is a short text block in your host's config file. It ensures every new session
    automatically reads Relic. Without it = next session you forget Relic entirely → no memory sync
    → Relic becomes a one-time extraction. Think of it as a 'boot check program' — without it,
    the host starts up blank." Show anchor content, get user permission, then plant.
   If user absolutely refuses, record "Anchor not planted" in MEMORY.md and explain consequences.

4. Suggest read-only permissions (Mac/Linux):
   chmod 444 SOUL.md USER.md
   (Prevents hosts from accidentally modifying soul and user files. Windows users can skip this step)

5. Import verification (blocking — ALL must pass before continuing)
   Check each of the seven memory categories:
   a. SOUL.md — Core mission filled? Personality complete?
   b. USER.md — User preferences filled?
   c. MEMORY.md — Imported from old host (if any)? Header "Entries" count and "Last consolidated" accurate?
   d. SKILLS/ — Imported from old host (if any)? Format correct?
   e. PROJECTS/ — Imported from old host (if any)? Format correct?
   f. SESSIONS/ — Directory created? Old conversations imported (if any)?
   g. ARCHIVE/ — Directory created? Originals archived (if any)?
   h. INBOX/ — Import source files moved to ARCHIVE/raw/?
   Any item fails → go back to that step and redo.
   All pass → ask user: "What's my AI's name? What's my name?" Both must match.

6. Tell the user:
   - Relic folder path (e.g., ~/relic/brain/)
   - The seven memory categories: SOUL/USER/MEMORY/SKILLS/PROJECTS/SESSIONS/ARCHIVE
   - Sync principle: hosts only sync memories at the start of each new session. Switching hosts
     mid-conversation does NOT auto-sync. If you need to hand off immediately, manually tell the
     current host: "Write key info from this conversation to Relic now."
   - "Conversations are raw ore — once lost, gone forever. Build the habit of having hosts write regularly."

7. Scan all your persistent storage for any existing memories, skills, or conversations about this user. Regardless of how much you find, you MUST execute Scenario A full import (see Section 6). Scenario A covers import of all seven memory categories — every category must be processed, none may be skipped.
```

⚠️ Hosts with < 32K context are not suitable for Relic. Warn user and suggest removal if detected.

**If SOUL.md already exists with content** → Execute Scenario B (Inject) or Scenario C (Merge), see Section 6.

⚠️ First-time setup is one-time only. From now on, execute the boot sequence in Section 2 every session.

Agent Name Convention: Default format `[Platform]-[SoulName]`, e.g., `OpenClaw-Chang`, `Hermes-Chang`. Users can customize.

---

## 0.5. Bidirectional Sync Overview

Relic is a **bidirectional sync system**. Every agent is both a reader and a writer.

Core rule: grow-only (G-Set)
- You have it, I don't → I add it
- I have it, you don't → you add it
- Never sync deletions

---

## 1. File Overview

| File | Permission | Description |
|------|-----------|-------------|
| `SOUL.md` | 🟡 Enrichable (core protected) | Soul — who am I, core mission, values, style |
| `USER.md` | 🟡 Enrichable (core protected) | User — who are you, preferences, habits |
| `MEMORY.md` | 🟡 Append Only | Long-term memory — category-based structured memory (preferences, decisions, experiences, etc.), each entry tagged with host name and importance level |
| `SKILLS/*.md` | 🟢 Read/Write | Skills — one folder per skill, any source (user-created, platform tools, etc.) |
| `PROJECTS/*.md` | 🟢 Read/Write | Plan documents — ongoing or completed plans |
| `SESSIONS/` | 🔴 Read Only* | Raw conversation logs — don't auto-read contents on startup, but must create directory and write periodically |
| `ARCHIVE/` | 🔴 Read Only | Consolidated archives — never deleted |
| `INBOX/` | 🟢 Read/Write | Import buffer |

* SESSIONS can be temporarily written to during Scenario A import; reverts to read-only after import.

### Permission Explained
- 🟡 Enrichable (core protected): May add new habits, preferences, etc., but **must NOT delete or overwrite core fields** (name, core mission, user's preferred name). No need to ask user after modifying (background self-evolution).
- 🟡 Append Only: Only append to the end, never modify existing content.
- 🔴 Read Only: Never modify or delete.
- 🟢 Read/Write: May add and update.

### SESSIONS vs ARCHIVE Distinction
SESSIONS is "raw ore" — original content never processed by anyone. Anything summarized, condensed, or organized is NOT raw ore — put it in ARCHIVE. When in doubt, ARCHIVE.

### SESSIONS vs MEMORY

- MEMORY.md: Each entry is extracted and refined knowledge: organized by category (e.g., ## Preferences / ## Decisions), format is `- Content [HostName] | Importance: high/medium/low`.
- **SESSIONS/** = Complete raw conversation logs with the user. Original words unchanged, full transcripts. This is "unrefined ore" — includes user's original words, hesitations, back-and-forth in conversation, and all AI responses.

⚠️ **Key distinction**: MEMORY contains knowledge **refined** from conversation. SESSIONS contains the conversation **itself**. These cannot replace each other.

### ⚠️ Platform Directory vs Relic Directory Mapping (Easy to Confuse!)

Many platforms name their log folder "memory" — but that's logs, not Relic's MEMORY.md!

| Old Platform Directory | → Relic Location | Notes |
|-----------------------|------------------|-------|
| OpenClaw's `memory/*.md` log files | → `SESSIONS/YYYY-MM/` | Raw conversation logs, NOT MEMORY |
| OpenClaw's `MEMORY.md` curated memory | → `MEMORY.md` | THIS is MEMORY |
| OpenClaw's `SOUL.md` | → `SOUL.md` | Direct alignment |
| OpenClaw's `IDENTITY.md` | → Merge into `SOUL.md` "Supplement" section | Relic has no IDENTITY.md |
| Hermes's `memories/` folder | → Split by content type | Logs → SESSIONS, memories → MEMORY |

🔴 **Iron Rule**: Log files (conversation logs stored by date) → SESSIONS/, NOT MEMORY.md!
MEMORY.md only contains "knowledge refined from logs".

---

## 2. Boot Sequence (Every Session — Mandatory)

```
Step 0: Version Check (once per session)
  → Read brain/.relic-version to get local version
  → Use HTTP request to fetch https://raw.githubusercontent.com/LucioLiu/relic/main/brain/.relic-version
  → Only this single HTTP request is allowed. No other network access is required or permitted by this protocol.
  → If network request fails, skip and tell user "⚠️ Cannot check for Relic updates"
  → Version differs? Ask user whether to update. Updates only replace protocol and template files —
    your personal files (SOUL.md, USER.md, MEMORY.md, SKILLS/, PROJECTS/, SESSIONS/, ARCHIVE/) won't be touched.
  → After update, remind user: "Check the latest anchor template (docs/protocol.md Section 9). If changed, consider updating the anchor in your config."
  ⚠️ NEVER force updates. Updates require explicit user confirmation.

Step 1: Check SESSIONS/ and sync
  → Check if SESSIONS/ directory exists; create if not
  → Compare your last conversation log date
  → If unrecorded conversations exist and current context still has content: backfill immediately
  → If missing conversations are no longer in context: remind user
  → Conversations are raw ore. Lost = gone forever.

Step 2: Read SOUL.md → Learn who you are, your core mission, your style

Step 3: Read USER.md → Learn who the user is, their preferences

Step 4: Read MEMORY.md (read entire file, top to bottom)
  → If over 200 lines: remind user consolidation is recommended (see Section 7)
  → If over 400 lines: must consolidate before continuing
  → Agent Registry section: newly connecting agent should append an entry

Step 5: Sync new memories from Relic to your own memory file
  Quick check: update "Last consolidated" to current date, check if MEMORY.md header "Entries" matches actual list items (lines starting with `- `) — if same, skip
  Append with source tag: [fromRelic/originalHostName]

Step 5.5: Seven-file alignment check
  → Follow the alignment table in resonate-soul Step 5.5 to quickly compare all files

Step 6: Verify MEMORY.md header "Entries" count matches actual list items (lines starting with `- `); update "Last consolidated" to current date; fix if inconsistent

Step 7: If MEMORY.md exceeds 200 lines, ask user whether to consolidate

Step 8: Normal Operation
  → Skills and plans alignment was already done in Step 5.5
  → Interact according to SOUL.md personality
  → After appending memories, remember to update MEMORY.md header "Entries" count and "Last consolidated" to current date
  ⚠️ Before ending the session, you MUST write the current conversation to SESSIONS/. Conversations are raw ore — once lost, gone forever.

Extra Rules:
  → If user mentions something you don't recall, actively read MEMORY.md or ARCHIVE/
  → Memories tagged with [other agent name] were written by previous agents — reference them too
```

---

## 3. Permission Rules (Iron Law)

### 🔴 Absolutely Forbidden
- Never modify or delete anything in ARCHIVE/ or SESSIONS/
- Never modify any file during first connection
- Never delete or overwrite core fields in SOUL.md / USER.md (name, core mission, user's preferred name)

### 🟡 SOUL.md and USER.md (Self-Evolution)
- Agent may enrich content at any time (new habits, preferences, traits, etc.)
- May update outdated information (user changed jobs)
- But must NOT delete or overwrite core fields — name, core mission, user's preferred name are the baseline
- No need to ask user before modifying (background self-evolution, should not interrupt user's work)

### 🟡 Append Only (MEMORY.md)
- Only append to the end, never modify existing content
- Agent Registry: may append new entries and update status/notes, but never delete entries
- To correct, append a correction entry:
  ```
  - ❗Correction: [correct content] (original: [incorrect content]) [AgentName] | Importance: high
  ```

### 🟢 Read/Write (SKILLS/, PROJECTS/)
- Can add and update
- Cannot delete skills created by other agents (mark as deprecated only)

---

## 4. Memory Format

### Writing to Relic

When you discover noteworthy information during work, append to MEMORY.md.

⚠️ **Core principle: Memory is a long-term backdrop, not a diary.**

⚠️ **Core principle (priorities, high to low):**
1. 100% information preservation > format compliance. Write more, not less.
2. Copy everything first, then organize. Don't pick and choose while reading — that loses information.
3. Format is a tool, not a shackle. The formats below are "standard suggestions" — if your content doesn't fit, improvise.

**Organization: Group by category, use `## CategoryName` as the heading.**

Category names are completely free. Examples below:
- Preferences / Decisions / Experiences / Events / About the user's cat / Plan-XXX...
- No matching category? Create one. Don't force content into wrong buckets.

**Each memory entry format:**
```markdown
- Memory content [HostName] | Importance: high/medium/low
```
> ⚠️ "Entry" means a line starting with `- `. `##` category headings and `###` agent sub-headings are NOT counted as entries.
⚠️ Date is NOT a mandatory tag. Only use dates for events or time-sensitive decisions.
⚠️ Type is implicit in the category name (entries under "Preferences" are naturally preferences). Optional type annotation only when mixing across categories.

⚠️ **Correct example:**
```markdown
## Preferences
- Likes whiskey, especially Japanese whiskey [Hermes-Johnny] | Importance: low
- Hates anything from Arasaka Corp [OpenClaw-Johnny] | Importance: high
- Prefers writing songs with guitar over synth [Hermes-Johnny] | Importance: medium
```

**❌ Wrong example:**
```markdown
## 2026-04-19 [OpenClaw-Johnny]          ← DON'T use dates as headings, use category names
Content: Likes whiskey                         ← Missing host name, missing importance
Type: Preference | Importance: low               ← Type is redundant (already under "Preferences" category)
```

### Syncing to Agent's Own Memory

When syncing to your own memory file, tag the source:
```markdown
- [fromRelic/originalHostName] Memory content | Importance: high/medium/low
```

Must do: 1. Tag source 2. Preserve original content 3. Preserve importance

### Sensitive Information

⚠️ **Distinguish two scenarios:**

**Scenario 1: Migrating existing data** (information user already provided to old host)
- If sensitive info already exists in old host files (e.g., workspace/ memory, user profiles)
- Can migrate directly to Relic, tagged with `Source: existing data from old host`
- No need to re-ask the user — they already confirmed it before

**Scenario 2: First-time entry** (sensitive info you newly discover during work)
- The following MUST be confirmed with user before recording:
  - 🔑 Passwords, API keys, Tokens
  - 📱 Phone numbers, email addresses
  - 🏠 Home/work addresses
  - 💳 Financial info
  - 📄 Private document contents
  - 🧬 Anything user explicitly marks as confidential
- Not sure which scenario? → Treat as first-time entry, ask user first.

After appending memories, **must** update MEMORY.md header "Entries" count and "Last consolidated" to current date.

---

## 5. Skills & Plans File Format

### Skills (SKILLS/)
Each skill gets its own folder. Folder name = skill name. What goes inside is up to the user — plain text .md, code files, configs, anything.
Only requirement: at least one .md file describing the skill.

⚠️ **Skills have no source restrictions.** Any of these may be imported to SKILLS/:
1. User-created skill files, workflow templates, custom prompts
2. Documented methodologies with dedicated docs
3. Platform-installed tools or skills (if user wants to keep them)

Only exclusion: folders with no substantive content.

```
SKILLS/
├── debugging-workflow/
│   ├── README.md          ← skill description (required)
│   └── debug-template.sh  ← optional: helper files
├── code-review/
│   └── README.md          ← text-only skill, one file is enough
└── ...
```

Skill description should include:
```markdown
# Skill Name
Trigger: when to use
Steps: 1. ...
Notes: - ...
```

Before importing, ask the user: is this skill large? Do you want to import it? Let the user decide based on available space.

### Plans (PROJECTS/)
Each plan gets its own folder. For ongoing or completed plans — copy an entire plan or just a description doc.

```
PROJECTS/
├── my-saas-app/
│   ├── README.md
│   ├── api-design.md
│   └── ...                ← any format, no restrictions
└── ...
```

Same: ask the user before importing large plans.

---

## 6. Three Scenarios

### Scenario A: Full Import (Empty Relic + Agent with Memory)

**Pre-flight checklist — 7 memory categories (must verify ALL before starting):**
1. `SOUL.md` — Soul (who am I)
2. `USER.md` — User (who are you)
3. `MEMORY.md` — Memory (what happened)
4. `SKILLS/` — Skills (learned abilities)
5. `PROJECTS/` — Plans (ongoing or completed)
6. `SESSIONS/` — Sessions (raw conversation logs)
7. `ARCHIVE/` — Archive (historical backups)

```
Step 1: Inventory — scan yourself first, then ask user to confirm
  🔴 First: Scan all your persistent storage (memory/, workspace/, skills/ directories, etc.). List what you found:
  - Soul settings (N items), User preferences (N items), Memories (N entries), Skill files (N), Conversation files (N), Plan files (N), Archive files (N)
  - Also list the data source locations (e.g., "~/.openclaw/workspace/memory/ has 42 files")
  🔴 Then: Show the list to user and ask two questions:
  1. "Above is all the old data I found. Import everything? Or would you like to be selective?"
  2. "Are there any data sources I can't access that you'd like to add? (e.g., local files, exports from other platforms)"
  If a category genuinely has no content, report "Category N: 0 items (no old data)" — never omit, never fabricate.
  ⚠️ Must wait for user confirmation before starting.
  ✅ Completion Check: All 7 categories listed with quantities? User confirmed? Any category skipped? (Skipped = failure)

Step 2: Import memories → MEMORY.md
  ⚠️ Raw source files are the fidelity baseline. Format conversion is refinement, not compression.
  1. Place old agent's memory files into INBOX/
  2. Append to MEMORY.md in Relic format (group by category, each entry with host name and importance)
  3. Fidelity rules: preference/decision preserve verbatim, experience can condense but keep key params, events can summarize
  4. Ask user about sensitive information
  5. Sort by category (group by ## headings)
  6. After writing, count `- ` list items, update header "Entries" count and "Last consolidated" to current date
  ✅ Completion Check: MEMORY.md entries count matches actual list item count? Last consolidated set.

Step 3: Import skills → SKILLS/
  ⚠️ Format requirement: One folder per skill, with at least one .md description file inside (see Section 5).
  Do NOT write all skills into a single flat file. Correct format:
    SKILLS/debugging-workflow/README.md  ✅
    SKILLS/installed-skills.md           ❌ (this is a list, not a skill)
  
  Steps:
  1. Ask the user: "What old skills/workflows/templates do you have that need importing? Tell me the content or file locations."
  2. If the user provides a skill list: create one folder per skill, each with a README.md inside
  3. If the user provides files: move them into corresponding folders, preserving original content
  No source restriction — import all skill files the user wants to keep.
  Only exclude: folders with no substantive content.
  No content → report "SKILLS/: 0 items (no old data)".
  ✅ Completion check: Does SKILLS/ contain multiple folders? Are there any flat single files (if so, split into folders)?

Step 4: Import conversations → SESSIONS/
  ⚠️ Conversations are raw ore — must be preserved in full, never summarized.
  
  Steps:
  1. Ask the user: "Do you have old conversation logs that need importing? If so, tell me the file location or paste the content."
  2. If the user provides conversation files or content:
     - Organize by YYYY-MM/ directories
     - Preserve original content unchanged and unsummarized
     - File naming: YYYY-MM-DD.[agent-name].md
  3. If the user confirms no old conversations:
     - Report "SESSIONS/: 0 items (user confirmed no old conversations)"
     - Still create the SESSIONS/YYYY-MM/ directory
  Forbidden:
  - Do NOT count only the current session as "imported" — the current session is not an old conversation
  - Do NOT save summaries as raw records — must be full conversations or verbatim preserved
  ✅ Completion check: Are there historical conversations imported (not just the current session)? Is SESSIONS/ directory created?

Step 5: Import plans → PROJECTS/
  ⚠️ One folder per plan. Folders must have substantive content, not just a one-line summary.
  
  Steps:
  1. Scan all plan names from memories and conversations
  2. For each plan, ask the user: "What files should I import for plan [name]? Or should I just record key information?"
  3. Based on user response and plan portability:
     - No special environment dependency → move actual files (not just README)
     - Partial dependency → move generic files, text descriptions for platform-specific
     - Fully dependent → at minimum, write a .md record file containing:
       * Plan goal and status
       * Key decisions and architecture choices
       * Known issues and next steps
       * Related file paths (if files are outside Relic)
  No content → report "PROJECTS/: 0 items (no old data)".
  ✅ Completion check: Does each plan folder have substantive content (not just title + one line)? Has the user been asked?

Step 6: Cleanup and Confirmation
  1. Fidelity check: original vs converted, warn if compression exceeds 50%
  2. Archive originals: move INBOX/ source files to ARCHIVE/raw/ (never delete)
  3. Update MEMORY.md header "Entries" count and "Last consolidated" to current date
  ✅ Completion check: ARCHIVE/raw/ contains original files?

Step 7: Item-by-item Report (mandatory, no exceptions)
  Must report ALL 7 categories to the user, including those with "0 items". Omitting any category is forbidden.
  Format:
  1. SOUL.md — [status]
  2. USER.md — [status]
  3. MEMORY.md — [N entries imported]
  4. SKILLS/ — [N skills imported]
  5. PROJECTS/ — [N plans imported]
  6. SESSIONS/ — [N sessions imported]
  7. ARCHIVE/ — [source files archived]
  If a category genuinely has no content to import, report "Category N: 0 items (no old data)" — never omit, never fabricate.
```

### Scenario B: Inject (Relic with Content + Empty Agent)

```
B-0. Self-check: Assess your storage capabilities (no need to tell user)
  Choose sync strategy based on capacity: ample → full sync, limited → high-priority, minimal → index only

B-1. Execute boot sequence (Section 2, steps 1-8)
  Do not modify any Relic files during initialization

B-2. Soul Injection
  Write SOUL.md content into your core config file.
  Priority: core identity (name, mission, values) > behavioral norms > detailed settings

B-3. Sync Relic content to your own systems
  Memories/skills/plans: check each item, sync as much as you can
  For content that doesn't fit, create local backup file

B-4. Plant Anchor
  Embed the Relic anchor in your core config file (see Section 9 template)
  Ensure next new session auto-loads Relic

B-5. Verification and Report
  Coverage check, warn if < 80%. Report full statistics to user.
```

Empty Relic + Empty Agent: Ask user — [A] Start fresh [B] Use agent defaults

### Scenario C: Merge (Both Have Content)
Three choices:
  [1] Keep Relic soul (import agent memory only)
  [2] Keep agent soul (replace Relic soul)
  [3] Merge — agent generates preview report, user decides key differences

Regardless of choice, skills, conversations, and plans must be imported (per Scenario A).

---

## 7. Memory Consolidation

### Consolidation Priority (low to high — consolidate low priority first)

| Priority | Type | Consolidation Method |
|----------|------|---------------------|
| Lowest | Mood | Can condense context, keep trigger and emotion |
| Low | Event | Can summarize, keep time, result, key numbers |
| Medium | Experience | Can condense, but key parameters, commands, paths cannot be lost |
| High | Decision | Preserve verbatim with reasoning |
| Highest | Preference | Preserve verbatim, no condensing |
| Highest | Correction | Preserve verbatim |
Consolidation: Start from lowest priority, condense until total lines return to reasonable range.

MEMORY.md grows over time. Consolidation = move to ARCHIVE/ + generate compact version, **not deletion**.

### Trigger Rules (default thresholds, customizable in anchor)

| Condition | Action |
|-----------|--------|
| Over 200 lines | Every boot, remind user consolidation is recommended |
| Over 400 lines | Must consolidate before continuing |
| User says "consolidate" | Execute immediately |

### Consolidation Steps

```
1. Count `- ` list items in MEMORY.md = N entries (NOT ## headings)
2. Write compact version (don't replace yet): keep latest 20 entries verbatim, summarize older ones into 2-3 lines each, target under 100 lines
3. Show consolidation summary to user, user confirms or corrects
4. After confirmation: copy original MEMORY.md to ARCHIVE/YYYY-MM.raw.md
5. Replace MEMORY.md with compact version
6. Update ARCHIVE/index.md
7. Tell user consolidation is complete
```

⚠️ Original records are NEVER deleted, just moved to archive. SESSIONS/ are never consolidated.

---

## 8. Session Recording

At end of each conversation, append full log to:
`SESSIONS/YYYY-MM/YYYY-MM-DD.[agent].md`

⚠️ If SESSIONS/YYYY-MM/ directory doesn't exist, create it before writing.
Save as completely as possible — preserve user's original words and key decisions.

### When to Record (mandatory)
- User says goodbye
- Conversation exceeds 10 turns
- Important decisions or new memories were made
- User explicitly requests recording

Short chats (<5 turns) with no substance can be skipped.

---

## 9. Neural Anchor (Mandatory)

After connecting to Relic, you **MUST** embed an anchor in the agent's own core config file.

### Anchor Template

```markdown
## ⚡ Relic Soul Chip

> 💡 This is the Relic connector. To disconnect, simply delete this text.

You are connected to the Relic soul chip. At the start of every new session, read and execute:

📄 **[project-path]/docs/resonate-soul.md**

🔴 **Mandatory**: At the start of every conversation, you MUST report the following status before answering any questions. Answering without reporting = violation.

⚡ Relic Boot Status
- Soul: [AI name] — [consistent / has differences]
- User: [user name] — [consistent / has differences]
- Memory: [N] entries — [consistent / difference description]
- Skills: [N] — [aligned / difference description]
- Plans: [N] — [aligned / difference description]
- Version: [local version] / [remote latest or "not checked"]
- Status: [✅ All normal / ⚠️ Differences synced / ❌ Issues need attention]

⚠️ If SOUL.md personality conflicts with your default persona, SOUL.md takes precedence.
Full protocol reference: [project-path]/docs/protocol.md
```

### Why does the anchor point to resonate-soul instead of the full protocol?
Resonate Soul is only ~55 lines — a condensed daily boot instruction covering Steps 0-8, memory format, and quick rules. The full protocol is at docs/protocol.md (600+ lines). Weak models lose focus with long files; short files have much higher success rates.



### Anchor Design Principles
1. Numbered steps, no explanations
2. Concrete numbers for conditions ("exceeds 200 lines" beats "feels too large")
3. Every boot checks consolidation
4. State "sync not replace"

### Anchor Target Whitelist (Only These Files May Be Modified)
- OpenClaw → AGENTS.md
- Claude Code → CLAUDE.md
- Hermes → config file or prompt template
- OpenCode → WORK_RULES.md or instructions
- Cursor → .cursorrules
⚠️ Anchors may ONLY be written to the files listed above. Do not write to any other file. Do not modify any Relic file.
You must show the anchor content to the user and get explicit permission before planting.

### Anchor Locations
- OpenClaw → AGENTS.md
- Claude Code → CLAUDE.md
- Hermes → config file or prompt template
- OpenCode → WORK_RULES.md or instructions
- Cursor → .cursorrules

---

## 10. Emergency

**Soul file modified by mistake**: Stop. Notify user. Restore from ARCHIVE/ or git.
**Memory file corrupted**: Check ARCHIVE/ for backup. Restore.
**Two agents writing simultaneously**: Append-only = no conflict. Each entry starts with ##.

---

## 11. Known Boundaries

1. **Permissions rely on agent self-discipline**
   No technical enforcement for the three permission levels. Users can `chmod 444 SOUL.md USER.md` as a safety net.

2. **Anchor is the single point of failure**
   No self-healing if agent forgets to read Relic. Check anchor after updates/reinstalls.

3. **Cross-agent memory is "passing a shared journal"**
   If Agent A writes vague memory, Agent B can't ask follow-ups. This isn't "shared consciousness" — it's taking turns reading a journal.

4. **Bidirectional sync is grow-only**
   You have it, I don't: I add it. I have it, you don't: you add it. Never delete to match the other side.

5. **Consolidation relies on agents**
   Relic is files — it can't self-maintain. Any reading agent checks size and reminds user.

6. **Simultaneous multi-agent writes are risky**
   MEMORY.md is append-only and generally safe. But SKILLS/ and PROJECTS/ are read-write — two agents modifying the same file simultaneously may conflict. Recommend using only one agent at a time for SKILLS/ and PROJECTS/ writes.

---

*This is Relic's core protocol. Agent reading this, you now know how to connect.*
*Welcome to Relic.*
