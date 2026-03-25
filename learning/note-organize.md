# 笔记整理与知识管理

## 真实来源

- **技能**：obsidian-cli, obsidian-markdown, obsidian, json-canvas, obsidian-bases
- **位置**：
  - `/opt/homebrew/lib/node_modules/openclaw/skills/obsidian/`
  - `~/.openclaw/workspace-pm/.agents/skills/obsidian-cli/`
  - `~/.openclaw/workspace-pm/.agents/skills/obsidian-markdown/`
- **CLI 工具**：obsidian-cli

---

## 干什么
使用 Obsidian CLI 自动整理笔记、创建知识索引、建立双向链接，构建个人知识库。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：obsidian-cli、obsidian-markdown
- 需要的配置：Obsidian vault 路径

### 2. 执行步骤

**给 OpenClaw 发送指令：**

```
帮我整理 Obsidian 笔记：
1. 扫描所有未分类的笔记
2. 按主题归类到对应文件夹
3. 创建标签索引
4. 建立相关笔记的双向链接
```

**具体操作示例：**

```bash
# 搜索笔记
obsidian search "产品设计"

# 创建新笔记
obsidian create "产品规划/Q2目标" --template weekly

# 批量添加标签
obsidian tag add "#待整理" --folder drafts

# 生成知识索引
obsidian index --format MOC
```

**OpenClaw 会自动：**
1. 扫描 vault 中的所有笔记
2. 分析笔记内容和主题
3. 按规则归类到文件夹
4. 创建标签和索引页
5. 建立笔记间的双向链接

### 3. 效果展示

```
笔记整理完成！

分类结果：
- 产品相关：12 篇 → /产品规划/
- 技术学习：8 篇 → /技术笔记/
- 会议记录：5 篇 → /会议纪要/
- 待整理：3 篇（标记 #待分类）

新增链接：
- [[Q2目标]] ↔ [[产品路线图]]
- [[搜索优化]] ↔ [[用户反馈分析]]
- [[技术方案]] ↔ [[架构设计]]

索引页生成：
- 产品规划 MOC.md
- 技术学习 MOC.md
- 标签索引.md
```

## obsidian-cli 常用命令

### 基本操作

```bash
# 查看帮助
obsidian --help

# 打开 vault
obsidian open /path/to/vault

# 列出笔记
obsidian list

# 搜索笔记
obsidian search "关键词"

# 创建笔记
obsidian create "笔记标题" --folder "文件夹"

# 读取笔记
obsidian read "笔记标题"

# 编辑笔记
obsidian edit "笔记标题" --content "内容"
```

### 高级操作

```bash
# 使用模板创建
obsidian create "日报" --template daily

# 添加标签
obsidian tag add "#标签" "笔记标题"

# 添加属性
obsidian property set "status" "done" "笔记标题"

# 重命名笔记
obsidian rename "旧标题" "新标题"

# 移动笔记
obsidian move "笔记标题" --folder "目标文件夹"

# 删除笔记
obsidian delete "笔记标题"
```

### 调试与开发

```bash
# 重载插件
obsidian reload-plugin "插件名"

# 运行 JavaScript
obsidian eval "console.log('hello')"

# 捕获错误
obsidian errors

# 截图
obsidian screenshot --output screenshot.png

# 检查 DOM
obsidian inspect "选择器"
```

## Obsidian Markdown 语法

obsidian-markdown 技能支持 Obsidian 特有的 Markdown 语法：

### Wikilinks

```markdown
[[笔记标题]]
[[笔记标题|显示文本]]
[[笔记标题#标题]]
[[笔记标题#标题|显示文本]]
```

### 嵌入

```markdown
![[笔记标题]]
![[图片.png]]
![[PDF文件.pdf]]
```

### Callouts

```markdown
> [!note] 笔记
> 这是一个笔记

> [!tip] 提示
> 这是一个提示

> [!warning] 警告
> 这是一个警告
```

### Frontmatter

```markdown
---
title: 笔记标题
date: 2024-01-15
tags: [标签1, 标签2]
status: draft
---
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Obsidian | 笔记软件 | https://obsidian.md |
| obsidian-cli | CLI 工具 | 技能安装 |
| obsidian-markdown | Markdown 支持 | 技能安装 |

## 来源

- **技能路径**：
  - `/opt/homebrew/lib/node_modules/openclaw/skills/obsidian/`
  - `~/.openclaw/workspace-pm/.agents/skills/obsidian-cli/`
  - `~/.openclaw/workspace-pm/.agents/skills/obsidian-markdown/`

## 相关资源

- [Obsidian CLI 技能文档](https://openclaw.ai/skills/obsidian-cli)
- [Obsidian Markdown 技能文档](https://openclaw.ai/skills/obsidian-markdown)
- [Obsidian 官网](https://obsidian.md)
- [Obsidian 集成](tools/obsidian-integration.md)
