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
