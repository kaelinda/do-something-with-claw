# 语音合成

## 干什么
使用 OpenClaw 调用 TTS（Text-to-Speech）服务，将文本转换为自然流畅的语音。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的配置：OpenAI API Key 或其他 TTS 服务配置
- 内置工具：tts

### 2. 执行步骤

#### 方式一：对话中直接使用
```
用户：把这段话读出来：大家好，欢迎使用 OpenClaw！
OpenClaw：[生成语音并自动播放]
```

#### 方式二：通过工具调用
```javascript
// 使用内置 tts 工具
const audio = await tts({
  text: "大家好，欢迎使用 OpenClaw！",
  voice: "alloy",  // 可选：alloy, echo, fable, onyx, nova, shimmer
  speed: 1.0       // 语速：0.25 到 4.0
});
```

#### 方式三：批量文本转语音
```bash
# 准备文本文件
cat articles/*.txt | openclaw tts --output ./audio --voice nova
```

### 3. 效果展示

**输入：**
```markdown
# 欢迎词
欢迎使用 OpenClaw 智能助手！我可以帮助你完成各种任务，
包括文档处理、代码开发、数据分析等。
```

**输出：**
- 生成 MP3 格式音频文件
- 支持多种语音风格
- 可调节语速

## 可用语音选项

| 语音名称 | 特点 | 适用场景 |
|----------|------|----------|
| alloy | 中性、平衡 | 通用场景 |
| echo | 男性、温暖 | 叙述、播客 |
| fable | 英式口音 | 故事、有声书 |
| onyx | 深沉男性 | 新闻、正式场合 |
| nova | 女性、活力 | 教学、引导 |
| shimmer | 女性、柔和 | 助手、友好对话 |

## 高级用法

### 1. 多角色对话生成
```javascript
// 为不同角色分配不同语音
const dialogue = [
  { speaker: "A", text: "你好，今天天气不错。", voice: "onyx" },
  { speaker: "B", text: "是啊，适合出去走走。", voice: "nova" }
];

for (const line of dialogue) {
  await tts({ text: line.text, voice: line.voice });
}
```

### 2. SSML 标记支持
```xml
<!-- 使用 SSML 控制语音细节 -->
<speak>
  欢迎使用 <emphasis level="strong">OpenClaw</emphasis>！
  <break time="500ms"/>
  我是你的智能助手。
</speak>
```

### 3. 长文本处理
```javascript
// 自动分割长文本
const longText = "...很长的文本...";
const chunks = splitText(longText, 4000); // OpenAI TTS 限制 4096 字符

for (const chunk of chunks) {
  const audio = await tts({ text: chunk });
  // 合并音频文件
}
```

### 4. 与其他功能结合
```
用户：把这篇飞书文档的内容读出来
OpenClaw：[读取文档内容] → [生成语音] → [播放]
```

## 使用场景

| 场景 | 描述 |
|------|------|
| 文章朗读 | 将博客、新闻转为音频 |
| 有声书制作 | 批量生成有声读物 |
| 视频配音 | 为视频生成旁白 |
| 无障碍访问 | 为视障用户提供语音支持 |
| 语言学习 | 发音示范 |
| 提醒播报 | 重要消息语音提醒 |

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| OpenAI API Key | 用于调用 TTS API | https://platform.openai.com |
| 音频播放器 | 播放生成的音频 | 系统自带 |

## 成本说明

| 模型 | 价格 |
|------|------|
| tts-1 | $0.015 / 1K 字符 |
| tts-1-hd | $0.030 / 1K 字符 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [OpenAI TTS API 文档](https://platform.openai.com/docs/api-reference/audio)
- [语音样本试听](https://platform.openai.com/docs/guides/text-to-speech/voice-options)
- [TTS 最佳实践](https://platform.openai.com/docs/guides/text-to-speech)
