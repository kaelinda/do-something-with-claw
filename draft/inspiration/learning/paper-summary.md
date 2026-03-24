# 论文/文章摘要生成

## 干什么
快速提取论文、文章、报告的核心内容，生成结构化摘要，支持多种输出格式。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：summarize
- 需要的配置：无

### 2. 执行步骤

**方式一：从 URL 提取**

```
帮我总结这篇文章：
https://arxiv.org/abs/2403.xxxxx

重点关注：
- 核心创新点
- 实验方法
- 主要结论
```

**方式二：从本地文件**

```
总结这个 PDF 论文：
~/Documents/papers/attention-is-all-you-need.pdf

输出格式：
- 一句话摘要
- 方法论要点
- 实验结果
- 局限性
```

**方式三：批量处理**

```
批量总结这个文件夹下的论文：
~/Documents/papers/

每篇输出：
- 标题
- 作者
- 一句话摘要
- 关键词（5 个）
```

**OpenClaw 会自动：**
1. 解析文档内容
2. 识别关键信息
3. 生成结构化摘要
4. 支持多种输出格式

### 3. 效果展示

```markdown
# 论文摘要 | Attention Is All You Need

**标题**：Attention Is All You Need
**作者**：Vaswani et al. (Google Brain)
**发表**：NeurIPS 2017

## 一句话摘要
提出了 Transformer 架构，完全基于注意力机制，抛弃了传统的循环和卷积结构。

## 核心创新
1. **自注意力机制**：计算序列中每个位置与其他所有位置的关系
2. **多头注意力**：并行多个注意力头，捕获不同的表示子空间
3. **位置编码**：使用正弦函数注入位置信息

## 方法论
- 编码器-解码器架构
- 6 层编码器，6 层解码器
- 每层包含多头注意力和前馈网络

## 实验结果
- WMT 英德翻译：BLEU 28.4（SOTA）
- WMT 英法翻译：BLEU 41.8（SOTA）
- 训练速度比传统方法快 10 倍

## 局限性
- 对长序列的注意力计算复杂度 O(n²)
- 需要大量训练数据
- 计算资源需求高

## 关键词
Transformer, Self-Attention, NMT, Neural Network, Deep Learning
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| summarize | 摘要技能 | 技能安装 |

## 来源

- 贡献者：Community
- 来源：学术研究实践
- 日期：2024

## 相关资源

- [Summarize 技能文档](https://openclaw.ai/skills/summarize)
- [Defuddle 技能文档](https://openclaw.ai/skills/defuddle)
