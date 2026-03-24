# Git 操作自动化

## 干什么
使用 OpenClaw 自动化 Git 操作，包括自动提交、分支管理、冲突解决等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要 Git 配置（用户名、邮箱）
- 需要 GitHub CLI（gh）或 Git

### 2. 执行步骤

#### 方式一：自动提交
```
用户：帮我提交当前的更改，提交信息写"优化代码结构"
OpenClaw：[执行 git add] → [git commit] → [git push]
✅ 提交成功！
Commit: abc1234
```

#### 方式二：批量操作
```bash
# 查看仓库状态
openclaw exec git status

# 查看提交历史
openclaw exec git log --oneline -10

# 创建新分支
openclaw exec git checkout -b feature/new-feature
```

### 3. 效果展示

**自动化提交流程：**
```
1. 检查当前状态（git status）
2. 暂存更改（git add）
3. 创建提交（git commit -m "message"）
4. 推送到远程（git push）
```

## 常用操作

### 1. 日常提交
```bash
# 查看更改
git status

# 暂存所有更改
git add .

# 提交
git commit -m "feat: 添加新功能"

# 推送
git push origin main
```

### 2. 分支管理
```bash
# 创建并切换分支
git checkout -b feature/xxx

# 查看所有分支
git branch -a

# 合并分支
git merge feature/xxx

# 删除分支
git branch -d feature/xxx
```

### 3. 撤销操作
```bash
# 撤销工作区更改
git checkout -- file.txt

# 撤销暂存
git reset HEAD file.txt

# 撤销最后一次提交（保留更改）
git reset --soft HEAD~1
```

### 4. 解决冲突
```bash
# 查看冲突文件
git diff --name-only --diff-filter=U

# 标记为已解决
git add resolved-file.txt

# 继续合并
git commit
```

## 高级用法

### 1. 智能提交信息
```javascript
// 根据更改自动生成提交信息
const changes = await git.diff();
const message = await generateCommitMessage(changes);

// conventional commits 格式
// feat: 新功能
// fix: 修复 bug
// docs: 文档更新
// style: 代码格式
// refactor: 重构
// test: 测试
// chore: 构建/工具
```

### 2. 自动化工作流
```javascript
// 代码更改后自动提交
watch.onFileChange("./src", async (file) => {
  await git.add(file);
  await git.commit(`chore: update ${file}`);
  await git.push();
});
```

### 3. 批量仓库操作
```bash
# 更新所有子模块
git submodule update --init --recursive

# 批量更新多个仓库
for repo in ~/projects/*; do
  cd $repo && git pull
done
```

### 4. Git Worktree 并行开发
```bash
# 创建 worktree
git worktree add ../feature-a feature/a
git worktree add ../feature-b feature/b

# 在不同目录并行开发
cd ../feature-a && npm test &
cd ../feature-b && npm test &

# 完成后清理
git worktree remove ../feature-a
```

## 与 GitHub/GitLab 集成

### 使用 gh CLI
```bash
# 创建 PR
gh pr create --title "新功能" --body "描述"

# 查看仓库信息
gh repo view

# 创建 Issue
gh issue create --title "Bug 报告" --body "描述"
```

### CI/CD 集成
```yaml
# .github/workflows/auto-commit.yml
name: Auto Commit
on:
  schedule:
    - cron: '0 0 * * *'
jobs:
  commit:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: ./update-script.sh
      - run: |
          git config user.name "Bot"
          git config user.email "bot@example.com"
          git add .
          git commit -m "chore: auto update"
          git push
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Git | 版本控制 | 系统安装 |
| GitHub CLI | 可选 | `brew install gh` |

## 最佳实践

### 提交信息规范
```
<type>(<scope>): <subject>

<body>

<footer>
```

示例：
```
feat(auth): 添加 OAuth 登录功能

- 支持 GitHub OAuth
- 支持 Google OAuth
- 添加登录状态持久化

Closes #123
```

### 分支命名规范
```
feature/xxx  - 新功能
bugfix/xxx   - 修复 bug
hotfix/xxx   - 紧急修复
release/x.x  - 发布分支
```

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [Pro Git 书籍](https://git-scm.com/book)
- [GitHub CLI 文档](https://cli.github.com/manual/)
- [Conventional Commits](https://www.conventionalcommits.org/)
