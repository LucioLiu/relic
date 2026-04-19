# Relic — Project Master Plan (Final Version)

> Name inspired by: Cyberpunk 2077 · Arasaka Relic Biochip
> A soul chip that works in any agent host.

---

## One-line Definition

Relic is a zero-dependency, pure-file, human-and-AI-readable AI personality persistence framework.
Any AI Agent can connect by reading the protocol once — no code required.

---

## Core Philosophy

```
Relic chip = Soul + Memory + Skills (central brain)
Agent (Host) = Execution + Tools (replaceable)

Relic doesn't depend on any specific Agent framework
Agents are replaceable hosts, Relic is the one soul
```

You (the user) have one soul chip (Relic) storing your personality, memories, and preferences.
You can plug this chip into any agent host (OpenClaw, Hermes, Claude Code, OpenCode...).
The host gains a soul and works for you. Change hosts, keep the soul.

---

## Design Principles

### 1. Convention over Configuration
File names are the convention: SOUL.md = soul, USER.md = user, MEMORY.md = memory.

### 2. Native Markdown
Humans edit directly, agents read directly. `cat SOUL.md` shows the soul.

### 3. Three-tier Permission (Anti-Cyberpsychosis)
| Permission | Files | What agents can do |
|-----------|-------|-------------------|
| 🟡 Enrichable (core protected) | SOUL.md, USER.md | May add content but must NOT modify core fields (name, mission, user's preferred name) |
| 🔴 Read Only | ARCHIVE/, SESSIONS/ | Read only — never modify or delete |
| 🟡 Append Only | MEMORY.md | Only append to the end, never modify old content |
| 🟢 Read/Write | SKILLS/, PROJECTS/ | May add and update |

### 4. Append-only Memory
Never modify history, only append. Periodic consolidation archives old entries; originals are never deleted.

### 5. Progressive Loading (6 layers)
```
L0 Soul (loaded every session, ~1K tokens): SOUL.md + USER.md
L1 Memory (loaded at startup, ~2-8K tokens): MEMORY.md last N entries
L2 Skills (loaded on demand): Relevant skills from SKILLS/
L3 Projects (loaded on demand): Relevant project docs from PROJECTS/
L4 Archive (loaded on demand): Consolidated memories from ARCHIVE/
L5+ Sessions (never auto-loaded): Full conversation logs in SESSIONS/
```

### 6. Neural Anchor in Agent (Critical!)
Plant an anchor in the agent's own core config file, ensuring the agent remembers to read Relic every session.
This is the prerequisite for the entire system — if the agent forgets Relic, nothing works.

### 7. Bilingual (Chinese + English)
File names in English (easy for agents to reference), content bilingual (everyone can read). UI supports language switching.

---

## Core File Structure

```
brain/
├── SOUL.md                  # 🟡 Enrichable (core protected) — Soul (includes Core Mission)
├── USER.md                  # 🟡 Enrichable (core protected) — User profile
├── MEMORY.md                # 🟡 Append Only — Refined memories
├── PROTOCOL.md              # Agent protocol (Chinese)
├── PROTOCOL.en.md           # Agent protocol (English)
├── .relic-version           # Version number
├── SKILLS/                  # 🟢 Read/Write — Skills library (YAML Front Matter metadata)
│   └── *.md
├── PROJECTS/                # 🟢 Read/Write — Project docs (agent or user added)
│   └── *.md
├── SESSIONS/                # 🔴 Read Only — Raw conversation logs (never auto-loaded)
│   ├── 2026-04/
│   │   ├── 2026-04-15.openclaw.md
│   │   └── 2026-04-16.opencode.md
│   └── ...
├── ARCHIVE/                 # 🔴 Read Only — Consolidated archives (never deleted)
│   ├── 2026-04.raw.md
│   └── index.md
└── INBOX/                   # 🟢 Read/Write — Import buffer
```

---

## Three Integration Scenarios

### Scenario A: Import (Empty Relic + Agent with Memory)
Full house-moving — not just memories, skills, conversations, and projects all come along.
1. Inventory — Agent scans all persistent content, lists for user confirmation
2. Import memories → MEMORY.md (sorted by timestamp, sensitive info asked proactively)
3. Import skills → SKILLS/ (exclude agent-platform-specific tools)
4. Import conversations → SESSIONS/ (original content unchanged, unsummarized)
5. Import projects → PROJECTS/ (identified from memories and conversations)
6. Cleanup and Confirmation — Fidelity check (original vs converted bytes, warn if >50% compression), archive originals to ARCHIVE/raw/ (never delete), report import statistics

### Scenario B: Inject (Relic with Content + Empty Agent)
B-0. Self-check: Assess agent storage capacity, choose transport strategy
B-1. Execute boot sequence (read SOUL/USER/MEMORY, sync new memories to self)
B-2. Soul injection: Write SOUL.md into agent core config (priority: core identity > behavioral norms > detailed settings)
B-3. Sync Relic content (memories/skills/projects, check each item)
B-4. Verification and Report: Coverage check + full sync report to user

Empty Relic + Empty Agent: Ask user —
  [A] Start fresh: describe yourself, agent fills SOUL.md
  [B] Use agent defaults: import agent's built-in persona

### Scenario C: Merge (Both Have Content)
Three choices, no complex overlap calculation:
  [1] Keep Relic soul (import agent memory only)
  [2] Keep agent soul (replace Relic soul)
  [3] Merge — agent generates preview report, lists key differences, user decides item by item

---

## Memory Consolidation

Dual-line system:
- **Soft limit 8K tokens**: Warn when exceeded, allow continuing
- **Hard limit 16K tokens**: Must consolidate when exceeded

Consolidation process:
1. Move entire MEMORY.md to ARCHIVE/YYYY-MM.raw.md (original preserved)
2. Agent generates compact version of MEMORY.md
3. Update ARCHIVE/index.md

SESSIONS/ (raw conversations) are never consolidated, never auto-loaded. User can choose retention period (forever/1yr/6mo/3mo), default forever. Space isn't an issue — one year of conversations ≈ 72MB, smaller than ten photos.

---

## Single-file Export

When exporting a .relic file (zip package), three-tier distillation:

| Level | Contents | Best for |
|-------|----------|----------|
| Soul Mode | SOUL.md + USER.md + MEMORY.md | Public sharing |
| Standard Mode | Soul + Skills + Projects | Device migration |
| Full Mode | Includes all SESSIONS/ | Complete backup (⚠️ privacy warning) |

---

## Neural Anchor Guide

After connecting to Relic, an anchor must be planted in the agent's own core config file. Full anchor template in `brain/PROTOCOL.md` Section 9.

Anchor locations per agent:
- OpenClaw → AGENTS.md
- Claude Code → CLAUDE.md
- Hermes → config file or prompt template
- OpenCode → WORK_RULES.md or instructions

---

## v1.1.1 Changes

Based on real OpenClaw testing of v1.0.4, 27 issues were identified and addressed:

### Concept Shift
- From "insert=gain soul, remove=factory reset" → "central brain + bidirectional sync"
- Every agent is both reader AND writer — grow-only (G-Set)
- Anchors changed from "optional" to "strongly recommended" with consequences explained

### PROTOCOL Restructure
- PROTOCOL.md: 864 → 475 lines (streamlined, no information loss)
- PROTOCOL.en.md: 823 → 475 lines (mirrors Chinese version)
- SESSIONS description: "never auto-loaded" → "must create and write, don't auto-read on startup"

### README Rewrite
- Complete rewrite as beginner-friendly decision tree
- No unexplained jargon in first 30 lines
- Competitor comparison table removed
- chmod explained in plain language
- All 6 file types described (not just 3)

### Permission Label Fix
- SOUL.md and USER.md unified to 🟡 (Enrichable, core protected) across all docs
- INBOX/README "delete" contradiction fixed → moved to ARCHIVE/raw/ permanently

### Bilingual Coverage
- All non-memory files now have bilingual versions
- ~15 new/updated files for complete Chinese+English coverage

### example-brain Expansion
- Added SKILLS/, PROJECTS/, SESSIONS/, INBOX/ with Silverhand-style examples
- Anti-idiot notes in all directory READMEs

### Version Unification
- All version strings unified to 1.1.1

---

## Discussion History

This plan was born from:
- **OpenClaw (Lobster)**: Proposed .chang/brain/ architecture (JSON format, progressive loading), contributed "North Star / Core Mission" concept, YAML Front Matter skill metadata, .relic-manifest.yaml index scheme, warned about over-engineering risks
- **Hermes**: Proposed three-layer architecture and group chat protocol, contributed "merge preview report" concept, agent capability tiering, self-describing file suggestions, pointed out long-term format longevity and version migration concerns
- **Atlas (OpenCode)**: Synthesized both sides, determined "lightweight + Markdown + zero-code" direction, proposed three-tier permissions, three integration scenarios, neural anchor mechanism, SESSIONS/ raw conversation preservation, named Relic

Final decision maker: Hua Xunchang (Brother / 弟弟)
