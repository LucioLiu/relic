# 手动设置指南

不需要 AI 帮忙，自己动手搞。

## 步骤

1. **打开 `brain/` 文件夹**（在下载的 `relic` 文件夹里面）

2. **复制模板文件**（模板文件名里有 `.template`，就是给你照着填的空表格）：
   - `SOUL.template.md` → 复制并改名为 `SOUL.md`
   - `USER.template.md` → 复制并改名为 `USER.md`
   - `MEMORY.template.md` → 复制并改名为 `MEMORY.md`

3. **用任何文本编辑器打开 `SOUL.md`**（记事本、TextEdit、VS Code 都行），至少填好「核心使命」部分

4. **打开 `USER.md`**，填上你的偏好

5. **（仅 Mac/Linux）锁定文件**防止误修改：
   ```
   chmod 444 SOUL.md USER.md
   ```
   意思是"给这两个文件上把锁"。以后你自己想改，先解锁就行。Windows 用户跳过。

6. **把你的 AI 工具指向** `AGENT.zh-CN.md`（中文）或 `AGENT.md`（英文）——它会接管剩下的

## 七大文件说明

| 文件 | 干什么 |
|------|--------|
| `SOUL.md` | AI 的灵魂——名字、性格、使命、风格 |
| `USER.md` | 你的信息——称呼、偏好、习惯 |
| `MEMORY.md` | 长期记忆——偏好、决策、经验（提炼过的知识，不是原始聊天） |
| `SKILLS/` | 技能——AI 学到的能力，每个技能一个文件夹 |
| `PROJECTS/` | 计划——正在进行或已完成的计划文档 |
| `SESSIONS/` | 对话日志——与 AI 的完整原始聊天记录 |
| `ARCHIVE/` | 归档——记忆太长时移到这里，永不删除 |

## 连接 AI 工具

| AI 工具 | 怎么连 |
|---------|--------|
| OpenClaw | 看 `examples/integrations/openclaw.zh-CN.md` |
| Hermes | 看 `examples/integrations/hermes.zh-CN.md` |
| Claude Code | 看 `examples/integrations/generic.zh-CN.md` |
| Cursor | 看 `examples/integrations/generic.zh-CN.md` |
| 其他 | 看 `examples/integrations/generic.zh-CN.md` |

所有工具的模式都一样：让 AI 读 `AGENT.zh-CN.md`，它自己搞定。

有问题？看 `docs/TROUBLESHOOTING.zh-CN.md`。
