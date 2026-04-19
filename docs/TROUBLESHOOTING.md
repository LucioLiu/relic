# 🔧 故障排查 / Troubleshooting

> 躯壳或用户遇到问题时，先看这里。
> When something goes wrong, check here first.

---

## 躯壳不读 Relic / Agent doesn't read Relic

**症状**：躯壳不记得你的 AI 名字、不记得你的偏好，好像从来没读过 SOUL.md。

**原因**：躯壳的核心配置里没有锚点（或锚点被清除了）。

**解决**：
1. 检查躯壳的核心配置文件（OpenClaw 看 AGENTS.md，Claude Code 看 CLAUDE.md 等）
2. 确认里面有 ⚡ Relic 灵魂芯片的锚点文字
3. 如果没有，参考 `examples/integrations/` 里对应躯壳的接入指南重新植入
4. 植入后重新启动躯壳

**预防**：躯壳升级/重装后可能会清空配置。升级后记得检查锚点还在不在。

---

## SOUL.md 被躯壳改了 / SOUL.md was modified by agent

**症状**：SOUL.md 的内容和之前不一样了。

**解决**：
1. 立即停止躯壳的当前操作
2. 如果项目在 git 管理下：`git checkout SOUL.md` 恢复
3. 如果没有 git：检查 ARCHIVE/ 里有没有备份
4. 如果都没有：手动修正 SOUL.md
5. 修正后检查躯壳的配置，确认锚点文字还在（锚点里有权限规则提醒）

---

## 记忆文件丢失 / Memory file missing

**症状**：MEMORY.md 不见了或变空了。

**解决**：
1. 检查 ARCHIVE/ 目录——可能上次整理时被移到了那里
2. 查看 ARCHIVE/index.md 找到最新的归档文件
3. 如果找到了：把归档内容复制回 MEMORY.md
4. 如果 ARCHIVE/ 里也没有：检查 git 历史或文件系统回收站

---

## 对话记录没被保存 / Sessions not recorded

**症状**：SESSIONS/ 里没有上次的对话记录。

**解决**：
1. 这需要躯壳主动写入。如果躯壳忘了，对话结束后跟它说：
   "请把今天的对话记录到 SESSIONS/2026-04/2026-04-16.[躯壳名].md"
2. 躯壳会追加完整对话到指定文件

**预防**：每天结束前养成提醒躯壳的习惯，或等 Phase 2 的自动化工具。

---

## 记忆太多躯壳记不住 / Too many memories, agent forgets

**症状**：躯壳说"我不记得你说过这个"，但你确实之前告诉过它。

**原因**：MEMORY.md 超过了躯壳读取的末尾 20 条范围。

**解决**：
1. 告诉躯壳："请在 MEMORY.md 全文里搜索 [关键词]"
2. 如果 MEMORY.md 太大（超过 16K tokens），需要整理——参考 docs/protocol.md 第七节
3. 整理后 MEMORY.md 会变短，关键信息被保留

---

## 换了新 Agent 怎么接入 / Switching to a new agent

**步骤**：
1. 查看新 Agent 的接入指南（`examples/integrations/` 目录）
2. 在新 Agent 的核心配置里植入锚点
3. 启动新 Agent，它会自动读取 Relic
4. MEMORY.md 里之前其他躯壳写的记忆，新躯壳同样会参考

---

## 如何断开 / How to Disconnect

**想停用 Relic？**

1. 删除躯壳核心配置里的锚点文字（AGENTS.md / CLAUDE.md / WORK_RULES.md 里的 `⚡ Relic 灵魂芯片` 区块）
2. 躯壳下次启动就不会再读 Relic 了
3. Relic 文件不会被自动删除——SOUL.md、MEMORY.md 等都还在
4. 想彻底清理：删除整个 `brain/` 目录即可（建议先备份）

**临时停用**：只删锚点就行，文件保留着，以后想恢复再植入锚点。

---

## 只有模板文件没有正式文件 / Only templates, no active files

**问题**：目录里只有 `SOUL.template.md`，没有 `SOUL.md`。

**解决**：
```
复制 SOUL.template.md → 改名为 SOUL.md
复制 USER.template.md → 改名为 USER.md
复制 MEMORY.template.md → 改名为 MEMORY.md
```

用文件管理器或命令行都行。躯壳读的是 SOUL.md（不带 template）。

---

## 想编辑 SOUL.md 或 USER.md 但权限是只读 / Want to edit read-only files

**问题**：设置了 `chmod 444 SOUL.md USER.md` 后，自己编辑也改不了。

**解决**：
```bash
chmod 644 SOUL.md USER.md    # 开启写权限
# 用编辑器修改...
chmod 444 SOUL.md USER.md    # 改回只读
```

> 💡 v0.2.0 起：躯壳可以丰富 SOUL.md 和 USER.md 的内容（新增习惯、偏好等），只有核心字段（名字、使命、用户称呼）受保护。如果躯壳需要改内容，不需要解除权限——它会在你允许的范围内自动丰富。

躯壳不会自动执行 `chmod`，所以需要用户手动操作。如果躯壳需要修改非核心内容，它会自行追加，不需要解除文件权限。

---

## 路径里怎么写 / What path to use

锚点里的路径取决于你把 Relic 放在哪里：

| 系统 System | 示例路径 Example path |
|------------|---------------------|
| Linux | `/home/你的用户名/relic/brain` |
| macOS | `/Users/你的用户名/relic/brain` |
| Windows (WSL) | `/home/你的用户名/relic/brain` |
| Windows (原生) | `C:\Users\你的用户名\relic\brain` |

把路径替换到锚点文字里的 `[brain路径]`。

---

## 多设备同步 / Multi-device Sync

**问题**：我在两台电脑上用 Relic，怎么同步？

**方案**：
1. **推荐：Git 同步** / Recommended: Git sync
   - 把 Relic 目录放在 Git 仓库里
   - 每次结束使用后 `git add . && git commit -m "sync" && git push`
   - 在另一台机器上 `git pull`
   - ⚠️ 注意：确保 `.gitignore` 排除敏感信息（SOUL.md、USER.md 可能包含私密内容）

2. **云盘同步** / Cloud drive sync
   - 把 Relic 目录放在 OneDrive/Dropbox/坚果云等同步盘里
   - 注意：不要两台机器同时写入 MEMORY.md（append-only 可以降低风险）

3. **手动拷贝** / Manual copy
   - 用 U 盘或网络共享拷贝整个 brain/ 目录

**注意**：MEMORY.md 是 append-only，多设备追加通常不会冲突。
但如果同时修改了 SKILLS/ 或 PROJECTS/，需要手动合并。

---

## 模型上下文太小 / Model Context Too Small

**问题**：PROTOCOL 默认 200/400 行整理阈值，但我的模型只有 4K 上下文。

**方案**：
如果模型上下文较小（4K-8K），把阈值调低：
- 整理提醒阈值：200 行 → **50 行**
- 强制整理阈值：400 行 → **100 行**
- 在锚点里直接把数字改掉就行，PROTOCOL 的数字是默认值，可以在锚点中自定义

---

## 找不到答案 / Can't find the answer

1. 重新阅读 `docs/protocol.md`——大部分问题在协议里都有说明
2. 查看 `examples/example-brain/`——看示例是怎么填的
3. 在 GitHub 上提 Issue
