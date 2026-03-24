# Obsidian 笔记操作

## 干什么
通过 OpenClaw 自动化管理 Obsidian 笔记库，包括创建、搜索、整理、批量操作等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：obsidian、obsidian-cli、obsidian-markdown、json-canvas
- 需要的配置：Obsidian vault 路径

### 2. 执行步骤

**方式一：创建和编辑笔记**

```
创建一条新笔记：
- Vault：~/Documents/Obsidian/MyVault
- 标题：产品规划 Q2
- 内容：[大纲或内容]
- 标签：#产品 #规划
- 文件夹：产品规划
```

**方式二：搜索笔记**

```
搜索我的 Obsidian 笔记：
- 关键词：产品设计
- 限制：最近 30 天
- 输出：标题 + 摘要 + 链接
```

**方式三：批量操作**

```
批量处理草稿笔记：
1. 搜索所有带 #草稿 标签的笔记
2. 检查创建时间超过 7 天的
3. 提醒用户处理或自动归档
```

**方式四：创建 Canvas**

```
创建一个 Canvas 文件：
- 路径：产品规划/架构图.canvas
- 节点：
  - 前端
  - 后端
  - 数据库
- 连接：前端 → 后端 → 数据库
```

**方式五：笔记整理**

```
整理周报笔记：
1. 搜索本周所有会议笔记
2. 提取待办事项
3. 创建汇总笔记
4. 建立双向链接
```

**OpenClaw 会自动：**
1. 操作 Obsidian vault 文件
2. 生成符合 Obsidian 语法的 Markdown
3. 创建双向链接和标签
4. 支持 Canvas、Bases 等高级功能

### 3. 效果展示

```
Obsidian 笔记操作完成！

创建笔记：
- 文件：产品规划/Q2目标.md
- 链接：obsidian://open?vault=MyVault&file=产品规划/Q2目标
- 标签：#产品 #规划 #Q2

搜索结果（3 条）：
1. 产品规划 Q1.md - 上季度规划回顾...
2. 产品设计规范.md - 设计系统文档...
3. 产品路线图.md - 年度规划概览...

Canvas 创建：
- 文件：架构图.canvas
- 节点数：5
- 连接数：4
- 预览：obsidian://open?vault=MyVault&file=架构图

批量整理：
- 处理笔记：12 篇
- 添加链接：28 个
- 创建索引：产品规划 MOC.md
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Obsidian | 笔记软件 | 官网下载 |
| obsidian-cli | CLI 工具 | 技能安装 |
| obsidian-markdown | Markdown 支持 | 技能安装 |
| json-canvas | Canvas 支持 | 技能安装 |

## 来源

- 贡献者：PM Agent
- 来源：个人知识管理实践
- 日期：2026-03-24

## 相关资源

- [Obsidian 官网](https://obsidian.md)
- [Obsidian CLI 技能文档](https://openclaw.ai/skills/obsidian-cli)
- [Obsidian Markdown 技能文档](https://openclaw.ai/skills/obsidian-markdown)
- [JSON Canvas 技能文档](https://openclaw.ai/skills/json-canvas)
