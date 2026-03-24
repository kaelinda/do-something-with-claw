# 视频帧提取

## 干什么
从视频中提取特定帧或创建缩略图，用于预览、截图、分析。

## 怎么干

### 1. 安装 ffmpeg

```bash
# macOS
brew install ffmpeg

# 验证安装
ffmpeg -version
```

### 2. 提取单帧

```bash
# 提取第一帧
~/skills/video-frames/scripts/frame.sh video.mp4 --out frame.jpg

# 提取特定时间的帧
~/skills/video-frames/scripts/frame.sh video.mp4 --time 00:00:10 --out frame-10s.jpg

# 提取 1 分钟处的帧
~/skills/video-frames/scripts/frame.sh video.mp4 --time 00:01:00 --out frame-1m.jpg
```

### 3. 批量提取帧

```bash
# 每秒提取 1 帧
ffmpeg -i video.mp4 -vf fps=1 frame_%04d.jpg

# 每 5 秒提取 1 帧
ffmpeg -i video.mp4 -vf fps=1/5 frame_%04d.jpg

# 提取所有 I 帧（关键帧）
ffmpeg -i video.mp4 -vf "select='eq(pict_type,I)'" -vsync vfr keyframe_%04d.jpg
```

### 4. 创建缩略图网格

```bash
# 创建 3x3 缩略图网格
ffmpeg -i video.mp4 -vf "select=not(mod(n\,100)),scale=160:90,tile=3x3" -frames:v 1 grid.jpg

# 创建 4x4 缩略图网格
ffmpeg -i video.mp4 -vf "select=not(mod(n\,200)),scale=120:68,tile=4x4" -frames:v 1 grid.jpg
```

### 5. 提取视频片段

```bash
# 提取 10-20 秒片段
ffmpeg -i video.mp4 -ss 00:00:10 -to 00:00:20 -c copy clip.mp4

# 从 30 秒开始提取 5 秒
ffmpeg -i video.mp4 -ss 00:00:30 -t 5 -c copy clip.mp4
```

### 6. 创建 GIF

```bash
# 从视频片段创建 GIF
ffmpeg -i video.mp4 -ss 00:00:10 -t 3 -vf "fps=10,scale=320:-1" output.gif

# 高质量 GIF（带调色板）
ffmpeg -i video.mp4 -ss 00:00:10 -t 3 -vf "fps=15,scale=480:-1:flags=lanczos,split[s0][s1];[s0]palettegen[p];[s1][p]paletteuse" output.gif
```

### 7. 效果展示

**提取的帧：**
```
output/
├── frame_0001.jpg    # 第 0 秒
├── frame_0002.jpg    # 第 1 秒
├── frame_0003.jpg    # 第 2 秒
├── keyframe_0001.jpg # 关键帧
└── grid.jpg          # 缩略图网格
```

**使用场景：**
- 视频预览图生成
- 关键帧分析
- 封面图选择
- 视频质量检查
- GIF 制作

## 常用参数

| 参数 | 说明 | 示例 |
|------|------|------|
| `-ss` | 起始时间 | `00:00:10` |
| `-to` | 结束时间 | `00:00:20` |
| `-t` | 持续时间 | `5` |
| `-vf fps` | 帧率 | `fps=1` |
| `-vf scale` | 尺寸 | `scale=160:90` |
| `-c copy` | 直接复制 | 快速提取 |

## 最佳实践

**快速提取特定帧：**
```bash
# -ss 放在 -i 前面更快（seek 模式）
ffmpeg -ss 00:01:30 -i video.mp4 -frames:v 1 -q:v 2 frame.jpg
```

**高质量截图：**
```bash
# 使用 PNG 格式保持质量
ffmpeg -i video.mp4 -ss 00:00:10 -frames:v 1 frame.png
```

**自动选择最佳帧：**
```bash
# 提取场景变化帧
ffmpeg -i video.mp4 -vf "select='gt(scene,0.3)'" -vsync vfr scene_%04d.jpg
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| ffmpeg | 视频处理工具 | `brew install ffmpeg` |
| 视频文件 | mp4/mov/avi 等 | 自行准备 |

## 来源

- 贡献者：Community
- 来源：video-frames 技能文档
- 日期：2024

## 相关资源

- [FFmpeg 官方文档](https://ffmpeg.org/documentation.html)
- [FFmpeg 命令速查](https://cheatography.com/themightyted/cheat-sheets/ffmpeg/)
