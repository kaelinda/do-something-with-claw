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

### ✍️ 内容创作 (1 个完整工作流)

#### Agent Teams 自动写小说
基于 GitHub 开源项目整理的完整多 Agent 小说写作工作流：

| 文档 | 说明 |
|------|------|
| [真实开源案例](content-creation/agent-teams-novel-writing.md) | 基于 Claude-Book 和 CoLong-Idea-Studio |
| [OpenClaw 可执行方案](content-creation/openclaw-agent-teams-novel-workflow.md) | 主 Agent + 4 子 Agent 工作流 |
| [Prompt 模板](content-creation/prompts/chapter-planner.md) | 章节规划、正文写作、人物审查、连续性审查 |
| [输出模板](content-creation/templates/outline-template.md) | 大纲、审查、状态回写模板 |
| [总控编排](content-creation/orchestrator/novel-master-agent.md) | 主 Agent 调度流程 |

---

### 💻 开发辅助 (4 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [使用 Codex 自动编写代码](development/codex-coding.md) | Codex CLI | 真实命令行工具 |
| [使用 Claude Code 自动编写代码](development/claude-code-coding.md) | Claude Code CLI | 真实命令行工具 |
| [并行修复多个 GitHub Issues](development/parallel-issue-fix.md) | git worktree + Codex | 可验证的命令 |
| [并行审查多个 GitHub PR](development/parallel-pr-review.md) | Codex + gh CLI | 可验证的命令 |

---

### 🎨 AI 能力 (5 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [图像生成](ai-capabilities/image-generation.md) | openai-image-gen skill | OpenClaw 内置技能 |
| [语音合成](ai-capabilities/speech-synthesis.md) | 内置 tts 工具 | OpenClaw 内置工具 |
| [语音转文字](ai-capabilities/speech-to-text.md) | Whisper CLI | 本地运行，无需 API Key |
| [视频帧提取](ai-capabilities/video-frames.md) | video-frames skill | 真实脚本命令 |
| [视频处理](ai-capabilities/video-processing.md) | video-frames skill | 真实技能文档 |

---

### 🔧 工具集成 (1 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [飞书文档操作](tools/feishu-integration.md) | feishu 技能组 | 真实技能文档 |

---

## 目录结构

```
├── ai-capabilities/        # AI 能力案例
├── content-creation/       # 内容创作案例
│   ├── prompts/           # Prompt 模板
│   ├── templates/         # 输出模板
│   └── orchestrator/      # 总控编排
├── development/           # 开发辅助案例
├── tools/                 # 工具集成案例
├── draft/                 # 草稿（待补充真实来源）
└── README.md
```

---

### 📚 学习辅助 (2 个)

| 案例 | 来源 | 说明 |
|------|------|------|
| [塑造 Agent 的灵魂](learning/soul-shaping-real.md) | 7 个真实 SOUL.md 文件 | 基于 OpenClaw 真实工作空间 |
| [创建每日自动写日记的 Agent](learning/mirror-agent-diary.md) | workspace-mirror | 真实运行的日记 Agent |

---

## 草稿目录

`draft/inspiration/` 存放了约 44 个**待补充真实来源**的案例草稿。

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

- **真实案例**：11 个（不含模板文件）
- **草稿**：44 个
- **更新时间**：2026-03-25

---

## License

MIT
