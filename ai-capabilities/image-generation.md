# 图像批量生成与画廊展示

## 干什么
使用 `openai-image-gen` 技能批量生成 AI 图像，并自动创建 HTML 缩略图画廊。

## 怎么干

### 1. 准备工作

```bash
# 确保已安装 OpenClaw
openclaw --version

# 设置 API Key
export OPENAI_API_KEY="sk-your-api-key"

# 确认 Python3 可用
python3 --version
```

### 2. 安装技能

```bash
# 技能已内置，无需单独安装
# 如需检查：
openclaw skill list | grep image
```

### 3. 创建提示词文件

创建 `prompts.txt`，每行一个提示词：

```text
# prompts.txt 示例
一只穿着宇航服的猫咪，站在火星表面，赛博朋克风格
水彩画风格的古老城堡，雾气缭绕的山谷，晨曦微光
日落时分的海边，印象派风格，温暖的色调
未来城市的霓虹街道，雨夜，赛博朋克
```

### 4. 执行命令

```bash
# 基础用法（GPT image model，高质量）
cd ~/Projects/my-images
openai-image-gen --prompts prompts.txt --output ./output

# 使用 DALL-E 3（高清）
openai-image-gen --prompts prompts.txt --output ./output --model dall-e-3 --quality hd

# 使用 DALL-E 2（更便宜）
openai-image-gen --prompts prompts.txt --output ./output --model dall-e-2

# 指定图像数量（随机采样）
openai-image-gen --prompts prompts.txt --output ./output --count 5
```

### 5. 输出结构

```
output/
├── image_001.png      # 生成的图像
├── image_002.png
├── image_003.png
├── prompts.json       # 提示词 → 文件映射
└── index.html         # 缩略图画廊（可直接打开）
```

### 6. 效果展示

**命令行输出：**
```
🎨 Generating images with GPT Image Model (quality: high)
📝 Loaded 10 prompts from prompts.txt
🖼️ Generating image 1/10...
🖼️ Generating image 2/10...
...
✅ Generated 10 images
📊 Gallery saved to output/index.html
```

**打开画廊：**
```bash
open output/index.html
# 或在浏览器中打开
```

## 模型对比

| 模型 | 质量 | 价格 | 特点 |
|------|------|------|------|
| `gpt-image-1` | high/medium/low | 按质量定价 | 最新模型，推荐 |
| `dall-e-3` | hd/standard | $0.04-0.08 | 高质量，单张生成 |
| `dall-e-2` | standard | $0.02 | 最便宜，可多张 |

## 高级参数

```bash
# GPT Image Model 专属
--background transparent    # 透明背景
--background opaque         # 不透明背景
--output-format webp        # 输出格式：png/jpeg/webp

# DALL-E 3 专属
--style vivid              # 戏剧性风格
--style natural            # 自然风格
```

## 常见问题

**Q: 生成失败怎么办？**
```bash
# 检查 API Key 是否有效
curl https://api.openai.com/v1/models \
  -H "Authorization: Bearer $OPENAI_API_KEY"

# 检查余额
# 登录 platform.openai.com 查看 Usage
```

**Q: 如何生成透明背景图？**
```bash
# 仅 GPT Image Model 支持
openai-image-gen --prompts prompts.txt --background transparent
```

**Q: 如何获取高清图？**
```bash
# DALL-E 3 HD 模式
openai-image-gen --prompts prompts.txt --model dall-e-3 --quality hd
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Python 3 | 运行环境 | 系统自带 |
| OpenAI API Key | 调用图像 API | platform.openai.com |

## 来源

- 贡献者：Community
- 来源：openai-image-gen 技能文档
- 日期：2024

## 相关资源

- [OpenAI Images API](https://platform.openai.com/docs/api-reference/images)
- [技能源码](https://github.com/openclaw/openclaw/tree/main/skills/openai-image-gen)
