# 翻译与多语言内容

## 真实来源

- **技能**：gemini
- **场景**：内容翻译、多语言适配

---

## 干什么
使用 OpenClaw 进行内容翻译、多语言适配，支持长文翻译和术语一致性。

## 怎么干

### 1. 准备工作

- OpenClaw 版本：>= 1.0.0
- gemini 技能已安装

### 2. 执行步骤

**方式一：简单翻译**

```
翻译这段文本：
原文：Hello, world!
目标语言：中文
风格：正式
```

**方式二：长文翻译**

```
翻译这篇文章：
[粘贴长文]

要求：
- 保持格式
- 术语一致
- 保留专有名词
```

**方式三：术语表翻译**

```
使用术语表翻译：

术语表：
- API → API（不翻译）
- OpenClaw → OpenClaw（不翻译）
- Skill → 技能

原文：OpenClaw provides various skills for automation.
```

**方式四：批量翻译**

```
批量翻译以下文件：
- README.md → README.zh.md
- CHANGELOG.md → CHANGELOG.zh.md
- docs/guide.md → docs/guide.zh.md
```

### 3. gemini 命令

```bash
# 简单翻译
gemini "翻译成中文：Hello, world!"

# 长文翻译
cat article.md | gemini "翻译成中文，保持格式"

# 带风格翻译
gemini "用口语化的中文翻译：This is a technical document."

# JSON 输出
gemini --json "翻译：Hello"
```

### 4. 效果展示

```
翻译完成！

原文（英文）：
OpenClaw is a powerful automation tool that helps you 
streamline workflows and boost productivity.

译文（中文）：
OpenClaw 是一款强大的自动化工具，可帮助您简化工作流程，
提升工作效率。

统计：
- 原文字数：128
- 译文字数：45
- 术语保留：3 个（OpenClaw, API, Skill）
- 处理时间：2.3 秒

批量翻译结果：
✅ README.md → README.zh.md
✅ CHANGELOG.md → CHANGELOG.zh.md
✅ docs/guide.md → docs/guide.zh.md
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| gemini | 翻译技能 | 技能安装 |

## 相关资源

- OpenClaw 技能：gemini
- OpenClaw 技能：tavily（搜索辅助）
