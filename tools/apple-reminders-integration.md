# Apple Reminders 任务管理

## 真实来源

- **技能**：apple-reminders
- **CLI**：remindctl（macOS 专属）
- **平台**：macOS only

---

## 干什么
通过 OpenClaw 自动化管理 Apple Reminders 提醒事项，包括添加、查看、编辑、完成、删除任务。

## 怎么干

### 1. 准备工作

- macOS 系统
- OpenClaw 版本：>= 1.0.0
- remindctl CLI 已安装（技能自动管理）

### 2. 执行步骤

**方式一：添加任务**

```
添加一个提醒：
- 标题：提交周报
- 截止时间：周五 18:00
- 列表：工作
- 优先级：高
```

**方式二：查看任务**

```
查看今日待办：
- 列表：所有列表
- 时间范围：今天
- 输出：标题 + 截止时间 + 优先级
```

**方式三：完成任务**

```
标记任务完成：
- 标题：提交周报
- 列表：工作
```

**方式四：搜索任务**

```
搜索包含"会议"的任务：
- 关键词：会议
- 输出：匹配的任务列表
```

### 3. remindctl 常用命令

```bash
# 列出所有列表
remindctl list lists

# 列出任务
remindctl list todos --list "工作"

# 添加任务
remindctl add "提交周报" --list "工作" --due "2026-03-28 18:00" --priority high

# 查看今日任务
remindctl list todos --due-today

# 完成任务
remindctl complete "提交周报" --list "工作"

# 删除任务
remindctl delete "任务标题" --list "工作"

# 搜索任务
remindctl search "关键词"

# JSON 输出
remindctl list todos --json
```

### 4. 效果展示

```
Apple Reminders 操作完成！

添加任务：
- 标题：提交周报
- 列表：工作
- 截止：2026-03-28 18:00
- 优先级：高

今日待办（5 条）：
1. [高] 提交周报 - 今天 18:00
2. [中] 参加产品评审 - 14:00
3. [低] 整理邮件 - 无截止
4. [中] 回复客户消息 - 16:00
5. [中] 准备下周计划 - 无截止

任务已完成：
- 标题：提交周报
- 完成时间：2026-03-25 15:30
- 已从列表移除
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| macOS | 操作系统 | Apple 设备 |
| OpenClaw | >= 1.0.0 | 官方安装 |
| remindctl | CLI 工具 | 技能自动安装 |

## 相关资源

- OpenClaw 技能：apple-reminders
- [Apple Reminders 官方文档](https://support.apple.com/guide/reminders/welcome/mac)
