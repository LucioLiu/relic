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

锚点模板见 `docs/protocol.zh-CN.md` 第九节。
Anchor template in `docs/protocol.md` Section 9.

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
