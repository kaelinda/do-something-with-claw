# Agent Teams 自动写小说（真实开源案例）

## 真实来源

- 项目：ThomasHoussin/Claude-Book
- GitHub：<https://github.com/ThomasHoussin/Claude-Book>
- 类型：Multi-Agent 小说写作框架
- 核心特征：章节规划、正文写作、风格校验、人物一致性审查、连续性审查、状态更新、电子书导出

## 为什么这个案例值得收录

这不是“我脑补出来的小说工作流”，而是一个已经公开的 **multi-agent novel writing framework**。

它把“自动写小说”拆成了一组明确分工的 Agent：

| Agent | 作用 |
|------|------|
| chapter-planner | 先规划本章 beats / 节奏 |
| chapter-writer | 按风格与设定写正文 |
| style-linter | 检查是否符合写作风格规则 |
| character-reviewer | 检查人物行为、语气是否一致 |
| continuity-reviewer | 检查时间线、空间逻辑、前后呼应 |
| state-updater | 抽取本章产生的状态变化，写回系统 |

这正是你说的 **Agent teams 自动写小说**。

## 仓库结构（来自开源 README）

```text
├── CLAUDE.md                 # 总控/编排说明
├── .claude/agents/           # 各类 agent 定义
├── .claude/skills/           # 可复用技能
├── bible/                    # 永久设定：风格、人物、世界观
├── state/                    # 每章状态（版本化）
├── story/                    # synopsis、plan、chapters
├── timeline/                 # 历史事件与当前章节事件
├── ebook/                    # 导出 EPUB/MOBI/AZW3
└── .work/                    # 中间产物
```

## 核心工作流

### 1. 建立小说圣经（Bible）
先准备不会轻易变动的长期设定：
- `bible/style.md`：文风规则
- `bible/structure.md`：结构规则
- `bible/characters/*.md`：人物卡
- `bible/universe/*.md`：地点、世界观、设定

### 2. 建立故事规划
- `story/synopsis.md`：故事简介
- `story/plan.md`：章节大纲

### 3. 初始化状态
- 在 `state/template/` 里准备初始状态
- 用 `state/current/` 指向当前状态

### 4. 启动多 Agent 写作
编排器会按顺序做这些事：
1. planner 规划章节节拍
2. writer 写章节初稿
3. perplexity-improver 降低套话和 AI 痕迹
4. style-linter 检查文风
5. character-reviewer 检查人物一致性
6. continuity-reviewer 检查时间线和逻辑
7. 如有问题，最多循环修订 3 次
8. state-updater 写回状态变化
9. timeline/history.md 追加历史事件
10. 保存最终章节

### 5. 导出电子书
用 `ebook/build-ebook.ps1` 导出 EPUB/MOBI/AZW3。

## 拿来就能用的最佳实践（脱敏版）

下面不是原仓库逐字复制，而是基于其真实结构整理出的 **最小可复用实践**。

### Step 1：建立目录

```text
my-novel/
├── bible/
│   ├── style.md
│   ├── characters/
│   │   ├── protagonist.md
│   │   └── mentor.md
│   └── universe/
│       └── city.md
├── story/
│   ├── synopsis.md
│   ├── plan.md
│   └── chapters/
├── state/
│   ├── template/
│   └── current/
└── timeline/
    ├── history.md
    └── current-chapter.md
```

### Step 2：先写 3 份关键输入

#### `bible/style.md`
```md
- 目标读者：喜欢悬疑与都市奇幻的年轻读者
- 文风：克制、冷静、少说教
- 节奏：每章必须有一个推进点和一个悬念点
- 禁止：空泛抒情、重复解释、总结式段落
```

#### `story/synopsis.md`
```md
在近未来上海，一位能够读取“城市残留记忆”的档案修复师，卷入一场跨越二十年的旧案。
```

#### `story/plan.md`
```md
# 第一卷
1. 主角接到异常档案
2. 第一次读取记忆失败
3. 发现失踪案线索
4. 遇到关键配角
5. 真相出现第一次反转
```

### Step 3：Agent Team 分工建议

这是我基于该开源仓库提炼出的 **推荐分工**：

| 角色 | 输入 | 输出 |
|------|------|------|
| 世界观策划 Agent | synopsis + universe | 世界规则补全 |
| 章节规划 Agent | synopsis + plan + current state | 本章 beats |
| 正文写作 Agent | beats + style + characters | 章节草稿 |
| 人物审查 Agent | draft + character cards | 人设一致性报告 |
| 连续性审查 Agent | draft + timeline/history | 时间线/逻辑报告 |
| 状态更新 Agent | final chapter | 状态变化、关系变化、事件回写 |

### Step 4：每章运行顺序

```text
章节规划 → 正文写作 → 人设检查 → 连续性检查 → 修订 → 写回状态
```

### Step 5：避免写崩的 5 条规则

1. **Bible 只读**：写作时不要随便改世界观主设定
2. **State 每章归档**：每章结束都保存一次状态快照
3. **Timeline 追加不覆盖**：历史事件只追加，方便追溯
4. **先规划再写**：不要直接从 synopsis 一步生成 3000 字正文
5. **审查 Agent 独立**：不要让 writer 自己评自己

## 为什么我推荐这个方案

### 推荐理由
- **真 Multi-Agent**：不是“一个 prompt 假装多个角色”
- **长篇友好**：把状态、时间线、人物设定拆开维护
- **可扩展**：你可以替换 writer、reviewer、导出器
- **有工程化思维**：章节状态、历史追踪、电子书导出都考虑到了

### 不推荐直接照搬的地方
- 原项目偏 **Claude Code 工作流**，如果你要落到 OpenClaw，需要重写成 OpenClaw 的 agent / sessions / memory 工作流
- 原项目默认输出语言是法语，落地时要改成中文或你的目标语言
- 有些增强步骤（如 perplexity-improver）依赖本地模型/GPU，门槛较高

## 对 OpenClaw 的落地改造建议

我已经另外补了一篇可直接执行的 OpenClaw 落地方案：

- [OpenClaw 版 Agent Teams 自动写小说（可执行方案）](openclaw-agent-teams-novel-workflow.md)

核心做法：
- 主 Agent：总控章节流程
- 子 Agent 1：章节规划
- 子 Agent 2：正文写作
- 子 Agent 3：人物一致性检查
- 子 Agent 4：连续性检查
- 主 Agent：汇总意见并出终稿

我的建议仍然是：
**先做轻量编排版，再决定是否演进成更复杂的平台。**

## 可复用提示词骨架（脱敏版）

### 章节规划 Agent
```text
你是章节规划 Agent。
输入：故事简介、章节大纲、当前状态、人物卡、时间线。
输出：本章目标、冲突、转折、结尾悬念、3-7 个 beats。
要求：不能引入违背 bible 的新设定。
```

### 正文写作 Agent
```text
你是正文写作 Agent。
根据章节 beats、文风规则、人物卡写出本章草稿。
要求：
1. 人物语气稳定
2. 每章必须推进剧情
3. 不重复解释读者已经知道的信息
```

### 连续性审查 Agent
```text
你是连续性审查 Agent。
检查本章与历史章节是否冲突：
- 时间线
- 地点切换
- 人物已知信息
- 道具/设定是否前后矛盾
输出问题列表，按严重程度排序。
```

## 相关开源备选

### 1. CoLong-Idea-Studio
- GitHub：<https://github.com/HITSZ-DS/CoLong-Idea-Studio>
- 特点：动态记忆优先、章节规划、写回 memory、可观测运行产物
- 更适合：长篇、连载、世界观复杂的故事生产线

### 2. novel-multi-agents
- GitHub：<https://github.com/QSPBU-LONG/novel-multi-agents>
- 公开信息较少，目前更适合作为补充参考，不适合作为首推样板

## 来源

- 贡献者：Community
- 来源：GitHub 开源仓库（Claude-Book / CoLong-Idea-Studio）
- 日期：2024

## 备注

本案例基于真实开源仓库整理，并做了脱敏与最佳实践改写。
不包含任何个人路径、私人项目名或敏感配置。
