# 目标管理

## 干什么
使用 OpenClaw 进行目标管理，包括目标设定、进度追踪、里程碑提醒等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 可选：Things 3、Obsidian、飞书多维表格

### 2. 执行步骤

#### 方式一：对话式管理
```
用户：帮我把「完成项目上线」拆分成可执行的里程碑
OpenClaw：已拆分目标「完成项目上线」：

1. 需求评审（预计 3 天）
2. 设计确认（预计 2 天）
3. 开发完成（预计 10 天）
4. 测试验收（预计 5 天）
5. 正式上线（预计 1 天）

预计总时长：21 天
需要我帮你创建任务吗？
```

#### 方式二：使用 Things 3
```bash
# 创建项目目标
things add-project "完成项目上线" \
  --tasks "需求评审,设计确认,开发完成,测试验收,正式上线"

# 查看项目进度
things show "完成项目上线"
```

#### 方式三：使用飞书多维表格
```javascript
// 创建目标追踪表
await feishu_bitable_create_record({
  app_token: "your-app-token",
  table_id: "goals-table",
  fields: {
    目标名称: "完成项目上线",
    截止日期: "2024-03-31",
    负责人: "张三",
    状态: "进行中",
    进度: 30
  }
});
```

### 3. 效果展示

**目标看板：**
```
🎯 目标管理看板

年度目标：
├── 技术成长
│   ├── 学习 Rust（进度：60%）
│   ├── 完成开源项目（进度：30%）
│   └── 写 12 篇技术博客（进度：75%）
│
├── 健康管理
│   ├── 减重 5kg（进度：40%）
│   ├── 每周运动 3 次（进度：80%）
│   └── 完成马拉松（进度：0%）
│
└── 财务规划
    ├── 存款目标（进度：50%）
    └── 投资学习（进度：100%）

总进度：54%
```

## 常用功能

### 1. SMART 目标设定
```javascript
// 检查目标是否符合 SMART 原则
function validateSMART(goal) {
  return {
    specific: goal.description ? '✅' : '❌ 具体',
    measurable: goal.metrics ? '✅' : '❌ 可衡量',
    achievable: goal.resources ? '✅' : '❌ 可实现',
    relevant: goal.alignment ? '✅' : '❌ 相关性',
    timeBound: goal.deadline ? '✅' : '❌ 有时限'
  };
}
```

### 2. 目标拆解
```javascript
// 将大目标拆解为里程碑
function breakDownGoal(goal) {
  const milestones = [];
  
  // 按时间拆解
  const phases = ['准备', '执行', '收尾'];
  
  // 按复杂度拆解
  const tasks = identifyTasks(goal);
  
  // 估算时间
  const estimates = estimateEffort(tasks);
  
  return milestones;
}
```

### 3. 进度追踪
```javascript
// 计算目标完成进度
async function calculateProgress(goalId) {
  const tasks = await getTasks(goalId);
  const completed = tasks.filter(t => t.status === 'done');
  const progress = (completed.length / tasks.length) * 100;
  
  return {
    total: tasks.length,
    completed: completed.length,
    progress: progress.toFixed(1) + '%'
  };
}
```

### 4. 风险预警
```javascript
// 检测目标风险
async function detectRisks(goal) {
  const risks = [];
  
  // 时间风险
  if (goal.daysRemaining < goal.estimatedDays * 0.3) {
    risks.push({ type: 'time', severity: 'high', message: '时间紧迫' });
  }
  
  // 进度风险
  if (goal.progress < 50 && goal.timePassed > 70) {
    risks.push({ type: 'progress', severity: 'medium', message: '进度滞后' });
  }
  
  return risks;
}
```

## 高级用法

### 1. OKR 管理
```markdown
# Q1 OKR

## Objective: 提升产品用户体验

### Key Results:
- [ ] 用户满意度从 80% 提升到 90%（当前：85%）
- [ ] 页面加载时间降低 50%（当前：降低 30%）
- [ ] 用户留存率提升 10%（当前：提升 5%）

### 进度追踪：
| 周次 | KR1 | KR2 | KR3 | 备注 |
|------|-----|-----|-----|------|
| W1   | 82% | 20% | 2%  |      |
| W2   | 84% | 25% | 3%  |      |
| W3   | 85% | 30% | 5%  |      |
```

### 2. 目标关联分析
```javascript
// 分析目标之间的依赖关系
function analyzeDependencies(goals) {
  const graph = buildDependencyGraph(goals);
  
  // 识别关键路径
  const criticalPath = findCriticalPath(graph);
  
  // 识别阻塞目标
  const blocked = findBlockedGoals(graph);
  
  return { criticalPath, blocked };
}
```

### 3. 定期回顾
```javascript
// 每周目标回顾
schedule.scheduleJob("0 20 * * 5", async () => {
  const weeklyReport = await generateWeeklyReview();
  await sendMessage({
    channel: "feishu",
    message: weeklyReport
  });
});
```

### 4. 激励机制
```javascript
// 完成目标时的奖励通知
async function celebrateGoalCompletion(goal) {
  const message = `🎉 恭喜完成目标「${goal.name}」！
  
历时：${goal.duration} 天
里程碑：${goal.milestones.length} 个

继续保持！💪`;

  await notify(message);
}
```

## 数据存储方案

### Obsidian 方案
```markdown
---
type: goal
status: active
deadline: 2024-03-31
progress: 60
---

# 完成项目上线

## 目标描述
将新功能模块从开发到上线，确保质量达标。

## 里程碑
- [x] 需求评审
- [x] 设计确认
- [ ] 开发完成
- [ ] 测试验收
- [ ] 正式上线

## 进度记录
- 2024-01-15: 完成需求评审
- 2024-01-18: 设计方案确认
- 2024-02-01: 开发进度 50%
```

### 飞书多维表格方案
```
| 字段名 | 类型 | 说明 |
|--------|------|------|
| 目标名称 | 文本 | 目标标题 |
| 描述 | 多行文本 | 详细描述 |
| 截止日期 | 日期 | 目标期限 |
| 进度 | 数字 | 0-100 |
| 状态 | 单选 | 进行中/已完成/暂停 |
| 负责人 | 人员 | 负责人 |
| 关联目标 | 双向关联 | 目标依赖 |
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Things 3 | 可选 | App Store |
| Obsidian | 可选 | https://obsidian.md |
| 飞书 | 可选 | https://feishu.cn |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [SMART 目标原则](https://www.mindtools.com/a4wo118/smart-goals)
- [OKR 管理方法](https://www.whatmatters.com/)
- [Things 3 技能](https://clawhub.com/skills/things-mac)
