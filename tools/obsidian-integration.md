# Obsidian 笔记操作

## 真实来源

- **技能**：obsidian、obsidian-cli、obsidian-markdown、json-canvas
- **GitHub**：https://github.com/yakitrak/obsidian-cli
- **安装**：`brew install yakitrak/yakitrak/obsidian-cli`

---

## 干什么
通过 OpenClaw 自动化管理 Obsidian 笔记库，包括创建、搜索、整理、批量操作等。

## 怎么干

### 1. 准备工作

```bash
# 安装 obsidian-cli
brew install yakitrak/yakitrak/obsidian-cli

# 设置默认 vault
obsidian-cli set-default "MyVault"
```

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

### 3. obsidian-cli 常用命令

```bash
# 设置默认 vault
obsidian-cli set-default "<vault-folder-name>"

# 获取默认 vault 路径
obsidian-cli print-default --path-only

# 搜索笔记（按名称）
obsidian-cli search "query"

# 搜索内容
obsidian-cli search-content "query"

# 创建笔记
obsidian-cli create "Folder/New note" --content "..." --open

# 移动/重命名（自动更新链接）
obsidian-cli move "old/path/note" "new/path/note"

# 删除笔记
obsidian-cli delete "path/note"
```

### 4. 效果展示

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
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Obsidian | 笔记软件 | [官网下载](https://obsidian.md) |
| obsidian-cli | CLI 工具 | `brew install yakitrak/yakitrak/obsidian-cli` |

## 相关资源

- [Obsidian 官网](https://obsidian.md)
- [obsidian-cli GitHub](https://github.com/yakitrak/obsidian-cli)
- OpenClaw 技能：obsidian、obsidian-cli、obsidian-markdown、json-canvas
