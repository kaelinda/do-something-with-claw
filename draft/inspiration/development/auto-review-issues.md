# 自动审查 GitHub Issues 并提交 PR

## 干什么
让 OpenClaw 自动拉取 GitHub Issues，分析问题，生成修复代码，并提交 PR。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：`gh-issues` 技能
- 需要的配置：GitHub Token

### 2. 执行步骤

**给 OpenClaw 发送指令：**

```
审查 openclaw/openclaw 仓库的 bug 标签 Issues：
- 限制：5 个
- 自动生成修复代码
- 提交 PR
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

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| GitHub Token | 仓库访问权限 | GitHub Settings |
| gh-issues 技能 | 自动处理 Issues | ClawHub 安装 |

## 来源

- 贡献者：Community
- 来源：gh-issues 技能文档
- 日期：2024

## 相关资源

- [gh-issues 技能](https://clawhub.com/skills/gh-issues)
- [OpenClaw 文档](https://docs.openclaw.ai)
