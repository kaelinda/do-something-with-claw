# GitHub 操作自动化

## 真实来源

- **技能**：github
- **CLI**：GitHub CLI (`gh`)
- **安装**：`brew install gh`

---

## 干什么
通过 OpenClaw 自动化 GitHub 操作，包括 Issue 管理、PR 处理、CI 监控等。

## 怎么干

### 1. 准备工作

```bash
# 安装 GitHub CLI
brew install gh

# 认证（一次性）
gh auth login

# 验证
gh auth status
```

### 2. 执行步骤

**方式一：Issue 管理**

```
列出仓库的所有 Open Issues：
- 仓库：owner/repo
- 状态：open
- 输出：编号 + 标题 + 标签
```

```
创建一个新 Issue：
- 标题：Bug: 登录页面加载缓慢
- 内容：描述问题、复现步骤、预期行为
- 标签：bug, high-priority
```

**方式二：PR 操作**

```
查看 PR 详情：
- PR 编号：55
- 仓库：owner/repo
- 显示：标题、状态、CI 结果、变更文件
```

```
创建 PR：
- 标题：feat: 添加用户仪表板
- 内容：变更说明、测试计划
- 分支：feature/dashboard → main
```

**方式三：CI/工作流监控**

```
查看最近的 CI 运行：
- 仓库：owner/repo
- 限制：最近 10 次
- 显示：状态、触发者、时长
```

```
查看失败的 CI 日志：
- Run ID：12345
- 只显示失败步骤
```

**方式四：API 查询**

```
查询仓库统计：
- 仓库：owner/repo
- 输出：Stars、Forks、Issues 数量
```

### 3. 常用命令

```bash
# ===== Issue 操作 =====
# 列出 Issues
gh issue list --repo owner/repo --state open

# 创建 Issue
gh issue create --title "Bug: something broken" --body "Details..."

# 关闭 Issue
gh issue close 42 --repo owner/repo

# ===== PR 操作 =====
# 列出 PRs
gh pr list --repo owner/repo

# 查看 PR 详情
gh pr view 55 --repo owner/repo

# 查看 CI 状态
gh pr checks 55 --repo owner/repo

# 创建 PR
gh pr create --title "feat: add feature" --body "Description"

# 合并 PR
gh pr merge 55 --squash --repo owner/repo

# ===== CI/工作流 =====
# 列出最近的运行
gh run list --repo owner/repo --limit 10

# 查看特定运行
gh run view <run-id> --repo owner/repo

# 只查看失败步骤日志
gh run view <run-id> --repo owner/repo --log-failed

# 重新运行失败的任务
gh run rerun <run-id> --failed --repo owner/repo

# ===== API 查询 =====
# JSON 输出
gh issue list --repo owner/repo --json number,title --jq '.[] | "\(.number): \(.title)"'

# 获取仓库信息
gh api repos/owner/repo --jq '{stars: .stargazers_count, forks: .forks_count}'
```

### 4. 效果展示

```
GitHub 操作完成！

Issue 列表（5 个 Open）：
#123: 修复登录页面样式问题 - bug, ui
#122: 添加暗色模式支持 - feature, enhancement
#121: 文档更新：API 接口说明 - docs
#120: 性能优化：首页加载时间 - performance
#119: 修复移动端适配问题 - bug, mobile

PR 详情：
- 标题：feat: 用户仪表板
- 作者：developer
- 状态：Open
- CI：✅ All checks passed
- 变更：+234 -56，8 files

CI 运行状态：
- Run #456: ✅ Success (main, 5 min ago)
- Run #455: ❌ Failed (feature/auth, 1 hour ago)
- Run #454: ✅ Success (main, 2 hours ago)
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| gh | GitHub CLI | `brew install gh` |
| GitHub 账号 | 有仓库权限 | GitHub 注册 |

## 相关资源

- [GitHub CLI 文档](https://cli.github.com/manual)
- [gh auth login](https://cli.github.com/manual/gh_auth_login)
- OpenClaw 技能：github
