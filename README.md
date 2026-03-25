# Do Something with Claw

> 收集大家用 OpenClaw 做什么的真实案例仓库。

## ⚠️ 项目质量承诺

本仓库**只收录有真实来源的案例**：
- 真实开源项目
- 真实技能文档
- 真实可验证的命令或配置

不接受"空想案例"或"想象中的用法"。

---

## 快速导航

### ✍️ 内容创作 (1 个完整工作流 + 6 个案例)

#### Agent Teams 自动写小说
基于 GitHub 开源项目整理的完整多 Agent 小说写作工作流：

| 文档 | 说明 |
|------|------|
| [真实开源案例](content-creation/agent-teams-novel-writing.md) | 基于 Claude-Book 和 CoLong-Idea-Studio |
| [OpenClaw 可执行方案](content-creation/openclaw-agent-teams-novel-workflow.md) | 主 Agent + 4 子 Agent 工作流 |
| [Prompt 模板](content-creation/prompts/chapter-planner.md) | 章节规划、正文写作、人物审查、连续性审查 |
| [输出模板](content-creation/templates/outline-template.md) | 大纲、审查、状态回写模板 |
| [总控编排](content-creation/orchestrator/novel-master-agent.md) | 主 Agent 调度流程 |

#### 其他
| 案例 | 来源 | 说明 |
|------|------|------|
| [自动生成自媒体内容](content-creation/auto-generate-content.md) | viral-writer 技能 | 小红书、公众号、抖音文案 |
| [翻译与多语言内容](content-creation/translation.md) | gemini 技能 | 内容翻译、多语言适配 |
| [视频脚本生成](content-creation/video-script.md) | OpenClaw + tts | 短视频、教学视频脚本 |
| [播客脚本生成](content-creation/podcast-script.md) | OpenClaw + tts | 单口、访谈播客脚本 |
| [长文写作](content-creation/long-form-writing.md) | OpenClaw + gemini | 技术文章、分析报告 |
| [SEO 优化内容](content-creation/seo-optimization.md) | OpenClaw + gemini | 关键词优化、Meta 描述 |

---

### 💻 开发辅助 (8 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [使用 Codex 自动编写代码](development/codex-coding.md) | Codex CLI | 真实命令行工具 |
| [使用 Claude Code 自动编写代码](development/claude-code-coding.md) | Claude Code CLI | 真实命令行工具 |
| [自动审查 GitHub Issues 并提交 PR](development/auto-review-issues.md) | gh-issues 技能 | 自动修复 Issues |
| [并行修复多个 GitHub Issues](development/parallel-issue-fix.md) | git worktree + Codex | 可验证的命令 |
| [并行审查多个 GitHub PR](development/parallel-pr-review.md) | Codex + gh CLI | 可验证的命令 |
| [Git 操作自动化](development/git-operations.md) | git CLI + gh CLI | 提交、分支管理、冲突解决 |
| [Docker 操作自动化](development/docker-operations.md) | Docker CLI | 镜像构建、容器管理 |
| [CI/CD 集成](development/cicd-integration.md) | GitHub Actions / GitLab CI | 构建测试部署流水线 |

---

### 🎨 AI 能力 (6 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [图像生成](ai-capabilities/image-generation.md) | openai-image-gen skill | OpenClaw 内置技能 |
| [DALL-E 图像生成详解](ai-capabilities/image-generation-dalle.md) | OpenAI Images API | DALL-E 3 使用指南 |
| [语音合成](ai-capabilities/speech-synthesis.md) | 内置 tts 工具 | OpenClaw 内置工具 |
| [语音转文字](ai-capabilities/speech-to-text.md) | Whisper CLI | 本地运行，无需 API Key |
| [视频帧提取](ai-capabilities/video-frames.md) | video-frames skill | 真实脚本命令 |
| [视频处理](ai-capabilities/video-processing.md) | video-frames skill | 真实技能文档 |

---

### 🔧 工具集成 (23 个)

#### IM 即时通讯 (11 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [飞书消息发送](tools/feishu-message.md) | message 工具 | 飞书 Bot API |
| [飞书文档操作](tools/feishu-integration.md) | feishu 技能组 | 文档、多维表格、知识库 |
| [企业微信消息发送](tools/wechat-work-integration.md) | message 工具 | 企业微信 API |
| [Slack 消息发送](tools/slack-integration.md) | slack 技能 | Slack Bot |
| [Discord 机器人集成](tools/discord-integration.md) | discord 技能 | Discord Bot |
| [Discord 机器人高级操作](tools/discord-bot.md) | discord 技能 | 投票、状态、线程等 |
| [Telegram 机器人集成](tools/telegram-integration.md) | message 工具 | Telegram Bot API |
| [iMessage/SMS 消息发送](tools/imessage-integration.md) | imsg 技能 | macOS 专属 |
| [WhatsApp 消息发送](tools/whatsapp-integration.md) | message 工具 | WhatsApp Business API |
| [Signal 消息发送](tools/signal-integration.md) | message 工具 | Signal 协议 |
| [Line 消息发送](tools/line-integration.md) | message 工具 | LINE Messaging API |

#### 社交媒体 (3 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [Twitter/X 发推集成](tools/twitter-integration.md) | xurl 技能 | X API v2 |
| [小红书内容发布](tools/xiaohongshu-integration.md) | xiaohongshu 技能 | 小红书 MCP |
| [GitHub 操作自动化](tools/github-integration.md) | github 技能 | gh CLI |

#### 笔记与任务 (5 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [Obsidian 笔记操作](tools/obsidian-integration.md) | obsidian-cli 技能 | 真实 CLI 工具 |
| [Notion 笔记操作](tools/notion-integration.md) | notion 技能 | Notion API |
| [Apple Notes 笔记操作](tools/apple-notes-integration.md) | apple-notes 技能 | macOS 专属 |
| [Apple Reminders 任务管理](tools/apple-reminders-integration.md) | apple-reminders 技能 | macOS 专属 |
| [Things 3 任务管理](tools/things-integration.md) | things-mac 技能 | macOS 专属 |

#### 其他工具 (4 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [浏览器自动化](tools/browser-automation.md) | 内置 browser 工具 | Playwright 底层 |
| [天气查询](tools/weather-query.md) | weather 技能 | wttr.in |
| [邮件管理](tools/email-management.md) | himalaya 技能 | IMAP/SMTP |
| [Trello 卡片管理](tools/trello-integration.md) | trello 技能 | Trello REST API |

---

### ⚙️ 自动化 (4 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [博客/RSS 监控更新](automation/blog-watcher.md) | blogwatcher 技能 | Go 安装 |
| [自动更新 OpenClaw 和技能](automation/auto-updater.md) | auto-updater 技能 | ClawHub |
| [监控告警](automation/alert-monitoring.md) | healthcheck 技能 | 系统安全审计 |
| [定时备份](automation/scheduled-backup.md) | rsync + cron | 文件、数据库备份 |

---

### 👤 个人助理 (5 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [每日总结报告生成](personal-assistant/daily-summary-report.md) | OpenClaw 会话记录 | 用户真实需求 |
| [会议纪要自动生成](personal-assistant/meeting-minutes.md) | OpenClaw + 飞书 | 真实工作流 |
| [邮件草稿生成](personal-assistant/email-draft.md) | OpenClaw + himalaya | 商务邮件 |
| [习惯追踪](personal-assistant/habit-tracking.md) | apple-reminders + things-mac | 每日习惯管理 |
| [目标管理](personal-assistant/goal-management.md) | things-mac 技能 | SMART/OKR 目标管理 |

---

### 📊 数据分析 (3 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [日志分析](data-analysis/log-analysis.md) | exec + jq | 内置工具 |
| [数据报告生成](data-analysis/data-report.md) | exec + jq + gemini | CSV/JSON 分析 |
| [数据清洗](data-analysis/data-cleaning.md) | jq + sed/awk | 缺失值、去重、格式化 |

---

### 📚 学习辅助 (7 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [塑造 Agent 的灵魂](learning/soul-shaping-real.md) | 7 个真实 SOUL.md 文件 | 基于 OpenClaw 真实工作空间 |
| [有意思的 SOUL.md 收录](learning/interesting-soul-collection.md) | 5 个真实 SOUL.md | 产品经理、开发者、镜子、分析师、通用助理 |
| [创建每日自动写日记的 Agent](learning/mirror-agent-diary.md) | workspace-mirror | 真实运行的日记 Agent |
| [代码学习与理解](learning/code-learning.md) | OpenClaw read/exec | 内置工具 |
| [论文/文章摘要生成](learning/paper-summary.md) | summarize 技能 | URL、PDF、YouTube 总结 |
| [笔记整理与知识管理](learning/note-organize.md) | obsidian-cli 技能 | Obsidian 自动化 |
| [创建不同角色的 Agent](learning/create-agent-roles.md) | SOUL.md 塑造 | PM、开发者、日记等角色 |

---

## 目录结构

```
├── ai-capabilities/        # AI 能力案例
├── automation/            # 自动化案例
├── content-creation/       # 内容创作案例
│   ├── prompts/           # Prompt 模板
│   ├── templates/         # 输出模板
│   └── orchestrator/      # 总控编排
├── data-analysis/         # 数据分析案例
├── development/           # 开发辅助案例
├── learning/              # 学习辅助案例
├── personal-assistant/    # 个人助理案例
├── tools/                 # 工具集成案例
├── draft/                 # 草稿（待补充真实来源）
└── README.md
```

---

## 草稿目录

`draft/inspiration/` 存放了约 41 个**待补充真实来源**的案例草稿。

这些草稿目前缺少真实开源项目或技能文档引用，未来找到真实来源后会迁移到正式目录。

---

## 如何贡献

### 收录标准
1. 有真实来源（GitHub 项目 / OpenClaw 技能 / 可验证命令）
2. 可复现
3. 已脱敏（不含个人信息）

### 贡献方式
1. Fork 本仓库
2. 在对应目录添加案例文件
3. 在文件头部注明真实来源
4. 更新 README
5. 提交 PR

---

## 统计

- **真实案例**：63 个（不含模板文件）
- **草稿**：41 个
- **更新时间**：2026-03-25

---

## License

MIT
