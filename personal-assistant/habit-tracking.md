# 习惯追踪

## 真实来源

- **技能**：apple-reminders, things-mac
- **位置**：
  - `/opt/homebrew/lib/node_modules/openclaw/skills/apple-reminders/`
  - `/opt/homebrew/lib/node_modules/openclaw/skills/things-mac/`
- **CLI 工具**：remindctl, things

---

## 干什么
使用 OpenClaw 建立习惯追踪系统，自动记录习惯完成情况，生成统计报告。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 可选：Apple Reminders（remindctl）
- 可选：Things 3（things CLI）
- 可选：Obsidian 或其他笔记工具

### 2. 执行步骤

#### 方式一：对话式记录
```
用户：今天完成了运动和读书
OpenClaw：✅ 已记录习惯完成
- 运动 ✅
- 读书 ✅

本周进度：5/7 天
```

#### 方式二：使用 Apple Reminders

```bash
# 查看今日习惯
remindctl list --list "每日习惯"

# 完成习惯
remindctl complete "运动"

# 添加新习惯
remindctl add "冥想" --list "每日习惯" --repeat daily
```

#### 方式三：使用 Things 3

```bash
# 查看今日任务
things today

# 完成任务
things add "运动" --completed

# 创建重复任务
things add "读书" --when today --tags "习惯"
```

### 3. 效果展示

**习惯追踪报告：**
```
📊 本周习惯报告 (2024-01-01 ~ 2024-01-07)

习惯完成率：
- 运动      ████████░░ 80%
- 读书      ███████░░░ 70%
- 冥想      ██████░░░░ 60%
- 早起      █████████░ 90%

总完成率：75%
较上周：+5%

🏆 连续记录：
- 早起：14 天
- 运动：7 天
```

## Apple Reminders CLI 参考

### 基本命令

```bash
# 列出提醒
remindctl list [--list LIST_NAME]

# 添加提醒
remindctl add "标题" --list LIST_NAME --repeat daily

# 完成提醒
remindctl complete "标题"

# 删除提醒
remindctl delete "标题"

# JSON 输出
remindctl list --json
```

### 创建习惯列表

```bash
# 创建习惯列表
remindctl new-list "每日习惯"

# 添加习惯项目
remindctl add "运动" --list "每日习惯" --repeat daily
remindctl add "读书" --list "每日习惯" --repeat daily
remindctl add "冥想" --list "每日习惯" --repeat daily
remindctl add "早起" --list "每日习惯" --repeat daily
```

## Things 3 CLI 参考

### 基本命令

```bash
# 查看收件箱
things inbox --limit 50

# 查看今日任务
things today

# 查看即将到来
things upcoming

# 搜索任务
things search "关键词"

# 查看项目
things projects

# 查看区域
things areas

# 查看标签
things tags
```

### 添加任务

```bash
# 基本添加
things add "买牛奶"

# 带备注
things add "买牛奶" --notes "2% + 香蕉"

# 指定项目/区域
things add "订机票" --list "旅行"

# 指定标题下
things add "打包充电器" --list "旅行" --heading "出发前"

# 带标签
things add "看牙医" --tags "健康,电话"

# 清单项
things add "旅行准备" --checklist-item "护照" --checklist-item "机票"

# 指定日期
things add "开会" --when today --deadline 2024-01-15

# 从 STDIN
cat <<'EOF' | things add -
标题行
备注行 1
备注行 2
EOF
```

### 修改任务

```bash
# 先获取 ID
things search "牛奶" --limit 5

# 修改标题
things update --id <UUID> --auth-token <TOKEN> "新标题"

# 修改备注
things update --id <UUID> --auth-token <TOKEN> --notes "新备注"

# 追加备注
things update --id <UUID> --auth-token <TOKEN> --append-notes "..."

# 移动到其他列表
things update --id <UUID> --auth-token <TOKEN> --list "旅行"

# 添加标签
things update --id <UUID> --auth-token <TOKEN> --add-tags "a,b"

# 完成/取消
things update --id <UUID> --auth-token <TOKEN> --completed
things update --id <UUID> --auth-token <TOKEN> --canceled
```

### 预览模式

```bash
# 安全预览（不实际执行）
things --dry-run add "买牛奶"
things --dry-run update --id <UUID> --auth-token <TOKEN> --completed
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Apple Reminders | 可选 | macOS/iOS 自带 |
| Things 3 | 可选 | App Store |
| Obsidian | 可选 | https://obsidian.md |

## 来源

- **技能路径**：
  - `/opt/homebrew/lib/node_modules/openclaw/skills/apple-reminders/SKILL.md`
  - `/opt/homebrew/lib/node_modules/openclaw/skills/things-mac/SKILL.md`
- **Things CLI 项目**：https://github.com/ossianhempel/things3-cli

## 相关资源

- [Apple Reminders 集成](tools/apple-reminders-integration.md)
- [Things 3 任务管理](tools/things-integration.md)
- [习惯追踪方法论](https://jamesclear.com/habit-tracker)
