# Generic Agent Integration

## Your agent isn't listed? No problem.

Relic is designed so any agent can connect.

As long as your agent can **read local files**, it can use Relic.

> ⚠️ **Prerequisite**: Make sure your agent can access the brain directory (readable file path).
> If the agent runs in a container/sandbox, mount the brain directory.

---

## Integration Steps

### Step 1: Initialize
Copy template files, remove `.template` suffix:
```
SOUL.template.md → SOUL.md
USER.template.md → USER.md
MEMORY.template.md → MEMORY.md
```
Fill them in (or ask your agent to help).

### Step 2: Neural Anchor

> 💡 Below is a simplified anchor. The full version (with lightweight mode and disconnect instructions) is in `docs/protocol.md` Section 9.
Find your agent's **core startup file** — the file it reads every session.
Add this to that file:

> 💡 **Tip**: If your agent prefers Chinese, use the anchor template from `docs/protocol.zh-CN.md`. For English, use the template below.

```markdown
## ⚡ Relic Soul Chip

> 💡 What is this? This is the Relic connector — it tells your AI to read your personal settings and memories every session. To disconnect, simply delete this text. See docs/protocol.md Section 9.

You are connected to the Relic soul chip. Your memory has two homes:
1. Your own memory system (auto-maintained, works normally)
2. Relic soul chip (shared across agents, maintained by you)

⚠️ This is a sync, not a brain replacement.
You are the host; Relic is the soul.

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
Step 5: Sync new memories from Relic to your own memory file
  Quick check: compare MEMORY.md header "Entries" with actual list items (lines starting with -) — if they match, skip sync
  "Your own memory file" means your platform's long-term memory (e.g., CLAUDE.md, memory logs, etc.). If unsure where to write, ask the user.
  → Append with source tag: [fromRelic/originalAgentName]
Step 6: Verify MEMORY.md header "Entries" count matches actual list items count
  → Fix if inconsistent (skip this step during Scenario B first injection)
Step 7: If MEMORY.md exceeds 200 lines:
  → Tell user "Relic memory file is large, consolidation recommended. Consolidate now?"
  → If user agrees, execute consolidation (see docs/protocol.md section 7)
  → If user says "not now", skip for this session, remind again next boot
Step 8: Work normally
  → Interact according to SOUL.md personality
  → Load SKILLS/ and PROJECTS/ as needed
  → ⚠️ After appending memories, remember to update MEMORY.md header "Entries" count

Full protocol: [project-path]/docs/protocol.md
```

Replace `[brain-path]` with your actual brain directory path.

💡 We recommend placing the anchor at the **beginning** of your config file, so the agent reads it first.

### Step 3: Verify
Ask your agent: "Did you read my Relic? What's my AI's name?"
If it answers correctly, you're connected.

---

## Common Agent Config Files

| Agent | Config File | Where to Anchor |
|-------|-----------|----------------|
| OpenClaw | AGENTS.md | Append anchor |
| Claude Code | CLAUDE.md | Append anchor |
| Cursor | .cursorrules | Append anchor |
| Aider | .aider.conf.yml | Add to read option |
| Cline | .clinerules | Append anchor |
| Custom | system prompt or config | Add anchor text |

---

## Import Old Memories

1. Place your agent's old memory files in `brain/INBOX/`
2. Tell your agent: "Read INBOX/ files, extract key info, append to MEMORY.md per docs/protocol.md"
3. Agent auto-converts and cleans up INBOX/
