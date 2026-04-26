# OpenClaw 接入指南 / OpenClaw Integration Guide

**English version**: [openclaw.md](openclaw.md)

## 前提 / Prerequisites

- 已安装 OpenClaw / OpenClaw installed
- 已下载 Relic 到 `~/relic/` / Relic downloaded to `~/relic/`

## 步骤 / Steps

### 第一次设置 / First-time Setup

1. 打开 OpenClaw，告诉它 / Open OpenClaw, tell it:
   > "读一下 `~/relic/AGENT.zh-CN.md`，把你知道的关于我的一切导入 Relic。"

2. OpenClaw 会执行场景A（完整导入）——记忆、技能、对话、项目 / OpenClaw executes Scenario A (Full Import) — memories, skills, conversations, projects

3. 等导入完成，看到汇报后继续 / Wait for import report before continuing

### 植入锚点 / Plant Anchor

在 `AGENTS.md` 中添加锚点（务必）。OpenClaw 每次启动会读这个文件。
Add anchor to `AGENTS.md` (mandatory). OpenClaw reads this file every session.

锚点内容如下 / Anchor content:
```markdown
<!-- RELIC 锚点开始 -->
步骤0：读取 `[brain路径]/.relic-version`，检查远程版本（超时5秒自动跳过）。
步骤1：检查 `[brain路径]/SESSIONS/` 未记录的对话 → 有则追加。
步骤2：读取 `[brain路径]/SOUL.md` → 理解自己是谁。
步骤3：读取 `[brain路径]/USER.md` → 理解用户是谁。
步骤4：读取 `[brain路径]/MEMORY.md` 全文。**超过 400 行必须先整理。**
步骤5：同步 Relic 新记忆到自己的记忆文件，标注 `[来自Relic/躯壳名]`。
步骤5.5：七大文件对齐检查。
步骤6：更新 MEMORY.md 头部：上次整理日期 + 核对条目数。
步骤7：MEMORY.md 超过 200 行则建议整理（详见第七节）。
步骤8：正常工作。重要事项随时追加到 MEMORY.md。

**必须汇报**：步骤8之后，汇报：完成的步骤、发现的问题、待用户决定的事项。

> **完整步骤和边界情况**：见 `docs/protocol.zh-CN.md` 第九节。
<!-- RELIC 锚点结束 -->
```

`[brain路径]` 替换为你的实际路径，如 `~/relic/brain`。
Replace `[brain路径]` with your actual path, e.g. `~/relic/brain`.

### 日常使用 / Daily Use

每次启动 OpenClaw 后，如果锚点已植入，Relic 会自动加载。
After planting anchor, Relic loads automatically every session.

如果锚点没植入，手动告诉 OpenClaw / Without anchor, manually tell OpenClaw:
> "读一下 `~/relic/docs/resonate-soul.zh-CN.md` 灵魂共鸣并执行。"

## 注意事项 / Notes

- OpenClaw 的 IDENTITY.md → 合并到 SOUL.md 的"补充"段，Relic 没有 IDENTITY.md
- OpenClaw 的记忆系统是 MEMORY.md，和 Relic 的 MEMORY.md 可以双向同步
- OpenClaw 会把新记忆同时写入自己的 MEMORY.md 和 Relic 的 MEMORY.md
- OpenClaw's memory system (MEMORY.md) syncs bidirectionally with Relic's MEMORY.md
