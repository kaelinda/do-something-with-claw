# 笔记整理与知识管理

## 干什么
使用 Obsidian CLI 自动整理笔记、创建知识索引、建立双向链接，构建个人知识库。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：obsidian、obsidian-cli、obsidian-markdown
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

```
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

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Obsidian | 笔记软件 | 官网下载 |
| obsidian-cli | CLI 工具 | 技能安装 |
| obsidian-markdown | Markdown 支持 | 技能安装 |

## 来源

- 贡献者：Community
- 来源：Obsidian 工作流实践
- 日期：2024

## 相关资源

- [Obsidian CLI 技能文档](https://openclaw.ai/skills/obsidian-cli)
- [Obsidian Markdown 技能文档](https://openclaw.ai/skills/obsidian-markdown)
- [Obsidian 官网](https://obsidian.md)
