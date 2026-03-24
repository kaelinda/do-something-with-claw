# 播客脚本生成

## 干什么
使用 OpenClaw 自动生成播客脚本，包括单口播客、访谈播客、专题播客等多种形式。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 可选：飞书文档、Obsidian

### 2. 执行步骤

#### 方式一：对话式生成
```
用户：帮我写一期关于「AI 如何改变工作方式」的播客脚本
OpenClaw：已生成播客脚本：

# AI 如何改变工作方式

## 开场白（1分钟）
大家好，欢迎来到今天的节目。
今天我们要聊一个热门话题：
人工智能正在如何改变我们的工作方式...

## 话题引入（2分钟）
最近，ChatGPT 的出现让所有人都在讨论 AI...
（话题背景、热点事件）

## 核心讨论（15分钟）
### 1. AI 已经在改变哪些工作？
- 写作和内容创作
- 编程和开发
- 数据分析...

### 2. 哪些工作会被取代？
...

### 3. 我们该如何应对？
...

## 总结收尾（2分钟）
总结一下今天的观点...
下期节目我们将聊...

感谢收听，我们下期再见！
```

#### 方式二：访谈脚本生成
```
用户：生成一期的访谈播客脚本，嘉宾是技术专家
OpenClaw：[生成包含嘉宾问答的访谈脚本]
```

### 3. 效果展示

**播客脚本结构：**
```
🎙️ 播客脚本：技术人的职业发展

时长：约 30 分钟
形式：单口 + 嘉宾访谈
风格：轻松对话

┌─────────────────────────────────────┐
│ 🎵 片头音乐（15秒）                 │
├─────────────────────────────────────┤
│ 📖 开场白（1分钟）                  │
│    - 自我介绍                       │
│    - 本期主题                       │
│    - 收听指南                       │
├─────────────────────────────────────┤
│ 💬 话题展开（25分钟）               │
│    - 第一个观点（8分钟）            │
│    - 第二个观点（8分钟）            │
│    - 第三方观点（9分钟）            │
├─────────────────────────────────────┤
│ 🎤 嘉宾访谈（15分钟）               │
│    - 嘉宾介绍                       │
│    - 问答环节                       │
│    - 嘉宾建议                       │
├─────────────────────────────────────┤
│ 📝 总结收尾（2分钟）                │
│    - 观点回顾                       │
│    - 下期预告                       │
│    - 订阅引导                       │
└─────────────────────────────────────┘
```

## 常用场景

### 1. 单口播客
```javascript
// 生成单口播客脚本
async function generateSoloPodcast(topic) {
  return {
    title: '播客标题',
    duration: '20-30分钟',
    structure: {
      intro: '开场引入（2分钟）',
      mainContent: [
        { point: '观点1', duration: '5分钟', examples: [] },
        { point: '观点2', duration: '5分钟', examples: [] },
        { point: '观点3', duration: '5分钟', examples: [] }
      ],
      conclusion: '总结收尾（3分钟）'
    },
    notes: '讲述要点、转场提示、语气建议'
  };
}
```

### 2. 访谈播客
```javascript
// 生成访谈播客脚本
async function generateInterviewPodcast(guest, topic) {
  return {
    preInterview: {
      backgroundResearch: '嘉宾背景调研',
      questionPrep: '预设问题列表'
    },
    script: {
      intro: '主持人介绍 + 嘉宾介绍（3分钟）',
      warmUp: '轻松开场问题（2分钟）',
      mainQA: [
        { question: '核心问题1', followUp: '追问方向' },
        { question: '核心问题2', followUp: '追问方向' }
      ],
      rapidFire: '快问快答环节（可选）',
      closing: '嘉宾建议 + 结束语（3分钟）'
    }
  };
}
```

### 3. 专题播客
```javascript
// 生成专题系列播客
async function generateSeriesPodcast(theme, episodeCount) {
  return {
    seriesTitle: '系列主题',
    episodes: [
      { ep: 1, title: '第1集标题', focus: '聚焦点' },
      { ep: 2, title: '第2集标题', focus: '聚焦点' },
      // ...
    ],
    continuity: '系列连贯性设计',
    crossReference: '集数之间的关联'
  };
}
```

### 4. 故事型播客
```javascript
// 生成叙事型播客
async function generateNarrativePodcast(story) {
  return {
    act: {
      setup: '故事背景设定',
      conflict: '冲突和挑战',
      resolution: '解决和反思'
    },
    pacing: '节奏控制',
    cliffhangers: '悬念设计',
    soundDesign: '音效建议'
  };
}
```

## 高级用法

### 1. 脚本模板库
```markdown
# 开场白模板

模板A（轻松风格）：
"嘿大家好，欢迎来到[播客名称]，我是[名字]。
今天我们要聊一个很有意思的话题...
准备好了吗？让我们开始吧！"

模板B（正式风格）：
"各位听众朋友大家好，欢迎收听本期节目。
在开始之前，我想先问大家一个问题..."
```

### 2. 转场设计
```javascript
// 转场语句生成
const transitions = {
  toNextPoint: [
    '说到这个，我想到了另一个相关的话题...',
    '这让我想起了...',
    '除了这些，还有一点很重要...'
  ],
  toGuest: [
    '说到这里，我想请今天的嘉宾分享一下他的看法...',
    '在这个问题上，[嘉宾名]有独特的见解...'
  ],
  toConclusion: [
    '好了，我们来总结一下今天的内容...',
    '时间差不多了，最后我想说...'
  ]
};
```

### 3. 时长控制
```javascript
// 根据目标时长调整内容
function adjustDuration(script, targetMinutes) {
  const wordsPerMinute = 150; // 中文语速
  
  script.sections.forEach(section => {
    const targetWords = section.minutes * wordsPerMinute;
    section.content = adjustContent(section.content, targetWords);
  });
}
```

### 4. 脚本标注
```markdown
# 标注格式

[语气：轻松] 大家好...
[语速：放慢] 这是一个很重要的观点...
[停顿：2秒] ...
[音效：叮] 
[BGM：淡入]
[BGM：切换为轻快]
```

### 5. 与 TTS 集成
```javascript
// 生成音频预览
async function previewPodcast(script) {
  const audioSegments = [];
  
  for (const section of script.sections) {
    const audio = await tts({
      text: section.content,
      voice: section.speaker === 'host' ? 'onyx' : 'echo',
      speed: section.pace || 1.0
    });
    audioSegments.push(audio);
  }
  
  return mergeAudio(audioSegments);
}
```

## 脚本模板

### 访谈脚本
```markdown
# 访谈播客脚本

## 准备阶段
- 嘉宾背景调研
- 核心问题列表（10-15个）
- 备选话题

## 开场（3分钟）
1. 播客介绍
2. 本期主题引入
3. 嘉宾介绍

## 正式访谈（20-25分钟）
### 第一部分：背景了解
Q1: 请简单介绍一下自己...
Q2: 您是如何进入这个领域的...

### 第二部分：核心话题
Q3: 关于[主题]，您的看法是...
Q4: 能分享一个具体的案例吗...
Q5: 在这个过程中遇到的最大挑战是...

### 第三部分：深入探讨
Q6: 您认为未来的趋势会是...
Q7: 对于新人有什么建议...

## 快问快答（3分钟）
- 最近在读什么书？
- 最推荐的一个工具？
- 一句话建议...

## 结尾（2分钟）
1. 嘉宾总结发言
2. 嘉宾联系方式
3. 下期预告
4. 订阅引导
```

### 故事播客脚本
```markdown
# 故事播客脚本

## 开场
- 引入故事背景
- 设定悬念

## 第一幕：设定
- 人物介绍
- 场景描述
- 初始状态

## 第二幕：冲突
- 事件发生
- 矛盾展开
- 转折点

## 第三幕：高潮
- 关键时刻
- 决策和行动

## 第四幕：结局
- 结果呈现
- 反思和启示

## 结尾
- 故事寓意
- 引发思考
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 飞书文档 | 可选，协作编辑 | https://feishu.cn |
| Obsidian | 可选，脚本管理 | https://obsidian.md |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [播客制作指南](https://www.buzzsprout.com/blog)
- [访谈技巧](https://www.npr.org/)
- [播客脚本写作](https://podcasts.apple.com/resources)
