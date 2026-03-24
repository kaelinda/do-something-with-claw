# Apple Notes 笔记操作

## 真实来源

- **技能**：apple-notes
- **CLI**：memo（macOS 专属）
- **平台**：macOS only

---

## 干什么
通过 OpenClaw 自动化管理 Apple Notes 笔记，包括创建、查看、编辑、删除、搜索、移动和导出。

## 怎么干

### 1. 准备工作

- macOS 系统
- OpenClaw 版本：>= 1.0.0
- memo CLI 已安装（技能自动管理）

### 2. 执行步骤

**方式一：创建笔记**

```
创建一条新笔记：
- 标题：会议纪要 - 产品评审
- 内容：讨论要点、待办事项
- 文件夹：工作
```

**方式二：搜索笔记**

```
搜索我的笔记：
- 关键词：产品
- 限制：最近 7 天
- 输出：标题 + 摘要
```

**方式三：移动笔记**

```
移动笔记到文件夹：
- 笔记：临时笔记
- 目标文件夹：归档
```

**方式四：导出笔记**

```
导出笔记：
- 笔记标题：项目计划
- 格式：Markdown
- 保存到：~/Documents
```

### 3. memo 常用命令

```bash
# 创建笔记
memo add "笔记标题" --body "笔记内容"

# 列出笔记
memo list

# 搜索笔记
memo search "关键词"

# 查看笔记内容
memo show "笔记标题"

# 编辑笔记
memo edit "笔记标题" --body "新内容"

# 移动笔记
memo move "笔记标题" --folder "目标文件夹"

# 删除笔记
memo delete "笔记标题"

# 导出笔记
memo export "笔记标题" --format markdown --output ~/Documents
```

### 4. 效果展示

```
Apple Notes 操作完成！

创建笔记：
- 标题：会议纪要 - 产品评审
- 文件夹：工作
- 创建时间：2026-03-25 10:30

搜索结果（3 条）：
1. 产品规划 Q2 - 更新于 2026-03-24
2. 产品设计规范 - 更新于 2026-03-20
3. 产品路线图 - 更新于 2026-03-15

移动完成：
- 笔记：临时笔记
- 已移动到：归档
- 原位置：工作

导出完成：
- 文件：~/Documents/项目计划.md
- 格式：Markdown
- 大小：2.3 KB
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| macOS | 操作系统 | Apple 设备 |
| OpenClaw | >= 1.0.0 | 官方安装 |
| memo | CLI 工具 | 技能自动安装 |

## 相关资源

- OpenClaw 技能：apple-notes
- [Apple Notes 官方文档](https://support.apple.com/guide/notes/welcome/mac)
