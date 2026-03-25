# 自动审查 GitHub Issues 并提交 PR

## 真实来源

- **技能**：gh-issues
- **位置**：`/opt/homebrew/lib/node_modules/openclaw/skills/gh-issues/`
- **能力**：拉取 Issues → 分析问题 → 生成修复代码 → 提交 PR → 监控审核评论

---

## 干什么
让 OpenClaw 自动拉取 GitHub Issues，分析问题，生成修复代码，并提交 PR。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：`gh-issues` 技能
- 需要的配置：GitHub Token (GH_TOKEN)

### 2. 执行步骤

**使用技能命令：**

```bash
# 拉取指定仓库的 bug 标签 Issues
/gh-issues owner/repo --label bug --limit 5

# 使用特定模型
/gh-issues owner/repo --label bug --model glm-5

# 持续监控模式
/gh-issues owner/repo --watch --interval 10

# 只处理 PR 审核评论
/gh-issues owner/repo --reviews-only

# 定时任务模式
/gh-issues owner/repo --cron --notify-channel -1002381931352
```

**OpenClaw 会自动：**
1. 拉取指定仓库的 Issues
2. 分析问题描述
3. 生成修复代码
4. 创建分支并提交
5. 打开 PR
6. 监控 PR 审核评论
7. 根据反馈修改代码

### 3. 效果展示

```
✅ Issue #123 已修复
   - 分支：fix/issue-123
   - PR：#456
   - 状态：等待审核

✅ Issue #124 已修复
   - 分支：fix/issue-124
   - PR：#457
   - 状态：已合并
```

## 技能工作流程

gh-issues 技能遵循 6 个阶段：

| 阶段 | 说明 |
|------|------|
| Phase 1 | 解析参数（仓库、标签、限制等） |
| Phase 2 | 获取 Issues（通过 GitHub REST API） |
| Phase 3 | 展示并确认 |
| Phase 4 | 预检查（工作树、远程访问、Token 等） |
| Phase 5 | 并行生成子代理修复 Issue |
| Phase 6 | PR 审核处理（自动回应审核评论） |

## 常用参数

| 参数 | 说明 | 默认值 |
|------|------|--------|
| `--label` | 按标签筛选 | 无 |
| `--limit` | 最大处理数量 | 10 |
| `--milestone` | 按里程碑筛选 | 无 |
| `--assignee` | 按指派人筛选 | 无 |
| `--fork` | 使用 Fork 模式 | 无 |
| `--watch` | 持续监控模式 | false |
| `--interval` | 监控间隔（分钟） | 5 |
| `--dry-run` | 只展示不执行 | false |
| `--cron` | 定时任务模式 | false |
| `--model` | 子代理使用的模型 | 默认模型 |
| `--notify-channel` | Telegram 通知频道 | 无 |

## Fork 模式

如果你没有目标仓库的写权限，可以使用 Fork 模式：

```bash
# 指定你的 Fork 仓库
/gh-issues owner/source-repo --fork your-username/your-fork
```

- Issues 从源仓库拉取
- 分支推送到你的 Fork
- PR 从 Fork 提交到源仓库

## 持续监控模式

启用 `--watch` 后，技能会持续运行：

```bash
/gh-issues owner/repo --watch --interval 10
```

每隔 10 分钟检查：
1. 新的符合条件的 Issues
2. 已创建 PR 的新审核评论
3. 自动处理审核反馈

## 定时任务模式

使用 `--cron` 进行定时任务调度：

```bash
/gh-issues owner/repo --cron --notify-channel -1002381931352
```

- 自动处理单个 Issue（按顺序）
- 完成后退出（不等待结果）
- 可通过 OpenClaw cron 调度

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| GitHub Token | GH_TOKEN | GitHub Settings → Developer Settings |
| gh-issues 技能 | 自动处理 Issues | OpenClaw 内置技能 |

## 来源

- **技能路径**：`/opt/homebrew/lib/node_modules/openclaw/skills/gh-issues/SKILL.md`
- **能力**：使用 curl + GitHub REST API（不依赖 gh CLI）

## 相关资源

- [gh-issues 技能文档](https://openclaw.ai/skills/gh-issues)
- [并行修复多个 Issues](development/parallel-issue-fix.md)
- [GitHub 集成](tools/github-integration.md)
