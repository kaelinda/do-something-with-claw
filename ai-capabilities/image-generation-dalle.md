# 图像生成

## 真实来源

- **技能**：openai-image-gen
- **API**：OpenAI Images API
- **模型**：DALL-E 3

---

## 干什么
通过 OpenClaw 批量生成 AI 图像，支持随机 Prompt 采样和 HTML 画廊展示。

## 怎么干

### 1. 准备工作

- OpenAI API Key
- OpenClaw 版本：>= 1.0.0
- openai-image-gen 技能已安装

### 2. 执行步骤

**方式一：单张生成**

```
生成一张图像：
- Prompt：一只穿着宇航服的猫在月球上
- 尺寸：1024x1024
- 风格：vivid
- 保存到：~/Pictures/ai-generated/
```

**方式二：批量生成**

```
批量生成产品宣传图：
- 主题：科技产品
- 数量：10 张
- 风格：现代、简约
- 用途：社交媒体
```

**方式三：随机 Prompt 采样**

```
使用 Prompt 池随机生成：
- Prompt 文件：prompts.txt
- 采样数量：5
- 每个生成 2 个变体
```

**方式四：生成画廊**

```
生成图像并创建画廊：
- 图像：已生成的 10 张
- 画廊文件：gallery.html
- 样式：网格布局
```

### 3. 配置示例

```bash
# 设置 API Key（在环境变量中）
export OPENAI_API_KEY="sk-..."

# 生成单张
openai-image-gen "一只穿着宇航服的猫在月球上" --output ~/Pictures/

# 批量生成
openai-image-gen --prompts prompts.txt --count 10 --output ./output/

# 生成画廊
openai-image-gen --prompts prompts.txt --gallery
```

### 4. 效果展示

```
图像生成完成！

生成配置：
- 模型：DALL-E 3
- 尺寸：1024x1024
- 质量：standard
- 风格：vivid

生成结果：
1. astronaut-cat-001.png (1.2 MB)
2. astronaut-cat-002.png (1.1 MB)
3. astronaut-cat-003.png (1.3 MB)

画廊已创建：
- 文件：gallery/index.html
- 图像：gallery/images/
- 可在浏览器中打开预览

Prompt 采样示例：
- "A serene Japanese garden at sunset"
- "A futuristic city with flying cars"
- "An underwater palace made of coral"
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| OpenAI API Key | API 访问凭证 | [OpenAI Platform](https://platform.openai.com/) |
| openai-image-gen | 技能 | 技能安装 |

## 费用说明

- DALL-E 3 (1024x1024): $0.04/张
- DALL-E 3 (1024x1792, 1792x1024): $0.08/张
- DALL-E 2 (1024x1024): $0.02/张

## 相关资源

- OpenClaw 技能：openai-image-gen
- [OpenAI Images API](https://platform.openai.com/docs/api-reference/images)
