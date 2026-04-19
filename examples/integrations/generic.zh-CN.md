# 通用接入指南 / Generic Integration Guide

**English version**: [generic.md](generic.md)

适用于：Claude Code、Cursor、Aider、Windsurf，或任何能读本地文件的 AI Agent。
Works with: Claude Code, Cursor, Aider, Windsurf, or any AI that reads local files.

## 前提 / Prerequisites

- 你使用的 AI 工具能读本地文件 / Your AI tool can read local files
- 已下载 Relic 到 `~/relic/` / Relic downloaded to `~/relic/`

## 步骤 / Steps

### 第一次设置 / First-time Setup

1. 打开你的 AI 工具，告诉它 / Open your AI tool, tell it:
   > "读一下 `~/relic/brain/PROTOCOL.md`，把你知道的关于我的一切导入 Relic。"

2. AI 会执行 PROTOCOL.md 中的场景A（完整导入） / AI executes Scenario A (Full Import) from PROTOCOL.md

3. 等导入完成后继续 / Wait for completion

### 植入锚点 / Plant Anchor

在你 AI 工具的配置文件里添加锚点（务必）。常见配置文件位置：
Add anchor to your AI tool's config file (mandatory). Common locations:

| AI 工具 | 配置文件 | Config File |
|---------|---------|-------------|
| Claude Code | `CLAUDE.md` | |
| Cursor | `.cursorrules` | |
| Aider | `.aider.conf.yml` | |
| 其他 | 系统提示词或 system prompt | |

锚点模板见 `brain/PROTOCOL.md` 第九节。
Anchor template in `brain/PROTOCOL.md` Section 9.

### 日常使用 / Daily Use

锚点植入后，每次启动自动加载 Relic。
After anchor is planted, Relic loads automatically every session.

如果没有锚点，每次手动告诉 AI / Without anchor, manually tell AI:
> "读一下 `~/relic/brain/PROTOCOL.md` 第二节「启动流程」并执行。"

## 注意事项 / Notes

- 如果你的 AI 没有持久化记忆功能，Relic 就是唯一的记忆载体
- If your AI has no persistent memory, Relic IS the memory
- Relic 是纯文件方案，不依赖网络——完全离线可用
- Relic is pure files — works completely offline, no network needed
