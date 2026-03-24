# 并行审查多个 GitHub PR

## 干什么
同时让多个 Codex 实例并行审查不同的 PR，大幅提升效率。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要安装：`codex` CLI、`gh` CLI
- 需要配置：OpenAI API Key、GitHub Token

### 2. 执行步骤

**给 OpenClaw 发送指令：**

```
帮我并行审查 user/repo 仓库的 PR #86、#87、#88
```

**OpenClaw 会执行：**

```bash
# 1. 获取所有 PR 引用
git fetch origin '+refs/pull/*/head:refs/remotes/origin/pr/*'

# 2. 启动多个 Codex 实例（并行执行）
bash pty:true workdir:~/project background:true command:"codex exec 'Review PR #86. git diff origin/main...origin/pr/86'"
bash pty:true workdir:~/project background:true command:"codex exec 'Review PR #87. git diff origin/main...origin/pr/87'"
bash pty:true workdir:~/project background:true command:"codex exec 'Review PR #88. git diff origin/main...origin/pr/88'"

# 3. 监控进度
process action:list

# 4. 获取审查结果
process action:log sessionId:XXX

# 5. 发布评论到 GitHub
gh pr comment 86 --body "$(cat review.md)"
```

### 3. 效果展示

```
启动了 3 个 Codex 实例...

✅ PR #86 审查完成
   - 发现 2 个潜在问题
   - 已发布评论

✅ PR #87 审查完成
   - 代码质量良好
   - 已发布评论

✅ PR #88 审查完成
   - 发现 1 个安全问题
   - 已发布评论

总耗时：5 分钟（串行需要 15 分钟）
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Codex CLI | OpenAI 代码助手 | `npm install -g @openai/codex` |
| gh CLI | GitHub 命令行 | `brew install gh` |
| OpenAI API Key | 调用 GPT 模型 | OpenAI 官网 |

## 注意事项

⚠️ **不要在 OpenClaw 自身的项目目录中审查 PR**，应克隆到临时目录：

```bash
REVIEW_DIR=$(mktemp -d)
git clone https://github.com/user/repo.git $REVIEW_DIR
cd $REVIEW_DIR && gh pr checkout 130
codex review --base origin/main
```

## 来源

- 贡献者：Community
- 来源：OpenClaw 技能文档
- 日期：2024

## 相关资源

- [Codex CLI 文档](https://github.com/openai/codex)
- [GitHub CLI 文档](https://cli.github.com)
