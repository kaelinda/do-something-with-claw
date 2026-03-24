# 习惯追踪

## 干什么
使用 OpenClaw 建立习惯追踪系统，自动记录习惯完成情况，生成统计报告。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 可选：Apple Reminders、Things 3
- 可选：obsidian 或其他笔记工具

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
```

#### 方式三：使用 Things 3
```bash
# 查看今日任务
things today

# 完成任务
things complete "运动"
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

## 常用功能

### 1. 创建习惯列表
```bash
# 使用 Apple Reminders 创建习惯列表
remindctl new-list "每日习惯"

# 添加习惯项目
remindctl add "运动" --list "每日习惯" --repeat daily
remindctl add "读书" --list "每日习惯" --repeat daily
remindctl add "冥想" --list "每日习惯" --repeat daily
```

### 2. 记录完成
```javascript
// 记录习惯完成
async function completeHabit(habitName) {
  await remindctl.complete(habitName);
  await logHabit(habitName, new Date());
}

// 在日记中记录
await appendToDiary(`- [x] ${habitName}`);
```

### 3. 统计分析
```javascript
// 生成周报告
const weekData = await getHabitData(weekStart, weekEnd);
const stats = calculateStats(weekData);

// 计算完成率
const completionRate = stats.completed / stats.total;
// 计算连续天数
const streak = calculateStreak(habitName);
```

## 高级用法

### 1. 智能提醒
```javascript
// 根据历史数据智能提醒
async function smartRemind() {
  const habits = await getTodayHabits();
  const now = new Date();
  
  for (const habit of habits) {
    if (!habit.completed && habit.usualTime < now) {
      await notify(`还没完成「${habit.name}」哦！`);
    }
  }
}
```

### 2. 习惯链分析
```javascript
// 分析习惯之间的关联
const correlations = analyzeHabitCorrelations(historyData);

// 输出：完成「早起」后，完成「运动」的概率提高 30%
```

### 3. 数据可视化
```javascript
// 生成习惯热力图
const heatmap = generateHabitHeatmap({
  habits: ['运动', '读书', '冥想'],
  period: 'month',
  output: 'habit-heatmap.png'
});
```

### 4. 与其他工具集成
```javascript
// 同步到 Notion
await notion.pages.create({
  parent: { database_id: habitDatabaseId },
  properties: {
    日期: { date: { start: today } },
    习惯: { title: [{ text: { content: habitName } }] },
    状态: { select: { name: '完成' } }
  }
});

// 同步到 Obsidian
await obsidian.appendNote('习惯追踪.md', `- [x] ${habitName} (${today})`);
```

### 5. 周期性报告
```javascript
// 每周日生成报告
schedule.scheduleJob("0 20 * * 0", async () => {
  const report = await generateWeeklyReport();
  await sendMessage(report);
});
```

## 实现示例

### Obsidian 习惯追踪
```markdown
# 习惯追踪

## 2024-01

| 日期 | 运动 | 读书 | 冥想 | 早起 | 备注 |
|------|------|------|------|------|------|
| 01   | ✅   | ✅   | ✅   | ✅   |      |
| 02   | ✅   | ❌   | ✅   | ✅   | 聚会 |
| 03   | ✅   | ✅   | ❌   | ✅   |      |
| ...  | ...  | ...  | ...  | ...  |      |

### 月度统计
- 运动完成：25/31 (81%)
- 读书完成：23/31 (74%)
- 冥想完成：28/31 (90%)
- 早起完成：27/31 (87%)
```

### Apple Reminders 集成
```bash
# 初始化习惯列表
#!/bin/bash
remindctl new-list "每日习惯"
habits=("运动" "读书" "冥想" "早起" "喝水")
for habit in "${habits[@]}"; do
  remindctl add "$habit" --list "每日习惯" --repeat daily
done
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Apple Reminders | 可选 | macOS/iOS 自带 |
| Things 3 | 可选 | App Store |
| Obsidian | 可选 | https://obsidian.md |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [Apple Reminders 技能](https://clawhub.com/skills/apple-reminders)
- [Things 3 技能](https://clawhub.com/skills/things-mac)
- [习惯追踪方法论](https://jamesclear.com/habit-tracker)
