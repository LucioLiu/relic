# Hermes 接入指南 / Hermes Integration Guide

**English version**: [hermes.md](hermes.md)

## 前提 / Prerequisites

- 已安装 Hermes / Hermes installed
- 已下载 Relic 到 `~/relic/` / Relic downloaded to `~/relic/`

## 步骤 / Steps

### 第一次设置 / First-time Setup

1. 告诉 Hermes / Tell Hermes:
   > "读一下 `~/relic/brain/PROTOCOL.md`，把你知道的关于我的一切导入 Relic。"

2. Hermes 会执行场景A（完整导入） / Hermes executes Scenario A (Full Import)

3. 等导入完成后继续 / Wait for completion before continuing

### 植入锚点 / Plant Anchor

Hermes 的锚点位置取决于你的配置方式。常见选项：
Hermes anchor location depends on your config. Common options:
- 配置文件中的 system prompt / System prompt in config
- `.hermes` 文件 / `.hermes` file
- 项目级 `.agents/skills/` 目录

锚点模板见 `brain/PROTOCOL.md` 第九节。
Anchor template in `brain/PROTOCOL.md` Section 9.

### 日常使用 / Daily Use

锚点植入后，每次启动自动加载 Relic。
After anchor is planted, Relic loads automatically every session.

## 注意事项 / Notes

- Hermes 可能没有自己的持久化记忆文件——这种情况下 Relic 是唯一的记忆载体
- Hermes may not have its own persistent memory — in this case Relic IS the memory
- 建议把 SKILLS/ 里的技能适配为 Hermes 的技能格式
- Recommend adapting SKILLS/ into Hermes's skill format
