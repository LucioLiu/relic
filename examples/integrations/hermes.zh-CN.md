# Hermes 接入指南 / Hermes Integration Guide

**English version**: [hermes.md](hermes.md)

## 前提 / Prerequisites

- 已安装 Hermes / Hermes installed
- 已下载 Relic 到 `~/relic/` / Relic downloaded to `~/relic/`

## 步骤 / Steps

### 第一次设置 / First-time Setup

1. 告诉 Hermes / Tell Hermes:
   > "读一下 `~/relic/AGENT.zh-CN.md`，把你知道的关于我的一切导入 Relic。"

2. Hermes 会执行场景A（完整导入） / Hermes executes Scenario A (Full Import)

3. 等导入完成后继续 / Wait for completion before continuing

### 植入锚点 / Plant Anchor

Hermes 的锚点位置取决于你的配置方式。常见选项：
Hermes anchor location depends on your config. Common options:
- 配置文件中的 system prompt / System prompt in config
- `.hermes` 文件 / `.hermes` file
- 项目级 `.agents/skills/` 目录

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

锚点植入后，每次启动自动加载 Relic。
After anchor is planted, Relic loads automatically every session.

## 注意事项 / Notes

- Hermes 的 `memories/` 下有 MEMORY.md 和 USER.md，日志类内容 → SESSIONS/，精选记忆 → MEMORY.md
- Hermes 可能没有自己的持久化记忆文件——这种情况下 Relic 是唯一的记忆载体
- Hermes may not have its own persistent memory — in this case Relic IS the memory
- 建议把 SKILLS/ 里的技能适配为 Hermes 的技能格式
- Recommend adapting SKILLS/ into Hermes's skill format
