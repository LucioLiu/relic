<!-- Relic 灵魂芯片 · 导入执行手册 | 作者：LucioLiu | 许可证：GPL v3 | 版本：1.2.0 -->

# 导入执行手册 / Import Execution Guide

## ⚡ 导入铁律

> 🔴 **七大记忆文件，缺一不可：**
> 1.`SOUL.md` 2.`USER.md` 3.`MEMORY.md` 4.`SKILLS/` 5.`PROJECTS/` 6.`SESSIONS/` 7.`ARCHIVE/`
>
> - 必须处理全部 7 类，即使某类为空也要报告
> - "没有数据" ≠ "可以跳过" → 必须报告"N类：0条"
> - 禁止省略任何类别，禁止编造数据

## 📋 强制：先输出计划再执行

导入前**必须**输出以下计划，等用户确认后执行：

```
导入计划：
- SOUL.md：[动作]
- USER.md：[动作]
- MEMORY.md：[动作]
- SKILLS/：[动作]
- PROJECTS/：[动作]
- SESSIONS/：[动作]
- ARCHIVE/：[动作]
```

## 步骤 1：扫描 + 确认

扫描所有持久化存储，按类别列清单。向用户问两个问题：
1. "以上是否全部导入？或选择性导入？"
2. "有没有遗漏的数据源？"

⚠️ 必须等用户确认后才开始。

❌ `我没有找到任何旧数据。`
✅ `扫描：灵魂2文件 | 记忆42条 | 技能3个 | 对话0 | 项目5个 | 归档8个。以上是否全部导入？`

## 步骤 2：SOUL + USER

🔴 **保真铁律：直接复制原文，不要概括重写。** 模板放不下的放"其它/Other"，**绝不丢弃**。原文归档到 `ARCHIVE/raw/`。

❌ `用户偏好：喜欢简洁代码风格` ← 压缩重写
✅ `用户偏好：代码风格偏好函数式非OOP，框架讨厌Spring全家桶，命名禁止拼音缩写` ← 逐字保留

## 步骤 3：MEMORY

❌ `## 工作习惯` + `- 常熬夜工作` ← 用分类名做标题
✅ `## 2026-04-19 [OpenClaw-常]` + `内容：常熬夜...` / `类型：偏好` / `重要度：中` ← 用日期+躯壳名

| 类型 | 精度要求 |
|------|---------|
| 偏好 / 决策 / 更正 | **必须逐字保留** |
| 经验 | 可精简，关键参数/路径不能丢 |
| 事件 | 可摘要 |
| 情绪 | 可精简背景 |

敏感信息：旧躯壳已有的→可迁移 | 新发现的密码/手机号等→**必须先问用户**
写入后：数 `##` 标题数，更新头部"条目数"和"更新时间"。

## 步骤 4：SKILLS

每技能一个文件夹，内含至少一个 `.md`。只搬用户创建的技能文件和有文档的方法论，不搬对话经验或AI概括。

❌ `SKILLS/skills-list.md` ← 平铺清单
✅ `SKILLS/debugging-workflow/README.md` ← 文件夹结构

## 步骤 5：SESSIONS

问用户旧对话位置。完整保存，禁止摘要。当前会话≠旧对话。
无旧对话→报告"0条（用户确认无旧对话）"，仍创建 `SESSIONS/YYYY-MM/` 目录。

## 步骤 6：PROJECTS

每个项目问用户导入什么。一个项目一个文件夹，内有实质内容。

❌ `PROJECTS/my-app/README.md` → "这是我的项目" ← 一句话
✅ `PROJECTS/my-app/` 含 README.md + api-design.md + notes.md ← 实质内容

## 步骤 7：归档 + 汇报

`INBOX/` → `ARCHIVE/raw/`。**必须逐项汇报 7 个类别**（含"0条"）：

```
1. SOUL.md：已导入  2. USER.md：已导入  3. MEMORY.md：N条
4. SKILLS/：N个  5. SESSIONS/：N个  6. PROJECTS/：N个  7. ARCHIVE/：N个已归档
```
省略任何类别 = 失败。

## 🔴 最后自检

七大类别：SOUL.md、USER.md、MEMORY.md、SKILLS/、PROJECTS/、SESSIONS/、ARCHIVE/

- ☐ 处理了全部 7 类？
- ☐ MEMORY 格式是 `## 日期 [躯壳名]`？（`## 类别名` = ❌）
- ☐ SKILLS 是文件夹？（单个 .md 平铺 = ❌）
- ☐ 问了用户旧对话位置？
- ☐ 问了用户每个项目导入内容？
- ☐ 7 类全部出现在汇报中？

## 植入锚点

导入完成后植入锚点到躯壳配置文件，指向 BOOT.md：

```markdown
## ⚡ Relic 灵魂芯片 / Soul Chip
> 这是 Relic 的接入声明。要停用？删除这段文字即可。
你已接入 Relic 灵魂芯片。每次新对话开始时，读取并执行：
📄 **[brain路径]/BOOT.md**
⚠️ 首次连接？→ 读 [brain路径]/IMPORT.md
⚠️ SOUL.md 人格与默认冲突时，以 SOUL.md 为准。
完整协议：[brain路径]/PROTOCOL.md
```

白名单：OpenClaw→AGENTS.md | Claude Code→CLAUDE.md | Hermes→配置文件 | OpenCode→WORK_RULES | Cursor→.cursorrules。植入前须获用户许可。

详细规则见 PROTOCOL.md
