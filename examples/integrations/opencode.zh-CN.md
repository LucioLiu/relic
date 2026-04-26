# OpenCode 接入指南 / OpenCode Integration Guide

**English version**: [opencode.md](opencode.md)

## 前提 / Prerequisites

- 已安装 OpenCode / OpenCode installed
- 已下载 Relic 到 `~/relic/` / Relic downloaded to `~/relic/`

## 步骤 / Steps

### 第一次设置 / First-time Setup

1. 告诉 OpenCode / Tell OpenCode:
   > "读一下 `~/relic/AGENT.zh-CN.md`，把你知道的关于我的一切导入 Relic。"

2. OpenCode 会执行场景A（完整导入） / OpenCode executes Scenario A (Full Import)

3. 等导入完成后继续 / Wait for completion

### 植入锚点 / Plant Anchor

推荐位置 / Recommended location: `WORK_RULES.md` 或 `opencode.json` 的 `instructions` 字段

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

锚点植入后，每次新会话自动加载 Relic。
After anchor is planted, Relic loads automatically every new session.

## 注意事项 / Notes

- OpenCode 支持 subagent，每个 subagent 都可以读 Relic
- OpenCode supports subagents — each can read Relic
- OpenCode 的 WORK_RULES.md 是每次会话自动加载的配置文件
- OpenCode's WORK_RULES.md is auto-loaded every session
