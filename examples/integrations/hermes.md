# Hermes Integration Guide

> ⚠️ **Prerequisite**: Make sure the agent can access the brain directory (readable file path). If the agent runs in a container/sandbox, you need to mount the brain directory.

## Step 1: Initialize Relic

If this is your first time:
1. Copy template files, remove the `.template` suffix:
   - `SOUL.template.md` → `SOUL.md`
   - `USER.template.md` → `USER.md`
   - `MEMORY.template.md` → `MEMORY.md`
2. Fill in SOUL.md and USER.md (you can ask Hermes to help)

If you already have Hermes memories:
1. Put Hermes's memory/config files into `brain/INBOX/`
2. Then proceed to Step 2

## Step 2: Plant Anchor (Critical Step)

> 💡 Below is a simplified anchor. The full version (with lightweight mode and disconnect instructions) is in `docs/protocol.md` Section 9.

Add the following to Hermes's **config file**. Recommended locations (by priority):
1. `system_prompt` field in `~/.hermes/config.yaml` (most reliable, read every session)
2. Project-level `.hermes/rules.md` file (for project-specific use)
3. `~/.hermes/SOUL.md` (if your Hermes version supports it)

```markdown
## ⚡ Relic Soul Chip

> 💡 What is this? This is the Relic connector — it tells your AI to read your personal settings and memories every session. To disconnect, simply delete this text. See docs/protocol.md Section 9.

You are connected to the Relic soul chip. Your memory has two homes:
1. Your own memory system (auto-maintained)
2. Relic soul chip (shared across agents, maintained by you)

⚠️ This is a sync update, not a brain replacement.
⚠️ If SOUL.md personality conflicts with your default persona, SOUL.md takes priority.

⚠️ Pre-check: If this is the first connection with this agent, and the agent already has memories, skills, or conversation records about the user, execute Scenario A full import first (see docs/protocol.md Section 6, Scenario A). If Relic files don't exist yet, run first-time setup (see docs/protocol.md Section 0).

<!-- RELIC ANCHOR START -->
Step 0: Read `[brain-path]/.relic-version`, check remote version (5s timeout, skip on failure).
Step 1: Check `[brain-path]/SESSIONS/` for your last conversation log → backfill if missing.
Step 2: Read `[brain-path]/SOUL.md` → understand your identity.
Step 3: Read `[brain-path]/USER.md` → understand the user.
Step 4: Read `[brain-path]/MEMORY.md` fully. **If >400 lines, consolidation required before proceeding.**
Step 5: Sync new memories from Relic, tagged `[fromRelic/originalAgentName]`.
Step 5.5: Seven-file alignment check.
Step 6: Update MEMORY.md header: last consolidated date + verify entry count.
Step 7: If MEMORY.md >200 lines, suggest consolidation (see Section 7).
Step 8: Begin normal work. Append important items to MEMORY.md as needed.

**Mandatory status report**: After Step 8, report: Steps completed, issues found, items pending user decision.

> **Full step details and edge cases**: See `docs/protocol.md` Section 9.
<!-- RELIC ANCHOR END -->
```

Replace `[brain-path]` with your actual path.
Common paths: Linux `/home/your-username/relic/brain`, Mac `/Users/your-username/relic/brain`.

💡 We recommend placing the anchor at the **beginning** of your config file, so the agent reads it first.

## Step 3: Verify

Start Hermes and ask it:
> "Did you read my Relic? Tell me my AI's name and my name."

If it can answer, the integration is successful.

## Daily Use

Use Hermes normally. It will automatically read Relic every session.
After conversations, remind Hermes to save session logs to SESSIONS/.

## Permission Reminders

- SOUL.md and USER.md: Hermes can only read, not modify
- MEMORY.md: Hermes can only append at the end
- SKILLS/ and PROJECTS/: Hermes can read and write freely

## Notes

- Hermes's `memories/` folder contains MEMORY.md and USER.md. Conversation logs → SESSIONS/, curated memories → MEMORY.md
