# 视频处理

## 干什么
使用 OpenClaw 处理视频文件，包括提取帧、剪辑片段、生成预览图等操作。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的依赖：ffmpeg
- 可选技能：video-frames

### 2. 执行步骤

#### 方式一：提取视频帧
```
用户：从这个视频中提取关键帧
OpenClaw：正在分析视频并提取关键帧...
[生成帧图像序列]
```

#### 方式二：使用 video-frames 技能
```bash
# 安装技能
openclaw skill install video-frames

# 提取视频帧
openclaw video-frames extract \
  --input video.mp4 \
  --output ./frames \
  --interval 1s  # 每秒提取一帧

# 提取关键帧
openclaw video-frames keyframes \
  --input video.mp4 \
  --output ./keyframes
```

#### 方式三：剪辑视频片段
```bash
# 使用 ffmpeg 剪辑
openclaw exec ffmpeg -i input.mp4 -ss 00:01:00 -to 00:02:00 -c copy output.mp4
```

### 3. 效果展示

**提取帧示例：**
```
输入：demo.mp4（10分钟视频，1080p）
输出：
- frames/frame_0001.jpg
- frames/frame_0002.jpg
- ...
- frames/frame_0600.jpg（按每秒1帧，共600帧）
```

**剪辑片段示例：**
```
输入：原始视频 30 分钟
输出：1-2 分钟片段，保持原始质量
```

## 常用操作

### 1. 提取关键帧
```bash
# 使用场景变化检测提取关键帧
ffmpeg -i video.mp4 -vf "select='eq(pict_type,I)'" -vsync vfr keyframes_%03d.jpg
```

### 2. 生成视频预览 GIF
```bash
# 生成预览动图
ffmpeg -i video.mp4 -vf "fps=10,scale=320:-1" -t 5 preview.gif
```

### 3. 提取音频
```bash
# 从视频中提取音轨
ffmpeg -i video.mp4 -vn -acodec mp3 audio.mp3
```

### 4. 视频转码
```bash
# 转换格式
ffmpeg -i input.avi -c:v libx264 -c:a aac output.mp4
```

### 5. 添加水印
```bash
# 右下角添加 logo
ffmpeg -i video.mp4 -i logo.png \
  -filter_complex "overlay=W-w-10:H-h-10" \
  output.mp4
```

## 高级用法

### 1. 智能场景分割
```javascript
// 使用 OpenClaw 分析视频内容
const scenes = await analyzeVideoScenes("video.mp4");

// 根据场景变化提取片段
for (const scene of scenes) {
  await extractClip({
    input: "video.mp4",
    start: scene.start,
    end: scene.end,
    output: `scene_${scene.id}.mp4`
  });
}
```

### 2. 批量处理
```bash
# 批量提取所有视频的缩略图
for video in *.mp4; do
  ffmpeg -i "$video" -ss 00:00:01 -vframes 1 "${video%.mp4}_thumb.jpg"
done
```

### 3. 生成视频时间线
```javascript
// 生成视频预览时间线
await generateTimeline({
  input: "video.mp4",
  interval: 10,  // 每10秒一个缩略图
  output: "timeline.jpg",
  columns: 5
});
```

### 4. 与 AI 结合
```
用户：分析这个视频，找出所有出现人脸的片段
OpenClaw：[提取帧] → [人脸检测] → [标记时间点]
输出：
- 00:01:23 - 00:01:45：检测到人脸
- 00:03:12 - 00:03:30：检测到人脸
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| ffmpeg | 视频处理工具 | `brew install ffmpeg` |
| video-frames 技能 | 可选 | ClawHub 安装 |

## 性能优化

### 硬件加速
```bash
# 使用 GPU 加速（NVIDIA）
ffmpeg -hwaccel cuda -i input.mp4 output.mp4

# 使用 VideoToolbox（macOS）
ffmpeg -hwaccel videotoolbox -i input.mp4 output.mp4
```

### 内存优化
```bash
# 限制线程数，降低内存占用
ffmpeg -threads 4 -i large_video.mp4 output.mp4
```

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区，video-frames 技能文档
- 日期：2024

## 相关资源

- [FFmpeg 官方文档](https://ffmpeg.org/documentation.html)
- [FFmpeg 命令速查](https://cheatsheetdocs.com/ffmpeg)
- [video-frames 技能](https://clawhub.com/skills/video-frames)
