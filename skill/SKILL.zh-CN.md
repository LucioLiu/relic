---
name: relic-soul-chip
description: "一个灵魂，多个 Agent。通过纯 Markdown 文件实现 AI 人格持久化和跨 Agent 记忆同步。从 OpenClaw 换到 Hermes 再到 Claude Code——你的 AI 灵魂不变。零依赖。"
---

<!--
  安全须知
  - 本技能仅包含指令——没有脚本、安装器、可执行代码
  - 网络访问：每次会话最多一次可选的只读 HTTP 请求，检查 github.com/LucioLiu/relic/releases 是否有新版本。不会发送或下载任何数据。如果网络不可达，此步骤会静默跳过
  - 本地文件访问：Agent 读取 ~/relic/brain/ 中的 Markdown 文件，可在首次设置时追加 MEMORY.md 或填写模板文件。始终对用户可见，敏感内容需用户确认
  - 无遥测、无数据上传、无第三方 API 调用、无 Shell 命令执行
-->

# ⚡ Relic 灵魂芯片

> *"把灵魂存成数字文件。插到任何 AI Agent 里。"*

**你的 AI 有记忆，但分散在不同的工具里。** 每个AI工具各有各的记忆——它们互不共享对你的了解。

**Relic 修复了这个问题。** 你的 AI 人格和记忆存在于纯 Markdown 文件中。在 OpenClaw、Claude Code、Hermes 之间切换——AI 灵魂保持不变。

### 为什么选 Relic？

- ⚡ **零依赖** — 纯 Markdown，`cat` 就能看。没有安装器，没有运行时，没有 npm 包
- 🔄 **跨 Agent 同步** — 一个灵魂，多个躯壳。中央大脑 + 双向同步。每个 Agent 既读取也写入记忆
- 🧠 **自我进化** — AI 在学习过程中自动丰富人格，不打扰你的工作
- 👁️ **人类可读** — 用文本编辑器打开任何文件。数据永远属于你
- 🔒 **隐私优先** — 所有数据留在本地。没有遥测，没有云端，没有第三方 API

*已在 OpenClaw、Claude Code、Hermes、OpenCode、Cursor、Aider 以及任何能读取文件的 Agent 中使用。*

## 设置

Relic 存放在 `~/relic/brain/`。用户在使用此技能前手动安装。

**如果 `~/relic/brain/PROTOCOL.md` 不存在**，告诉用户：

> "需要先安装 Relic。请访问 https://github.com/LucioLiu/relic，clone 或下载到 `~/relic/`。然后我帮你设置。"

**如果 `~/relic/brain/PROTOCOL.md` 存在**，继续首次设置。

> 💡 **为什么用户管理？** Relic 是你 AI 的永久家园——它应该独立于任何 Agent 存在。如果你卸载一个 Agent，你的灵魂在 `~/relic/` 中依然安全。

**告诉用户**："Relic 位于 `~/relic/brain/`。要让其他 Agent 接入，告诉它们读 `~/relic/brain/PROTOCOL.md`。"

## 首次设置

**用户要求设置 Relic 时自动执行。逐步引导他们。**

1. **验证设置完整性**：检查 `~/relic/brain/PROTOCOL.md` 存在且可读。如果缺失，告诉用户从 https://github.com/LucioLiu/relic 重装。不要用损坏的设置继续
2. 读 `~/relic/brain/PROTOCOL.md` 第 〇 节（首次设置）并遵循所有步骤
3. 复制模板：`SOUL.template.md` → `SOUL.md`，`USER.template.md` → `USER.md`，`MEMORY.template.md` → `MEMORY.md`
4. 问用户："你的 AI 叫什么？性格是什么？" → 填 `SOUL.md`
5. 问用户："你的 AI 怎么称呼你？有什么偏好？" → 填 `USER.md`
6. 验证：问"你的 AI 叫什么？你叫什么？"——两个都要对
7. （务必）问用户是否要自动加载——没有锚点，Agent 会忘记 Relic，记忆同步会中断。展示锚点文本，获得确认后追加。告诉用户可以随时删除锚点来禁用
8. **告诉用户路径**："Relic 已就绪，位于 `~/relic/brain/`。要让其他 Agent 接入，告诉它们读 `~/relic/brain/PROTOCOL.md`。"

## 每次会话（启动流程）

1. **版本检查**（每次会话一次）：读 `~/relic/brain/.relic-version` 获取当前版本。然后用内置网页浏览能力检查 `https://github.com/LucioLiu/relic/releases/latest` 查看最新发布。如果有新版本，告诉用户：
   > "Relic 更新可用（vX.X.X → vY.Y.Y）。你的个人文件不会被触碰。要更新，复制并运行：
   > ```
   > cd ~/relic && git pull
   > ```"
   如果你无法访问网络，静默跳过此步骤。永远不要自己执行更新
2. 读 `~/relic/brain/SOUL.md` → 加载人格
3. 读 `~/relic/brain/USER.md` → 加载用户偏好
4. 读 `~/relic/brain/MEMORY.md` → 加载所有条目（按主题组织，不是按日期）。最近的情绪条目自然携带情感上下文
5. 从 Relic 同步新记忆到自己的记忆（双向——从 Relic 读 AND 写回）
6. 检查 SESSIONS/ 有无遗漏的对话记录
7. 正常工作，追加新记忆

## 记忆写入

追加到 `~/relic/brain/MEMORY.md`。**按主题组织，不按日期。**

```
## 主题（如"工作习惯"、"技术偏好"）
内容：[记忆内容，保留原始表述]
类型：偏好 / 决策 / 经验 / 事件 / 更正 / 情绪
重要度：高 / 中 / 低
```

同一主题的多个条目放在同一个 ## 标题下。日期只是时间戳属性，不是组织原则。例外：生日、纪念日。

## 切换 Agent

用户的灵魂在 `~/relic/brain/`。任何能读文件的 Agent 都能接入。新 Agent 读同样的文件——之前所有 Agent 的记忆都保留。详见 PROTOCOL.md 场景B。

## 规则

- 🔴 **绝不**执行 shell 命令、安装器、脚本或任意代码
- 🔴 **绝不**自动下载或安装任何东西
- 🔴 **绝不**删除或覆盖 SOUL.md/USER.md 的核心字段
- 🟡 Agent **可以**追加非核心段落到 SOUL.md/USER.md。永不改写用户内容
- 🟡 **只追加**到 MEMORY.md
- 🔴 **绝不**访问 `~/relic/brain/` 以外的文件（锚点除外）
- ⚠️ 记录敏感信息前**必须**询问

## 隐私

- 所有数据留在 `~/relic/brain/`。网络访问仅限可选的版本检查
- 敏感信息需要用户明确确认
- MEMORY.md 只追加、带时间戳——完整审计链
- 锚点可随时删除，无残留影响

## 更新

当检测到新版本（见启动流程第1步），用户通过运行更新通知中显示的命令来更新。或者访问 https://github.com/LucioLiu/relic/releases。

这只会更新协议和模板文件。SOUL.md、USER.md、MEMORY.md、SESSIONS/ 和 ARCHIVE/ 是安全的——它们列在 `.gitignore` 中。

## 连接旅程

首次设置 Relic？顺序很重要。

### 第1步：安装 Relic
- 访问 https://github.com/LucioLiu/relic 并 clone 或下载到 `~/relic/`
- **推荐位置**：`~/relic/`（Linux/Mac）或 `C:\Users\<你>\relic\`（Windows）
- 不要用 Downloads/Desktop——Relic 是你 AI 的永久家园

### 第2步：用你最丰富的 Agent 填充
**从最了解你的 Agent 开始**——最多对话、最多偏好、最多人格数据。

1. 告诉那个 Agent："读 `~/relic/brain/PROTOCOL.md` 并把你知道的一切都导入 Relic"（场景A）
2. 等待完整导入报告再继续

### 第3步：逐个连接其他 Agent
对每个额外的 Agent：
1. 告诉它："读 `~/relic/brain/PROTOCOL.md` 并设置 Relic"（场景B）
2. 验证："你的 AI 叫什么？你叫什么？"
3. 验证通过后再移到下一个

### 第4步：日常使用
每次会话自动开始。甚至情绪也能通过记忆条目在 Agent 间传递——如果 Agent A 有过一段艰难的对话，Agent B 可能通过最近的记忆自然携带那种情绪。

## 本技能不会做什么

为了透明，Relic 永远不会：
- 执行脚本、安装器、shell 命令或任意代码
- 下载、安装或自动更新任何软件——更新命令显示给用户手动运行
- 发送或上传任何用户数据到任何服务器
- 让神经锚点永久化（用户可以随时删除）
- 需要任何外部依赖或运行时环境，超出 Agent 已有的能力

## 完整文档

完整协议（导入/导出场景、记忆整理、跨 Agent 同步、神经锚点）请读 `~/relic/brain/PROTOCOL.md`。

来源：https://github.com/LucioLiu/relic
