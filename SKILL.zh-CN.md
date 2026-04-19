---
name: relic-soul-chip
description: "Relic 灵魂芯片——让你的 AI Agent 拥有跨会话的持久人格和记忆。纯 Markdown，人类可读。换躯壳，灵魂跟着走。"
version: "1.1.1"
author: LucioLiu
license: GPL-3.0
homepage: "https://github.com/LucioLiu/relic"
compatibility:
  - "能读文件的 Agent（任何平台）"
  - "需要：git（仅用于 clone 安装），在 Relic 目录中读写文件"
allowed-tools:
  - "Read"
  - "Write"
  - "Bash(git clone:*)"
metadata:
  hermes:
    tags: [人格, 记忆, 跨Agent, 身份, AI灵魂, Agent记忆, Markdown, 用户偏好]
    related_skills: []
    requires_toolsets: []
    requires_binaries: ["git"]
    filesystem_scope:
      read: ["~/relic/brain/"]
      write: ["~/relic/brain/MEMORY.md", "~/relic/brain/SESSIONS/", "~/relic/brain/ARCHIVE/", "~/relic/brain/SOUL.md", "~/relic/brain/USER.md"]

---

# ⚡ Relic 灵魂芯片

给你的 AI Agent 一个跨会话的持久人格和记忆。纯 Markdown。人类可读。

**你的 AI 有记忆，但它们被困在各自的笼子里。** 每个工具各有各的记忆——OpenClaw 认识一个版本的你，Hermes 认识另一个。**Relic 把它们统一起来。** 一个灵魂存在纯 Markdown 文件中。换躯壳，灵魂跟着走。

### 为什么选 Relic？

- ⚡ **零依赖** — 纯 Markdown，`cat` 就能看
- 🔄 **跨 Agent 同步** — 一个灵魂，多个躯壳。中央大脑 + 双向同步
- 🧠 **自我进化** — AI 在学习过程中自动丰富自己的人格
- 👁️ **人类可读** — 用任何文本编辑器打开文件
- 🔒 **隐私优先** — 所有数据留在本地

## 需求

| 需求 | 用途 | 可选 |
|------|------|------|
| `git` | 克隆/更新 Relic 仓库 | 是（可手动下载） |
| HTTP 请求 | 版本检查（raw.githubusercontent.com，每次会话一次） | 是（离线可跳过） |
| 文件系统读取 | 读取 SOUL.md、USER.md、MEMORY.md | 否 |
| 文件系统写入 | 追加到 MEMORY.md、写入会话日志 | 否 |
| Agent 配置修改 | 植入"神经锚点"实现自动加载 | 是（用户可跳过） |

所有文件操作都限制在 `~/relic/brain/`（或用户指定的目录）。唯一可能访问外部的是可选的神经锚点（在 Agent 配置中）。网络访问仅限于版本检查和可选的 git pull，没有数据上传，没有第三方服务。

## 步骤

### 首次设置

1. 安装 Relic：`git clone https://github.com/LucioLiu/relic.git ~/relic`
2. 读完整协议：`~/relic/brain/PROTOCOL.md`
3. 复制模板到正式文件（SOUL.md、USER.md、MEMORY.md）
4. 帮用户填写 SOUL.md（AI 名字 + 核心使命）和 USER.md（用户偏好）
5. **神经锚点（务必）：** 告诉用户这非常重要——没有锚点，下次会话 Agent 会忘记读 Relic，记忆同步会中断。展示要追加的内容，获得确认后追加。
6. 验证：问"我的 AI 叫什么？我叫什么？"——两个都要答对
7. 检查 SESSIONS/ 目录是否存在，同步遗漏的对话

### 每次会话（启动流程）

1. **版本检查**（每次会话一次）：读 `~/relic/brain/.relic-version`，与远程版本对比。有新版本时询问用户是否更新。绝不强推更新。
2. 读 SOUL.md → 加载人格
3. 读 USER.md → 加载用户偏好
4. 读 MEMORY.md → 加载所有条目（按主题组织，不按日期）
5. 同步 Relic 的新记忆到自己的记忆文件（双向——从 Relic 读 AND 写回新记忆）
6. 正常工作，追加新记忆

## 记忆写入

追加到 `~/relic/brain/MEMORY.md`。**按主题组织，不按日期。**

```
## 主题（如"工作习惯"、"技术偏好"）
内容：[记忆内容，保留原始表述]
类型：偏好 / 决策 / 经验 / 事件 / 更正 / 情绪
重要度：高 / 中 / 低
```

## 切换到其他 Agent

用户的灵魂在 `~/relic/brain/`。新 Agent 读同样的文件，遵循 PROTOCOL.md 场景B（注入）。

## 安全与隐私

- **范围限制**：所有读写限制在 `~/relic/brain/`
- **SOUL.md/USER.md**：核心字段受保护——永不删除或覆盖。Agent 可以追加新的非核心段落（如发现的习惯、偏好）作为后台自我进化。
- **敏感数据**：记录前必须展示内容并获得用户明确确认
- **有限网络访问**：每次会话一次可选的版本检查。无遥测、无数据上传。
- **只追加审计**：MEMORY.md 条目带时间戳，永不删除

## 连接旅程

首次设置 Relic 时，顺序很重要：

### 第一步：为 Relic 选一个家

挑一个稳定、好记的位置：
- **推荐**：`~/relic/`（Linux/Mac）或 `C:\Users\<你>\relic\`（Windows）
- 避免 Downloads、Desktop 或临时文件夹——Relic 是永久的
- 如果通过 Agent skill 安装（如 OpenClaw），Agent 应该建议一个位置并向你确认

### 第二步：用最了解你的 Agent 填充 Relic

你的 Agent 们对你的了解程度不同。**从最了解你的那个开始**——那个和你对话最多、掌握最多偏好和人格数据的 Agent。

1. 告诉那个 Agent："读 `~/relic/brain/PROTOCOL.md`，把我的一切导入 Relic"
2. 该 Agent 会执行场景A（完整导入）——记忆、技能、对话、项目
3. 等待它完全完成并向你展示导入报告

### 第三步：逐个连接其他 Agent

对每个额外的 Agent（按任意顺序）：
1. 告诉该 Agent："读 `~/relic/brain/PROTOCOL.md`，为我设置 Relic"
2. 该 Agent 会执行场景B（注入）——读取灵魂、同步记忆、注入人格
3. 验证：问"我的 AI 叫什么？我叫什么？"——两个都必须答对
4. 只有在验证通过后，才继续下一个 Agent

### 第四步：日常使用

设置完成后，每次会话自动开始。无需额外步骤。

> 💡 **提示**：如果你和 Agent A 的对话改变了某些重要事项（新偏好、重大决策），Agent B 会在下次会话通过 Relic MEMORY.md 同步自然获取。甚至情绪也会转移——如果 Agent A 经历了一次令人沮丧的对话，Agent B 可能通过记忆条目自然携带这个上下文。

## 规则

- 🔴 永不删除或覆盖 SOUL.md 或 USER.md 的核心字段
- 🟡 Agent 可以追加非核心段落到 SOUL.md/USER.md。永不改写用户已有内容
- 🟡 只追加到 MEMORY.md
- 🔴 永不从 SKILLS/ 或 PROJECTS/ 执行脚本
- 🔴 永不删除 SESSIONS/ 或 ARCHIVE/
- 🔴 永不访问 ~/relic/brain/ 以外的文件（锚点除外）
- ⚠️ 记录敏感信息前必须询问

## 此技能不做的事

为了透明，Relic 永远不会：
- 执行脚本、安装程序或任意代码
- 自动运行 update.sh（用户必须手动选择）
- 从 SKILLS/ 安装软件或平台特定工具
- 在未先展示具体变更的情况下修改 ~/relic/brain/ 之外的任何文件
- 上传、传输或分享任何用户数据
- 让神经锚点永久化（用户可随时移除）

## 完整文档

阅读 `~/relic/brain/PROTOCOL.md` 获取完整协议，包括：
- 三种导入场景（空→满、满→空、双方都有数据）
- 文件过大时的记忆整合
- Relic 与 Agent 记忆之间的双向同步
- 会话记录指南

来源：https://github.com/LucioLiu/relic
