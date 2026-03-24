# OpenClaw 版 Agent Teams 自动写小说（可执行方案）

## 适用场景

当你想用 OpenClaw 搭一个 **多 Agent 协作写长篇小说** 的工作流时，这个方案可以直接照着跑。

目标不是“一次性生成整本书”，而是把小说生产拆成稳定的流水线：

```text
设定准备 → 章节规划 → 正文写作 → 人设检查 → 连续性检查 → 定稿归档
```

这个方案参考了真实开源项目：
- `ThomasHoussin/Claude-Book`
- `HITSZ-DS/CoLong-Idea-Studio`

但这里给你的，是 **OpenClaw 版可执行落地方案**。

---

## 一、推荐架构

### 主 Agent：小说总控 PM
职责：
- 读取设定与当前状态
- 派发本章任务给子 Agent
- 汇总审查意见
- 触发修订
- 归档最终章节与状态

### 子 Agent 1：章节规划 Agent
职责：
- 根据总纲和当前状态，产出本章 beats
- 明确本章目标、冲突、转折、悬念

### 子 Agent 2：正文写作 Agent
职责：
- 根据 beats + 风格规则 + 人物卡写出章节草稿

### 子 Agent 3：人物一致性审查 Agent
职责：
- 检查人设、语气、动机是否跑偏

### 子 Agent 4：连续性审查 Agent
职责：
- 检查时间线、地点、前情、道具、已知信息是否冲突

> 第一版我**不建议**继续拆更多 agent。
> 4 个子 Agent 已经够用，复杂度和收益比较平衡。

---

## 二、目录结构（最小可用）

```text
novel-project/
├── bible/
│   ├── style.md
│   ├── structure.md
│   ├── characters/
│   │   ├── protagonist.md
│   │   └── supporting-cast.md
│   └── universe/
│       └── world.md
├── story/
│   ├── synopsis.md
│   ├── plan.md
│   └── chapters/
│       ├── chapter-01.md
│       └── chapter-02.md
├── state/
│   ├── current.md
│   └── archive/
├── timeline/
│   ├── history.md
│   └── current-chapter.md
└── reviews/
    ├── character/
    └── continuity/
```

---

## 三、先准备 5 个基础文件

### 1. `bible/style.md`
```md
# 文风规则
- 类型：都市悬疑 + 奇幻
- 叙述：第三人称近距离视角
- 语言：克制、具体、少空话
- 节奏：每章必须有推进点与悬念点
- 禁止：总结式结尾、重复解释、说教
```

### 2. `bible/characters/protagonist.md`
```md
# 主角卡
- 姓名：沈砚
- 职业：档案修复师
- 核心能力：能读取物品残留记忆
- 性格：冷静、克制、多疑
- 弱点：不信任他人，容易独自承担
- 禁忌：不会轻易暴露能力
```

### 3. `bible/universe/world.md`
```md
# 世界观
- 时间：近未来都市
- 特殊设定：部分旧物会残留高强度记忆片段
- 社会认知：大多数人不相信超常现象
- 风险：读取过强记忆可能导致短暂意识混乱
```

### 4. `story/synopsis.md`
```md
在近未来城市，一名能读取旧物残留记忆的档案修复师，因一份异常档案卷入一场二十年前的失踪案。
```

### 5. `story/plan.md`
```md
# 第一卷计划
1. 主角接触异常档案
2. 第一次读取失败
3. 发现失踪案线索
4. 遇到关键证人
5. 第一卷反转：失踪者可能仍然活着
```

---

## 四、每章执行流程

## Step 1：章节规划
让主 Agent 给“章节规划 Agent”派任务。

### 输入
- `story/synopsis.md`
- `story/plan.md`
- `state/current.md`
- `timeline/history.md`
- `bible/style.md`
- 人物卡 / 世界观

### 输出
写入：`story/chapter-XX-outline.md`

### 输出格式建议
```md
# Chapter 03 Outline

## 本章目标
主角确认异常档案与旧案之间存在直接关联。

## 冲突
主角必须在继续追查与隐藏能力之间做选择。

## 转折
关键证据显示旧案中的失踪者并非单纯受害者。

## 悬念
主角在结尾听到了一个本不该出现的声音。

## Beats
1. 主角在修复室复查档案
2. 读取记忆出现异常
3. 联系旧案相关人失败
4. 从影像残片中看见关键符号
5. 结尾留下新的疑点
```

---

## Step 2：正文写作
把 outline 交给“正文写作 Agent”。

### 输入
- `story/chapter-XX-outline.md`
- `bible/style.md`
- `bible/characters/*.md`
- `bible/universe/*.md`
- `timeline/history.md`

### 输出
写入：`story/chapters/chapter-XX-draft.md`

### 要求
- 先出草稿，不要求一次完美
- 不新增违反 bible 的核心设定
- 每章必须有推进

---

## Step 3：人物一致性审查
把草稿交给“人物审查 Agent”。

### 输出
写入：`reviews/character/chapter-XX.md`

### 审查模板
```md
# Character Review - Chapter 03

## 结论
- 是否通过：否

## 问题
1. 主角在第 4 段过度坦白，不符合“不会轻易暴露能力”的设定
2. 配角林初的语气突然变得过于轻佻，与前文不一致

## 建议修改
- 删除主角直接解释能力的对白
- 将林初的表达改回克制、试探型语气
```

---

## Step 4：连续性审查
把草稿交给“连续性审查 Agent”。

### 输出
写入：`reviews/continuity/chapter-XX.md`

### 审查模板
```md
# Continuity Review - Chapter 03

## 结论
- 是否通过：否

## 问题
1. 第二章结尾主角已离开档案馆，本章开头却仍在原地，缺少过渡
2. 第三段提到的录音笔在前文尚未出现
3. 时间从傍晚直接跳到凌晨，没有交代

## 建议修改
- 补一段回到修复室的过渡
- 给录音笔补首次出现节点
- 明确夜间调查的时间推进
```

---

## Step 5：主 Agent 汇总并修订
主 Agent 读取两个 review：
- `reviews/character/chapter-XX.md`
- `reviews/continuity/chapter-XX.md`

然后决定：
- 如果问题少：直接小修
- 如果问题多：再派回“正文写作 Agent”修订一轮

### 修订原则
- 最多 2~3 轮
- 只修关键问题，不做无限润色
- 防止陷入“永远改不完”

---

## Step 6：定稿与状态回写
当章节通过后：

### 最终产物
- `story/chapters/chapter-XX.md` 最终稿
- `state/current.md` 更新当前人物关系、已知线索、道具状态
- `state/archive/chapter-XX-state.md` 归档快照
- `timeline/history.md` 追加本章事件摘要

### `state/current.md` 示例
```md
# 当前状态
- 主角已确认异常档案与旧案有关
- 新线索：档案中的符号与旧城区地铁站有关
- 林初开始怀疑主角隐瞒了关键信息
- 道具状态：录音笔已损坏，无法再次回放
```

### `timeline/history.md` 示例
```md
# 历史事件

## Chapter 03
- 主角再次读取异常档案
- 发现旧案新线索
- 与林初关系出现裂痕
- 档案中出现神秘声音
```

---

## 五、OpenClaw 里的执行方式

## 方案：主 Agent + 子 Agent 派发

你可以用 `sessions_spawn` 派发每个子任务。

### 1. 派发章节规划
```json
{
  "runtime": "subagent",
  "label": "novel-ch03-outline",
  "task": "你是章节规划 Agent。请根据 synopsis、plan、current state、timeline 和人物卡，生成 Chapter 03 outline，输出目标、冲突、转折、悬念、5个 beats。"
}
```

### 2. 派发正文写作
```json
{
  "runtime": "subagent",
  "label": "novel-ch03-draft",
  "task": "你是正文写作 Agent。根据 Chapter 03 outline、style.md、人物卡与世界观，写出 2500-4000 字章节草稿。"
}
```

### 3. 派发人物审查
```json
{
  "runtime": "subagent",
  "label": "novel-ch03-character-review",
  "task": "你是人物一致性审查 Agent。请检查这章是否有人设跑偏、语气失真、动机异常。输出问题清单与修改建议。"
}
```

### 4. 派发连续性审查
```json
{
  "runtime": "subagent",
  "label": "novel-ch03-continuity-review",
  "task": "你是连续性审查 Agent。请检查时间线、地点、设定、道具、已知信息是否冲突。输出问题清单与修改建议。"
}
```

---

## 六、我推荐的运行节奏

### 推荐
**一次只推进一章。**

理由：
- 长篇最怕前面改了，后面全崩
- 一章一归档，便于回滚
- 审查反馈容易闭环

### 不推荐
一次连续生成 10 章。

理由：
- 漂移会越来越严重
- 状态维护成本暴增
- 后面返工很重

---

## 七、最小 MVP

如果你今天就要开跑，我建议第一版只做这些：

- 1 个主 Agent
- 4 个子 Agent
- 只写 1 卷
- 每章 2500~4000 字
- 每章最多修 2 轮
- 不做电子书导出
- 不做花哨 UI

**先验证“写得稳不稳”，再考虑“做得炫不炫”。**

---

## 八、常见失败点

### 1. Writer 直接乱加设定
解决：
- bible 只读
- 审查 agent 独立

### 2. Review 太多，永远过不去
解决：
- 只拦截关键问题
- 限制修订轮数

### 3. 章节有文风，但没推进
解决：
- outline 必须先明确“本章目标”
- 每章至少一个推进点

### 4. 后面章节忘了前面内容
解决：
- `timeline/history.md` 必须持续追加
- `state/current.md` 必须每章更新

---

## 九、我的明确建议

### 推荐方案
先按这个 OpenClaw 版工作流落地。

### 推荐理由
- 比“一个大 prompt 写整本书”稳定得多
- 比完整复刻大型研究框架简单得多
- 足够接近真实生产流程
- 方便逐步加 Agent

### 不推荐方案
一上来就做成超复杂平台。

原因：
- 调试成本高
- 失败点太多
- 很容易还没写出第一章就先把系统做死

---

## 十、配套文件建议

我已经补了 4 个核心 prompt 模板，可直接复用：

- `content-creation/prompts/chapter-planner.md`
- `content-creation/prompts/chapter-writer.md`
- `content-creation/prompts/character-reviewer.md`
- `content-creation/prompts/continuity-reviewer.md`

下一步如果继续沉淀成完整仓库模板，建议再补：

- `templates/outline-template.md`
- `templates/character-review-template.md`
- `templates/continuity-review-template.md`
- `templates/state-template.md`

---

## 来源

- 贡献者：Community
- 来源：基于 GitHub 开源项目 Claude-Book / CoLong-Idea-Studio 的 OpenClaw 落地改写
- 日期：2024

## 备注

这是可执行工作流方案，不是空泛概念说明。
已做脱敏处理，可直接拿来作为 OpenClaw 多 Agent 小说项目的起点。
