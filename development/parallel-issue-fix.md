# 并行修复多个 GitHub Issues

## 干什么
使用 git worktree 创建多个工作目录，让多个 Codex 实例并行修复不同的 issues。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要安装：`codex` CLI、`gh` CLI
- 需要配置：OpenAI API Key、GitHub Token

### 2. 执行步骤

**给 OpenClaw 发送指令：**

```
帮我并行修复 issues #78 和 #99
```

**OpenClaw 会执行：**

```bash
# 1. 为每个 issue 创建 worktree
git worktree add -b fix/issue-78 /tmp/issue-78 main
git worktree add -b fix/issue-99 /tmp/issue-99 main

# 2. 在每个 worktree 中启动 Codex（并行执行）
bash pty:true workdir:/tmp/issue-78 background:true command:"pnpm install && codex --yolo 'Fix issue #78: <问题描述>. Commit and push.'"
bash pty:true workdir:/tmp/issue-99 background:true command:"pnpm install && codex --yolo 'Fix issue #99: <问题描述>. Commit and push.'"

# 3. 监控进度
process action:list
process action:log sessionId:XXX

# 4. 创建 PR
cd /tmp/issue-78 && git push -u origin fix/issue-78
gh pr create --repo user/repo --head fix/issue-78 --title "fix: ..." --body "..."

# 5. 清理 worktree
git worktree remove /tmp/issue-78
git worktree remove /tmp/issue-99
```

### 3. 效果展示

```
创建了 2 个 worktree...

✅ Issue #78 修复完成
   - 分支：fix/issue-78
   - PR：#101
   - 状态：等待审核

✅ Issue #99 修复完成
   - 分支：fix/issue-99
   - PR：#102
   - 状态：等待审核

总耗时：8 分钟（串行需要 20 分钟）
```

## 为什么用 worktree？

| 方式 | 优点 | 缺点 |
|------|------|------|
| 多个 clone | 完全隔离 | 占用双倍磁盘 |
| **git worktree** | 共享 .git，省空间 | 需要管理 worktree |

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Codex CLI | OpenAI 代码助手 | `npm install -g @openai/codex` |
| gh CLI | GitHub 命令行 | `brew install gh` |
| OpenAI API Key | 调用 GPT 模型 | OpenAI 官网 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 技能文档
- 日期：2024

## 相关资源

- [Git Worktree 文档](https://git-scm.com/docs/git-worktree)
- [Codex CLI 文档](https://github.com/openai/codex)
