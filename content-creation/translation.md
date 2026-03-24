# 翻译内容

## 干什么
让 OpenClaw 帮你翻译多语言内容，支持术语管理、上下文理解、专业领域翻译。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：无（内置翻译能力）
- 需要的配置：可选术语表

### 2. 执行步骤

**方式一：简单翻译**

```
翻译这段内容为英文：
"OpenClaw 是一个强大的 AI 助手框架，支持多模态交互和自动化工作流。"
```

**方式二：专业领域翻译**

```
翻译以下技术文档为中文，注意保持专业术语的准确性：
[paste your technical document]

要求：
- 保持代码块不翻译
- 专业术语保留英文或使用标准译法
- 保持 Markdown 格式
```

**方式三：多语言批量翻译**

```
批量翻译以下内容到日语、韩语、法语：
1. "欢迎使用 OpenClaw"
2. "自动化你的工作流程"
3. "提升你的效率"

输出格式：
原文 | 日语 | 韩语 | 法语
```

**方式四：术语管理翻译**

```
使用以下术语表翻译：
- Agent -> 智能体
- Workflow -> 工作流
- Skill -> 技能

待翻译内容：
[paste content]
```

**OpenClaw 会自动：**
1. 识别内容语言和目标语言
2. 理解上下文和专业领域
3. 应用术语管理规则
4. 保持格式和结构
5. 输出高质量翻译

### 3. 效果展示

**输入：**
```
OpenClaw enables developers to build AI-powered automation workflows 
with natural language interfaces.
```

**输出：**
```
OpenClaw 让开发者能够用自然语言界面构建 AI 驱动的自动化工作流。
```

**术语管理示例：**
```
原文：The Agent uses Skills to complete tasks.
译文：智能体使用技能来完成任务。

术语表已应用：
✓ Agent -> 智能体
✓ Skills -> 技能
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 无额外依赖 | 内置能力 | - |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [多语言支持文档](https://docs.openclaw.ai/i18n)
- [术语管理指南](https://docs.openclaw.ai/glossary)
