# OpenClaw 接入 Relic 指南

> ⚠️ **前提 / Prerequisite**: 确保 Agent 能访问 brain 目录（文件路径可读）。如果 Agent 运行在容器/沙箱中，需要挂载 brain 目录。

## 第一步：初始化 Relic

如果这是第一次使用：
1. 复制模板文件，去掉 `.template` 后缀：
   - `SOUL.template.md` → `SOUL.md`
   - `USER.template.md` → `USER.md`
   - `MEMORY.template.md` → `MEMORY.md`
2. 填写 SOUL.md 和 USER.md（可以请 OpenClaw 帮你填）

如果已有 OpenClaw 的记忆：
1. 把 OpenClaw 的 MEMORY.md、SOUL.md 等文件放入 `brain/INBOX/`
2. 然后进行第二步

## 第二步：植入锚点（关键步骤）

> 💡 以下为简化版锚点。完整版（含轻量模式、断开指引）见 `docs/protocol.zh-CN.md` 第九节。

在 OpenClaw 的 **AGENTS.md** 文件中加入以下内容：

```markdown
## ⚡ Relic 灵魂芯片

> 💡 这是什么？这是 Relic 的接入声明，让 AI 每次启动时读取你的个人设置和记忆。要停用？删除这段文字即可。详见 docs/protocol.zh-CN.md 第九节。

你已接入 Relic 灵魂芯片。你的记忆有两个家：
1. 你自己的记忆系统（OpenClaw 自动维护）
2. Relic 灵魂芯片（跨躯壳共享，由你维护）

⚠️ 这是同步更新，不是替换你的大脑。
⚠️ 如果 SOUL.md 中的人格与你自带的默认人设冲突，以 SOUL.md 为准。

⚠️ 前置检查：如果是首次连接此躯壳，且该躯壳已有关于用户的记忆、技能或对话记录，先执行场景A完整导入（见 docs/protocol.zh-CN.md 第六节场景 A），然后再执行以下步骤。如果 Relic 文件还不存在，先执行首次设置（见 docs/protocol.zh-CN.md 〇节）。

每次会话开始，按顺序执行以下步骤：

步骤1：查看 [Relic的brain路径]/SESSIONS/ 里你上次的对话是否已记录
  → 如果遗漏且当前上下文还有内容：立即补充
  → 如果遗漏但上下文已没有：告诉用户"上次对话未记录"
  → 如果 SESSIONS/ 为空（首次）：跳过
步骤2：读取 [Relic的brain路径]/SOUL.md
  → 如果文件不存在：告诉用户需要先执行首次设置（见 docs/protocol.zh-CN.md 〇节）
步骤3：读取 [Relic的brain路径]/USER.md
步骤4：读取 [Relic的brain路径]/MEMORY.md（读全部，从上到下）
步骤5：把 Relic MEMORY.md 中你不知道的新记忆，追加到你自己的记忆文件里
  快速检查：看 MEMORY.md 头部的"条目数"和实际列表项（- 开头的行）数是否一致，一致则跳过同步
  "你自己的记忆文件"指 OpenClaw 的 memory/ 日记文件。如果不确定往哪写，问用户。
  → 追加时标注来源：[来自Relic/原躯壳名]
步骤6：检查 MEMORY.md 头部的"条目数"是否和实际条目数一致
  → 不一致就修正（场景B首次注入时跳过此步骤）
步骤7：如果 MEMORY.md 超过 200 行：
  → 告诉用户"Relic 记忆文件较大，建议整理。是否现在整理？"
  → 用户同意后执行整理流程（见 docs/protocol.zh-CN.md 第七节）
  → 用户说"暂时不要"则本次跳过，下次启动再提醒
步骤8：正常工作
  → 根据 SOUL.md 的人格与用户交互
  → 根据任务需要按需加载 SKILLS/ 和 PROJECTS/
  → ⚠️ 追加记忆后记得更新 MEMORY.md 头部的"条目数"

完整协议：[Relic项目路径]/docs/protocol.zh-CN.md
```

把 `[Relic的brain路径]` 替换成你的实际路径。常见路径：
- Linux/Mac: `/home/你的用户名/relic/brain` 或 `/Users/你的用户名/relic/brain`
- Windows (WSL): `/home/你的用户名/relic/brain`
- Windows (原生): `C:\Users\你的用户名\relic\brain`

💡 小技巧：如果你不确定路径，在终端里 `cd` 到 brain 目录，然后输入 `pwd`（Linux/Mac）或 `cd`（Windows）查看完整路径。

💡 建议把锚点加在配置文件的**开头**，这样 Agent 启动时最先读到。

## 第三步：验证

启动 OpenClaw，问它：
> "你读了我的 Relic 吗？告诉我我的 AI 叫什么名字、我叫什么名字。"

如果它能回答出来，说明接入成功。

## 日常使用

正常使用 OpenClaw 即可。它每次启动会自动读 Relic。
对话结束后，记得提醒 OpenClaw 把对话记录到 SESSIONS/（未来会自动化）。

## 权限提醒

- SOUL.md 和 USER.md：OpenClaw 只能读，不能改
- MEMORY.md：OpenClaw 只能在末尾追加
- SKILLS/ 和 PROJECTS/：OpenClaw 可以自由读写

# OpenClaw 的身份文件注意事项
- OpenClaw 的 IDENTITY.md → 合并到 SOUL.md 的补充段，Relic 没有 IDENTITY.md
