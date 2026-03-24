# Things 3 任务管理

## 真实来源

- **技能**：things-mac
- **CLI**：things（macOS 专属）
- **应用**：Things 3 by Cultured Code
- **平台**：macOS only

---

## 干什么
通过 OpenClaw 自动化管理 Things 3 任务，包括添加、更新、查看、搜索项目和待办事项。

## 怎么干

### 1. 准备工作

- macOS 系统
- Things 3 已安装（App Store 购买）
- OpenClaw 版本：>= 1.0.0

### 2. 执行步骤

**方式一：添加待办**

```
添加一个待办事项：
- 标题：完成产品文档
- 项目：产品规划
- 截止日期：2026-03-28
- 标签：文档、重要
- 备注：需要包含 API 说明
```

**方式二：查看任务**

```
查看今日任务：
- 显示：标题 + 项目 + 截止日期
- 排序：按优先级
```

**方式三：搜索任务**

```
搜索包含"设计"的任务：
- 范围：所有项目和待办
- 输出：匹配结果列表
```

**方式四：添加项目**

```
创建新项目：
- 标题：Q2 产品规划
- 区域：工作
- 描述：第二季度产品迭代计划
```

### 3. things CLI 常用命令

```bash
# 添加待办
things add "完成产品文档" --project "产品规划" --due "2026-03-28" --tag "文档,重要"

# 添加项目
things add-project "Q2 产品规划" --area "工作"

# 查看 Inbox
things inbox

# 查看今日
things today

# 查看即将到来
things upcoming

# 查看某项目下的待办
things project "产品规划"

# 搜索
things search "关键词"

# 查看区域列表
things areas

# 查看项目列表
things projects

# 查看标签列表
things tags

# 完成待办
things complete "待办标题"

# 取消待办
things cancel "待办标题"
```

### 4. 效果展示

```
Things 3 操作完成！

添加待办：
- 标题：完成产品文档
- 项目：产品规划
- 截止：2026-03-28
- 标签：文档, 重要
- 备注：需要包含 API 说明

今日任务（4 条）：
1. [产品规划] 完成产品文档 - 今天
2. [日常工作] 回复邮件 - 今天
3. [个人] 锻炼 - 今天
4. [学习] 阅读《设计心理学》 - 今天

即将到来（本周）：
- 周三：产品评审会议
- 周四：提交周报
- 周五：团队复盘

搜索结果（3 条）：
1. [产品规划] 设计系统规划
2. [日常工作] 设计评审准备
3. [学习] 设计模式学习
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| macOS | 操作系统 | Apple 设备 |
| Things 3 | 任务管理应用 | [App Store](https://apps.apple.com/app/things-3/id904280696) |
| OpenClaw | >= 1.0.0 | 官方安装 |

## 相关资源

- OpenClaw 技能：things-mac
- [Things 3 官网](https://culturedcode.com/things/)
- [Things URL Scheme](https://culturedcode.com/things/support/articles/2803573/)
