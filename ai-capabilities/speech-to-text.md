# 语音转文字（本地运行）

## 干什么
使用 Whisper CLI 本地将音频转换为文字，无需 API Key，完全离线运行。

## 怎么干

### 1. 安装 Whisper

```bash
# macOS
brew install openai-whisper

# 验证安装
whisper --help
```

### 2. 基础转录

```bash
# 转录音频文件（默认 medium 模型）
whisper recording.mp3

# 指定输出格式
whisper meeting.m4a --output_format txt --output_dir ./transcripts

# 输出多种格式
whisper interview.mp3 --output_format all --output_dir ./output
```

### 3. 翻译模式

```bash
# 将非英语音频翻译成英语文字
whisper spanish_audio.mp3 --task translate --output_format srt
```

### 4. 模型选择

```bash
# 快速转录（小模型）
whisper audio.mp3 --model tiny

# 平衡速度和质量
whisper audio.mp3 --model base

# 高质量转录
whisper audio.mp3 --model medium

# 最高质量（需要更多内存）
whisper audio.mp3 --model large
```

### 5. 效果展示

**命令行输出：**
```
[00:00.000 --> 00:03.000] 大家好，今天我们来讨论项目进度。
[00:03.000 --> 00:06.500] 首先，上周我们完成了登录模块的开发。
[00:06.500 --> 00:10.200] 这周的重点是优化性能和修复 bug。
```

**输出文件：**
```
output/
├── audio.txt      # 纯文本
├── audio.srt      # 字幕文件
├── audio.vtt      # WebVTT 字幕
├── audio.json     # JSON 格式
└── audio.tsv      # 时间戳格式
```

## 模型对比

| 模型 | 参数量 | 英文速度 | 多语言 | 内存需求 |
|------|--------|----------|--------|----------|
| tiny | 39M | ~32x | ✅ | ~1GB |
| base | 74M | ~16x | ✅ | ~1GB |
| medium | 769M | ~6x | ✅ | ~5GB |
| large | 1550M | ~2x | ✅ | ~10GB |

## 常见问题

**Q: 模型下载到哪里？**
```
~/.cache/whisper/
```

**Q: 如何处理长音频？**
```bash
# 大模型会自动分段处理
whisper long_audio.mp3 --model medium
```

**Q: 如何提高中文识别准确率？**
```bash
# 使用 medium 或 large 模型
whisper chinese_audio.mp3 --model medium --language Chinese
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Whisper CLI | 本地语音识别 | `brew install openai-whisper` |
| 音频文件 | mp3/m4a/wav/flac 等 | 自行准备 |

**优势：完全本地运行，无需 API Key，无限次使用！**

## 来源

- 贡献者：Community
- 来源：openai-whisper 技能文档
- 日期：2024

## 相关资源

- [Whisper 官方介绍](https://openai.com/research/whisper)
- [GitHub 源码](https://github.com/openai/whisper)
