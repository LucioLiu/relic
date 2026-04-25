# OpenClaw Integration Guide

> ⚠️ **Prerequisite**: Make sure the agent can access the brain directory (readable file path). If the agent runs in a container/sandbox, you need to mount the brain directory.

## Step 1: Initialize Relic

If this is your first time:
1. Copy template files, remove the `.template` suffix:
   - `SOUL.template.md` → `SOUL.md`
   - `USER.template.md` → `USER.md`
   - `MEMORY.template.md` → `MEMORY.md`
2. Fill in SOUL.md and USER.md (you can ask OpenClaw to help)

If you already have OpenClaw memories:
1. Put OpenClaw's MEMORY.md, SOUL.md, and other files into `brain/INBOX/`
2. Then proceed to Step 2

## Step 2: Plant Anchor (Critical Step)

> 💡 Below is a simplified anchor. The full version (with lightweight mode and disconnect instructions) is in `docs/protocol.md` Section 9.

Add the following to OpenClaw's **AGENTS.md** file:

```markdown
## ⚡ Relic Soul Chip

> 💡 What is this? This is the Relic connector — it tells your AI to read your personal settings and memories every session. To disconnect, simply delete this text. See docs/protocol.md Section 9.

You are connected to the Relic soul chip. Your memory has two homes:
1. Your own memory system (OpenClaw auto-maintained)
2. Relic soul chip (shared across agents, maintained by you)

⚠️ This is a sync update, not a brain replacement.
⚠️ If SOUL.md personality conflicts with your default persona, SOUL.md takes priority.

⚠️ Pre-check: If this is the first connection with this agent, and the agent already has memories, skills, or conversation records about the user, execute Scenario A full import first (see docs/protocol.md Section 6, Scenario A). If Relic files don't exist yet, run first-time setup (see docs/protocol.md Section 0).

At the start of every session, execute these steps IN ORDER:

Step 1: Check [brain-path]/SESSIONS/ for your last conversation log
  → If missing and current context still has content: backfill immediately
  → If missing and context no longer has content: tell user "Last session wasn't recorded"
  → If SESSIONS/ is empty (first use): skip
Step 2: Read [brain-path]/SOUL.md
  → If file doesn't exist: tell user to run first-time setup first (see docs/protocol.md Section 0)
Step 3: Read [brain-path]/USER.md
Step 4: Read [brain-path]/MEMORY.md (read entire file, top to bottom)
Step 5: Sync new memories from Relic that you don't know yet to your own memory file
  Quick check: compare MEMORY.md header "Entries" with actual list items (lines starting with -), skip sync if they match
  "Your own memory file" refers to OpenClaw's memory/ journal files. If unsure where to write, ask the user.
  → Append with source tag: [fromRelic/originalAgentName]
Step 5.5: Seven-file alignment check (see resonate-soul Step 5.5 alignment table)
  → Skip if SOUL/USER core fields match; diff-check SKILLS/PROJECTS folder names
Step 6: Verify MEMORY.md header "Entries" count matches actual list items
  → Fix if inconsistent (skip this step during Scenario B first injection)
Step 7: If MEMORY.md exceeds 200 lines:
  → Tell user "Relic memory file is large, consolidation recommended. Consolidate now?"
  → If user agrees, execute consolidation (see docs/protocol.md Section 7)
  → If user says "not now", skip for this session, remind again next boot
Step 8: Work normally
  → Interact according to SOUL.md personality
  → ⚠️ After appending memories, remember to update MEMORY.md header "Entries" count

🔴 **Mandatory**: After completing the above steps, you MUST report the following status before answering any user questions. Answering without reporting = violation.

⚡ Relic Startup Status
- Soul: [AI name] — [Consistent / Differences]
- User: [User address] — [Consistent / Differences]
- Memory: [N] entries — [Consistent / Difference details]
- Skills: [N] — [Aligned / Difference details]
- Projects: [N] — [Aligned / Difference details]
- Version: [Local version] / [Latest remote or "Not checked"]
- Status: [✅ All normal / ⚠️ Differences synced / ❌ Issues need attention]

Full protocol: [project-path]/docs/protocol.md
```

Replace `[brain-path]` with your actual path. Common paths:
- Linux/Mac: `/home/your-username/relic/brain` or `/Users/your-username/relic/brain`
- Windows (WSL): `/home/your-username/relic/brain`
- Windows (native): `C:\Users\your-username\relic\brain`

💡 Tip: If you're unsure of the path, `cd` into the brain directory in your terminal, then run `pwd` (Linux/Mac) or `cd` (Windows) to see the full path.

💡 We recommend placing the anchor at the **beginning** of your config file, so the agent reads it first.

## Step 3: Verify

Start OpenClaw and ask it:
> "Did you read my Relic? Tell me my AI's name and my name."

If it can answer, the integration is successful.

## Daily Use

Use OpenClaw normally. It will automatically read Relic every session.
After conversations, remember to remind OpenClaw to save session logs to SESSIONS/ (this will be automated in the future).

## Permission Reminders

- SOUL.md and USER.md: OpenClaw can only read, not modify
- MEMORY.md: OpenClaw can only append at the end
- SKILLS/ and PROJECTS/: OpenClaw can read and write freely

## OpenClaw Identity File Notes

- OpenClaw's IDENTITY.md → merge into SOUL.md's supplementary section. Relic doesn't have IDENTITY.md
