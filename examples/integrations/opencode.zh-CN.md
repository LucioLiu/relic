# OpenCode 接入指南 / OpenCode Integration Guide

**English version**: [opencode.md](opencode.md)

## 前提 / Prerequisites

- 已安装 OpenCode / OpenCode installed
- 已下载 Relic 到 `~/relic/` / Relic downloaded to `~/relic/`

## 步骤 / Steps

### 第一次设置 / First-time Setup

1. 告诉 OpenCode / Tell OpenCode:
   > "读一下 `~/relic/brain/PROTOCOL.md`，把你知道的关于我的一切导入 Relic。"

2. OpenCode 会执行场景A（完整导入） / OpenCode executes Scenario A (Full Import)

3. 等导入完成后继续 / Wait for completion

### 植入锚点 / Plant Anchor

推荐位置 / Recommended location: `WORK_RULES.md` 或 `opencode.json` 的 `instructions` 字段

锚点模板见 `brain/PROTOCOL.md` 第九节。
Anchor template in `brain/PROTOCOL.md` Section 9.

### 日常使用 / Daily Use

锚点植入后，每次新会话自动加载 Relic。
After anchor is planted, Relic loads automatically every new session.

## 注意事项 / Notes

- OpenCode 支持 subagent，每个 subagent 都可以读 Relic
- OpenCode supports subagents — each can read Relic
- OpenCode 的 WORK_RULES.md 是每次会话自动加载的配置文件
- OpenCode's WORK_RULES.md is auto-loaded every session
