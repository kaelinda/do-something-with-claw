# Do Something with Claw

> 收集大家用 OpenClaw 做什么的开源仓库。

## 快速导航

### 🤖 自动化 (4 个)
- [自动收集 GitHub 主题](automation/collect-github-themes.md) - 让 OpenClaw 自动搜索下载开源主题
- [每日自动写日记](automation/mirror-daily-diary.md) - 创建每天午夜自动写日记的 Agent
- [博客/RSS 监控更新](automation/blog-watcher.md) - 监控博客和 RSS 源的更新
- [自动更新 Clawdbot 和技能](automation/auto-updater.md) - 定时自动更新到最新版本

### ✍️ 内容创作 (1 个)
- [自动生成自媒体内容](content-creation/auto-generate-content.md) - 支持公众号、小红书、抖音文案

### 💻 开发辅助 (5 个)
- [使用 Codex 自动编写代码](development/codex-coding.md) - 让 OpenAI Codex 自动编写代码、修复 bug
- [使用 Claude Code 自动编写代码](development/claude-code-coding.md) - 让 Anthropic Claude 自动编写代码
- [并行审查多个 GitHub PR](development/parallel-pr-review.md) - 多个 Codex 实例并行审查 PR
- [并行修复多个 GitHub Issues](development/parallel-issue-fix.md) - 使用 git worktree 并行修复
- [自动审查 GitHub Issues 并提交 PR](development/auto-review-issues.md) - 自动修复 bug 并提交

### 📊 数据分析 (2 个)
- [数据报告生成](data-analysis/data-report.md) - 自动生成数据分析报告
- [日志分析](data-analysis/log-analysis.md) - 分析系统日志并提取关键信息

### 👤 个人助理 (3 个)
- [每日总结报告生成](personal-assistant/daily-summary-report.md) - 每天 23:00 自动生成工作总结
- [邮件草稿生成](personal-assistant/email-draft.md) - 快速生成专业邮件草稿
- [会议纪要整理](personal-assistant/meeting-minutes.md) - 自动整理会议记录

### 📚 学习辅助 (5 个)
- [笔记整理与知识管理](learning/note-organize.md) - 使用 Obsidian 整理笔记
- [论文/文章摘要生成](learning/paper-summary.md) - 快速提取论文要点
- [代码学习与解释](learning/code-learning.md) - 帮助理解复杂代码
- [塑造 Agent 的灵魂（SOUL.md）](learning/soul-shaping.md) - 定义 Agent 的性格、特质、风格
- [创建不同角色的 Agent](learning/create-agent-roles.md) - 产品经理、开发者、分析师等

### 🔧 工具集成 (3 个)
- [飞书文档操作](tools/feishu-integration.md) - 读写飞书文档、多维表格
- [Obsidian 笔记操作](tools/obsidian-integration.md) - 自动化笔记管理
- [浏览器自动化](tools/browser-automation.md) - 自动打开网页、截图、填表

---

## 目录结构

```
├── automation/          # 自动化场景
│   ├── daily-report/    # 每日报告
│   ├── content-sync/    # 内容同步
│   └── ...
├── content-creation/    # 内容创作
│   ├── blog-writing/    # 博客写作
│   ├── translation/     # 翻译
│   └── ...
├── development/         # 开发辅助
│   ├── code-review/     # 代码审查
│   ├── pr-management/   # PR 管理
│   └── ...
├── data-analysis/       # 数据分析
├── personal-assistant/  # 个人助理
├── learning/            # 学习辅助
└── tools/               # 工具集成
```

## 如何贡献

### 1. 选择目录
根据你的使用场景，选择合适的目录分类。

### 2. 创建案例文件
每个案例一个 Markdown 文件，文件名用英文小写+连字符，如 `daily-standup-report.md`。

### 3. 填写模板

```markdown
# [案例名称]

## 干什么
<!-- 一句话描述你要做的事 -->

## 怎么干
<!-- 具体步骤、配置、命令等 -->

### 1. 准备工作
- 需要 OpenClaw 版本：x.x.x
- 需要的技能/插件：
- 需要的配置：

### 2. 执行步骤
1. 
2. 
3. 

### 3. 效果展示
<!-- 截图、日志、输出示例 -->

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= x.x.x | 官方安装 |
| xxx | xxx | xxx |

## 来源

- 贡献者：[你的名字]
- 来源：[原始链接/讨论/灵感]
- 日期：YYYY-MM-DD

## 相关资源

- [相关文档]()
- [相关技能]()
- [相关讨论]()
```

### 4. 提交 PR
1. Fork 本仓库
2. 创建分支：`git checkout -b feature/your-case-name`
3. 提交更改：`git commit -m 'feat: 添加 xxx 案例'`
4. 推送分支：`git push origin feature/your-case-name`
5. 创建 Pull Request

## 分类说明

| 分类 | 说明 | 示例 |
|------|------|------|
| automation | 自动化场景 | 定时报告、自动同步、监控告警 |
| content-creation | 内容创作 | 博客写作、翻译、文案生成 |
| development | 开发辅助 | 代码审查、PR 管理、CI/CD |
| data-analysis | 数据分析 | 数据清洗、报告生成、可视化 |
| personal-assistant | 个人助理 | 日程管理、邮件处理、备忘录 |
| learning | 学习辅助 | 笔记整理、知识问答、学习计划 |
| tools | 工具集成 | 第三方服务集成、API 调用 |

## 许可证

MIT License

---

**OpenClaw**: https://github.com/openclaw/openclaw
**文档**: https://docs.openclaw.ai
**社区**: https://discord.com/invite/clawd
