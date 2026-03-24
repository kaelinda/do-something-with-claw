# 视频脚本生成

## 干什么
使用 OpenClaw 自动生成视频脚本，包括短视频、长视频、教程、解说等多种类型。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 可选：相关技能或配置

### 2. 执行步骤

#### 方式一：对话式生成
```
用户：帮我写一个 3 分钟的产品介绍视频脚本
OpenClaw：已生成视频脚本：

# 产品介绍视频脚本

## 开场（0:00-0:15）
[画面：产品Logo动画]
旁白：在信息爆炸的时代，如何高效管理你的时间？

## 问题引入（0:15-0:45）
[画面：繁忙的办公场景]
旁白：每天面对无数消息、会议、任务...
你是否也感到力不从心？

## 产品展示（0:45-2:00）
[画面：产品界面演示]
旁白：智能助手，让一切变得简单...
（展示核心功能）

## 结尾（2:00-3:00）
[画面：用户满意的笑容]
旁白：开启你的高效之旅，从现在开始。
```

#### 方式二：主题式生成
```
用户：写一个「如何学习编程」的教学视频脚本
OpenClaw：[生成教学视频脚本]
```

### 3. 效果展示

**生成的脚本结构：**
```
📄 视频脚本：如何学习编程

时长：约 8 分钟
风格：教学类
目标观众：编程初学者

┌─────────────────────────────────────┐
│ 场景 1：开场引入（0:00-0:30）       │
├─────────────────────────────────────┤
│ 画面：代码编辑器动画                │
│ 配音：欢迎来到编程的世界...         │
│ 字幕：中英双语                      │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│ 场景 2：为什么要学编程（0:30-1:30） │
├─────────────────────────────────────┤
│ 画面：应用场景蒙太奇                │
│ 配音：编程可以改变世界...           │
│ 要点：1.职业机会 2.思维提升 3.创造  │
└─────────────────────────────────────┘

...（共 8 个场景）
```

## 常用场景

### 1. 短视频脚本
```javascript
// 生成抖音/快手风格短视频脚本
async function generateShortVideoScript(topic) {
  return {
    duration: '60秒',
    hook: '开场 3 秒抓住眼球',
    body: '核心内容 40 秒',
    cta: '引导互动 17 秒',
    music: '推荐配乐风格',
    effects: '推荐特效'
  };
}
```

### 2. 教学视频脚本
```javascript
// 生成教学视频脚本
async function generateTutorialScript(topic) {
  return {
    intro: '课程介绍和学习目标',
    prerequisites: '前置知识说明',
    sections: [
      { title: '概念讲解', duration: '5分钟' },
      { title: '实操演示', duration: '10分钟' },
      { title: '练习任务', duration: '3分钟' }
    ],
    summary: '知识点回顾',
    resources: '扩展学习资源'
  };
}
```

### 3. 产品解说脚本
```javascript
// 生成产品解说脚本
async function generateProductScript(product) {
  return {
    hook: '痛点问题引入',
    solution: '产品解决方案',
    features: '核心功能展示',
    benefits: '用户价值说明',
    demo: '使用场景演示',
    cta: '行动号召'
  };
}
```

### 4. Vlog 脚本
```javascript
// 生成 Vlog 脚本
async function generateVlogScript(theme) {
  return {
    opening: '开场白',
    segments: [
      { scene: '场景描述', talking: '对白', broll: '空镜建议' }
    ],
    closing: '结尾感悟',
    music: '背景音乐建议'
  };
}
```

## 高级用法

### 1. 分镜脚本生成
```markdown
# 分镜脚本

| 镜号 | 景别 | 画面内容 | 旁白 | 时长 | 备注 |
|------|------|----------|------|------|------|
| 1 | 全景 | 城市天际线 | 开场白 | 3s | 日出镜头 |
| 2 | 中景 | 主角走入 | 自我介绍 | 5s | 跟拍 |
| 3 | 特写 | 产品界面 | 功能讲解 | 10s | 录屏 |
| 4 | 近景 | 用户反馈 | 评价展示 | 5s | 采访 |
```

### 2. 多风格适配
```javascript
// 根据平台调整风格
const styles = {
  'douyin': {
    duration: '15-60秒',
    pace: '快节奏',
    hook: '3秒黄金开场',
    ending: '悬念/互动'
  },
  'bilibili': {
    duration: '5-20分钟',
    pace: '适中',
    structure: '完整叙事',
    ending: '干货总结'
  },
  'youtube': {
    duration: '10-30分钟',
    pace: '适中偏快',
    structure: '故事化',
    ending: '订阅引导'
  }
};
```

### 3. 脚本优化
```javascript
// 根据时长优化脚本
function optimizeScript(script, targetDuration) {
  const currentDuration = script.totalDuration;
  
  if (currentDuration > targetDuration) {
    // 精简内容
    return compressScript(script);
  } else if (currentDuration < targetDuration) {
    // 扩展内容
    return expandScript(script);
  }
  
  return script;
}
```

### 4. 协作编辑
```javascript
// 多人协作脚本
async function collaborativeScript(scriptId) {
  // 同步到飞书文档
  await feishuDoc.write({
    doc_token: scriptId,
    content: scriptContent
  });
  
  // 多人实时编辑
  // 评论和修改建议
}
```

### 5. AI 配音集成
```javascript
// 生成配音
async function generateNarration(script) {
  for (const scene of script.scenes) {
    const audio = await tts({
      text: scene.narration,
      voice: 'onyx',  // 专业男声
      speed: 1.0
    });
    scene.audioUrl = audio.url;
  }
}
```

## 脚本模板

### 产品发布脚本
```markdown
# [产品名称] 发布视频脚本

## 开场（15秒）
- 画面：Logo 动画
- 旁白：[一句话价值主张]

## 痛点（30秒）
- 画面：问题场景
- 旁白：描述用户痛点

## 方案（60秒）
- 画面：产品展示
- 旁白：如何解决痛点

## 证明（30秒）
- 画面：用户反馈/数据
- 旁白：效果证明

## 结尾（15秒）
- 画面：CTA
- 旁白：行动号召
```

### 教程视频脚本
```markdown
# [主题] 教程视频脚本

## 开场
- 本期学习目标
- 预计时长

## 准备工作
- 需要的工具/材料
- 前置知识

## 步骤分解
1. 步骤一
   - 操作演示
   - 注意事项
2. 步骤二
   ...

## 常见问题
- Q1: ...
- Q2: ...

## 总结
- 知识点回顾
- 下期预告
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 飞书文档 | 可选，协作编辑 | https://feishu.cn |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [短视频脚本技巧](https://www.youtube.com/creatoracademy)
- [视频叙事结构](https://www.storyblocks.com/blog)
