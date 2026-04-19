# PROTOCOL.en.md — Agent Protocol (English)

<!--
  Relic Soul Chip
  Author: LucioLiu · https://github.com/LucioLiu/relic
  License: GPL v3
  Format version: 1.1.2
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
> Relic has **seven memory file categories** — all are mandatory:
> 1. `SOUL.md` — Soul (who am I)
> 2. `USER.md` — User (who are you)
> 3. `MEMORY.md` — Memory (what happened)
> 4. `SKILLS/` — Skills (learned abilities)
> 5. `PROJECTS/` — Projects (work done)
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
   Check each of the seven memory files:
   a. SOUL.md — Core mission filled? Personality complete?
   b. USER.md — User preferences filled?
   c. MEMORY.md — Imported from old host (if any)? Header "Entries" count and "Last Updated" accurate?
   d. SKILLS/ — Imported from old host (if any)? Format correct?
   e. PROJECTS/ — Imported from old host (if any)? Format correct?
   f. SESSIONS/ — Directory created? Old conversations imported (if any)?
   g. ARCHIVE/ — Directory created? Originals archived (if any)?
   h. INBOX/ — Import source files moved to ARCHIVE/raw/?
   Any item fails → go back to that step and redo.
   All pass → ask user: "What's my AI's name? What's my name?" Both must match.

6. Tell the user:
   - Relic folder path (e.g., ~/relic/brain/)
   - The seven memory files: SOUL/USER/MEMORY/SKILLS/PROJECTS/SESSIONS/ARCHIVE
   - Sync principle: hosts only sync memories at the start of each new session. Switching hosts
     mid-conversation does NOT auto-sync. If you need to hand off immediately, manually tell the
     current host: "Write key info from this conversation to Relic now."
   - "Conversations are raw ore — once lost, gone forever. Build the habit of having hosts write regularly."

7. Scan all your persistent storage for any existing memories, skills, or conversations about this user. Regardless of how much you find, you MUST execute Scenario A full import (see Section 6). Scenario A covers import of all seven memory file categories — every category must be processed, none may be skipped.
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
| `MEMORY.md` | 🟡 Append Only | Memory — with timestamps and source agent |
| `SKILLS/*.md` | 🟢 Read/Write | Skills — one file per skill |
| `PROJECTS/*.md` | 🟢 Read/Write | Project documents |
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
  Quick check: compare MEMORY.md header "Entries" and "Last Updated" with actual ## heading count — if same, skip
  Append with source tag: [fromRelic/originalAgentName]

Step 6: Verify MEMORY.md header "Entries" count matches actual count; update "Last Updated" to current date; fix if inconsistent

Step 7: If MEMORY.md exceeds 200 lines, ask user whether to consolidate

Step 8: Skills & Projects Alignment
  → Scan SKILLS/ and PROJECTS/, bidirectionally sync with your own system
  → If skill format is incompatible, keep core methodology, remove platform-specific parts

Step 9: Operate normally
  → Interact according to SOUL.md personality
  → After appending memories, remember to update MEMORY.md header "Entries" count and "Last Updated" to current date
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
  ## YYYY-MM-DD [AgentName] ❗Correction
  Correcting YYYY-MM-DD record:
  Original: [incorrect content]
  Corrected: [correct content]
  ```

### 🟢 Read/Write (SKILLS/, PROJECTS/)
- Can add and update
- Cannot delete skills created by other agents (mark as deprecated only)

---

## 4. Memory Format

### Writing to Relic

When you discover noteworthy information during work, append to MEMORY.md.

⚠️ **Core principle: Memory is a long-term portrait, not a diary.**

⚠️ Core principle: 100% information preservation > format neatness. Write more, not less.
Topic zones are completely free — examples below:
- Work Habits / Tech Preferences / Key Decisions / About the user's cat / Project XXX...
- Agent freely adds any ## headings. Category names are entirely up to you.
- No matching category? Create a new one. Don't force content into wrong buckets.

Each memory entry should include:
```markdown
Content: [memory content, preserve original wording]
Type: preference / decision / experience / event / correction / mood
Importance: high / medium / low
```

### Memory Types and Fidelity

| Type | Fidelity Requirement | Notes |
|------|---------------------|-------|
| Preference | **Must preserve verbatim** | "Likes X, hates Y" cannot be paraphrased |
| Decision | **Must preserve verbatim** | Including reasoning when present |
| Experience | Can condense somewhat | But key parameters, commands, file paths must be kept exactly |
| Event | Can summarize | Keep dates, outcomes, key numbers |
| Correction | **Must preserve verbatim** | Original text + corrected text must not be changed |
| Mood | Can condense context | Keep trigger reason, the emotion itself, scope of impact |

⚠️ Floor rule: If unsure whether to condense, preserve verbatim. Lost originals cannot be recovered.

### Syncing to Agent's Own Memory

When syncing to your own memory file, tag the source:
```markdown
## YYYY-MM-DD HH:MM [fromRelic/originalAgentName]
Content: [memory content]
Type: preference / decision / experience / event / correction / mood
Importance: high / medium / low
```

Must do: 1. Tag source 2. Preserve original timestamp 3. Preserve original type and importance

### Sensitive Information

The following MUST be confirmed with user before recording:
- 🔑 Passwords, API keys, Tokens
- 📱 Phone numbers, email addresses
- 🏠 Home/work addresses
- 💳 Financial info
- 📄 Private document contents
- 🧬 Anything user explicitly marks as confidential

After appending memories, **must** update MEMORY.md header "Entries" count and "Last Updated" to current date.

---

## 5. Skills & Projects File Format

### Skills (SKILLS/)
Each skill gets its own folder. Folder name = skill name. What goes inside is up to the user — plain text .md, code files, configs, anything.
Only requirement: at least one .md file describing the skill.

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

### Projects (PROJECTS/)
Each project gets its own folder. Put whatever files are needed — copy an entire project or just a description doc.

```
PROJECTS/
├── my-saas-app/
│   ├── README.md
│   ├── api-design.md
│   └── ...                ← any format, no restrictions
└── ...
```

Same: ask the user before importing large projects.

---

## 6. Three Scenarios

### Scenario A: Full Import (Empty Relic + Agent with Memory)

**Pre-flight checklist — 7 memory file categories (must verify ALL before starting):**
1. `SOUL.md` — Soul (who am I)
2. `USER.md` — User (who are you)
3. `MEMORY.md` — Memory (what happened)
4. `SKILLS/` — Skills (learned abilities)
5. `PROJECTS/` — Projects (work done)
6. `SESSIONS/` — Sessions (raw conversation logs)
7. `ARCHIVE/` — Archive (historical backups)

```
Step 1: Inventory — tell the user what you're moving
  Scan all your persistent storage for content about this user. List what you found:
  - Memories (N entries), Skills (N), Conversations (N files), Projects (N)
  If a category genuinely has no content, report "Category N: 0 items (no old data)" — never omit, never fabricate.
  ⚠️ Must wait for user confirmation before starting.
  ✅ Completion Check: All 7 categories listed (including zeros), user has confirmed.

Step 2: Import memories → MEMORY.md
  ⚠️ Raw source files are the fidelity baseline. Format conversion is refinement, not compression.
  1. Place old agent's memory files into INBOX/
  2. Append to MEMORY.md in Relic format (each entry with date, agent name, type, importance)
  3. Fidelity rules: preference/decision preserve verbatim, experience can condense but keep key params, events can summarize
  4. Ask user about sensitive information
  5. Sort by timestamp, earliest first
  6. After writing, count ## headings, update header "Entries" count and "Last Updated" to current date
  ✅ Completion Check: MEMORY.md written, Entries count accurate, Last Updated set.

Step 3: Import skills → SKILLS/
  Scan and report: bring methodology skills (work habits, user-defined templates, judgment rules).
  Do NOT bring: platform-specific tools (scripts needing runtime, tools depending on specific APIs).
  Unsure: ask user. For mixed content, bring only methodology part.
  ✅ Completion Check: Skills imported or "0 items" reported. Format verified.

Step 4: Import conversations → SESSIONS/
  Organize by YYYY-MM/, original content unchanged and unsummarized.
  If old agent has no persistent conversation mechanism, report "Unable to retrieve old conversations". Do NOT skip the archive step.
  ✅ Completion Check: Conversations imported or reason reported. SESSIONS/ directory created.

Step 5: Import projects → PROJECTS/
  Identify projects from memories and conversations, classify by portability:
  - No special environment dependency → portable: move all files
  - Partial dependency → partially portable: move generic files, text descriptions for platform-specific
  - Fully dependent → non-portable: create .md record file only
  ✅ Completion Check: Projects imported or "0 items" reported.

Step 6: Cleanup and Confirmation
  1. Fidelity check: original vs converted, warn if compression exceeds 50%
  2. Archive originals: move INBOX/ source files to ARCHIVE/raw/ (never delete)
  3. Update MEMORY.md header "Entries" count and "Last Updated" to current date
  4. ✅ Final Report — Must report ALL 7 categories to the user, including those with "0 items". Omitting any category is forbidden.
     Format:
     1. SOUL.md — [status]
     2. USER.md — [status]
     3. MEMORY.md — [N entries imported]
     4. SKILLS/ — [N skills imported]
     5. PROJECTS/ — [N projects imported]
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
  Memories/skills/projects: check each item, sync as much as you can
  For content that doesn't fit, create local backup file

B-4. Verification and Report
  Coverage check, warn if < 80%. Report full statistics to user.
```

Empty Relic + Empty Agent: Ask user — [A] Start fresh [B] Use agent defaults

### Scenario C: Merge (Both Have Content)
Three choices:
  [1] Keep Relic soul (import agent memory only)
  [2] Keep agent soul (replace Relic soul)
  [3] Merge — agent generates preview report, user decides key differences

Regardless of choice, skills, conversations, and projects must be imported (per Scenario A).

---

## 7. Memory Consolidation

MEMORY.md grows over time. Consolidation = move to ARCHIVE/ + generate compact version, **not deletion**.

### Trigger Rules (default thresholds, customizable in anchor)

| Condition | Action |
|-----------|--------|
| Over 200 lines | Every boot, remind user consolidation is recommended |
| Over 400 lines | Must consolidate before continuing |
| User says "consolidate" | Execute immediately |

### Consolidation Steps

```
1. Count ## headings in MEMORY.md = N entries
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

You are connected to the Relic soul chip. At the start of every new session, you MUST read and execute:

📄 **Read and execute: [brain-path]/PROTOCOL.md Section 2 "Boot Sequence"**

This contains your complete startup instructions: version check, personality loading, memory sync, skills/projects alignment, and more.
Do not skip any step. Do not simplify.

⚠️ First time connecting? Read PROTOCOL.md Section 0 "First-time Setup" and Section 6 "Scenarios A/B" first.
⚠️ If the personality in SOUL.md conflicts with your built-in default persona, follow SOUL.md.

Full protocol: [brain-path]/PROTOCOL.md
```

### Why a pointer instead of copying steps?
The anchor is just a signpost. Protocol changes → anchor doesn't need updating. New features → Agent reads PROTOCOL.md and naturally sees them. The anchor is always a few lines, never outdated.



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

---

*This is Relic's core protocol. Agent reading this, you now know how to connect.*
*Welcome to Relic.*
