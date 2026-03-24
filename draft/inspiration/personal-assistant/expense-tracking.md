# 记账助手

## 干什么
使用 OpenClaw 进行日常记账，自动记录支出、生成财务报告、分析消费习惯。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 可选：飞书多维表格、Notion、Obsidian

### 2. 执行步骤

#### 方式一：对话式记账
```
用户：今天午饭花了 35 元
OpenClaw：✅ 已记录支出
- 日期：2024-01-15
- 类别：餐饮
- 金额：35 元
- 备注：午饭

本月餐饮支出：1,280 元
本月总支出：3,560 元
```

#### 方式二：批量记账
```
用户：记录今天的支出
- 地铁：6 元
- 午餐：35 元
- 咖啡：28 元
- 晚餐：45 元

OpenClaw：✅ 已批量记录 4 笔支出
今日支出：114 元
```

#### 方式三：语音记账
```
用户：[语音] 记一笔，超市购物 158 元
OpenClaw：[语音识别] → [记录]
✅ 已记录：
- 类别：购物
- 金额：158 元
```

### 3. 效果展示

**月度财务报告：**
```
📊 2024年1月 财务报告

## 收支概况
收入：15,000 元
支出：8,560 元
结余：6,440 元
储蓄率：43%

## 支出分类
餐饮     ████████████ 2,580 元 (30%)
房租     ██████████ 2,000 元 (23%)
交通     ████ 720 元 (8%)
购物     ████ 680 元 (8%)
娱乐     ███ 450 元 (5%)
其他     █████████ 2,130 元 (26%)

## 对比分析
较上月：
- 总支出 +12%
- 餐饮支出 +18% ⚠️
- 购物支出 -25% ✅

## 建议
餐饮支出偏高，建议控制在 2,000 元以内
```

## 常用功能

### 1. 快速记账
```javascript
// 记录单笔支出
async function recordExpense(amount, category, note) {
  const record = {
    date: new Date(),
    type: 'expense',
    amount: amount,
    category: category,
    note: note
  };
  
  await saveToDatabase(record);
  return record;
}
```

### 2. 分类统计
```javascript
// 按类别统计
async function getExpensesByCategory(startDate, endDate) {
  const expenses = await queryExpenses(startDate, endDate);
  const grouped = groupBy(expenses, 'category');
  
  return Object.entries(grouped).map(([category, items]) => ({
    category,
    total: sum(items.map(i => i.amount)),
    count: items.length
  }));
}
```

### 3. 预算管理
```javascript
// 设置月度预算
const budgets = {
  '餐饮': 2000,
  '交通': 500,
  '购物': 1000,
  '娱乐': 500
};

// 检查预算
async function checkBudget(category) {
  const spent = await getMonthSpent(category);
  const budget = budgets[category];
  const remaining = budget - spent;
  
  if (remaining < budget * 0.2) {
    await notify(`⚠️「${category}」预算即将用完，剩余 ${remaining} 元`);
  }
}
```

### 4. 周期报告
```javascript
// 生成周报告
async function generateWeeklyReport() {
  const week = getWeekRange();
  const expenses = await queryExpenses(week.start, week.end);
  
  return {
    total: sum(expenses.map(e => e.amount)),
    byDay: groupByDay(expenses),
    byCategory: groupByCategory(expenses),
    topExpenses: getTopExpenses(expenses, 5)
  };
}
```

## 高级用法

### 1. 智能分类
```javascript
// 基于描述自动分类
function autoCategorize(description) {
  const rules = {
    '餐饮': ['午餐', '晚餐', '外卖', '餐厅', '奶茶', '咖啡'],
    '交通': ['地铁', '公交', '打车', '滴滴', '加油'],
    '购物': ['超市', '淘宝', '京东', '便利店'],
    '娱乐': ['电影', '游戏', 'KTV', '门票']
  };
  
  for (const [category, keywords] of Object.entries(rules)) {
    if (keywords.some(k => description.includes(k))) {
      return category;
    }
  }
  return '其他';
}
```

### 2. 消费分析
```javascript
// 分析消费习惯
async function analyzeSpendingHabits() {
  const history = await getHistoryMonths(6);
  
  return {
    avgMonthly: average(history.map(h => h.total)),
    trend: calculateTrend(history),
    unusualSpending: detectAnomalies(history),
    suggestions: generateSuggestions(history)
  };
}
```

### 3. 定期支出提醒
```javascript
// 固定支出提醒
const recurringExpenses = [
  { day: 1, name: '房租', amount: 2000 },
  { day: 15, name: '订阅服务', amount: 100 }
];

schedule.scheduleJob("0 9 * * *", async () => {
  const today = new Date().getDate();
  const due = recurringExpenses.find(e => e.day === today);
  if (due) {
    await notify(`今日固定支出：${due.name} ${due.amount} 元`);
  }
});
```

### 4. 多账户管理
```javascript
// 支持多账户
const accounts = {
  cash: { name: '现金', balance: 500 },
  alipay: { name: '支付宝', balance: 2000 },
  wechat: { name: '微信', balance: 1500 },
  card: { name: '银行卡', balance: 10000 }
};

// 记账时选择账户
async function recordExpense(amount, category, account) {
  accounts[account].balance -= amount;
  await saveRecord({ amount, category, account });
}
```

### 5. 导出报告
```javascript
// 导出为 CSV
async function exportToCSV(startDate, endDate) {
  const records = await queryRecords(startDate, endDate);
  const csv = records.map(r => 
    `${r.date},${r.type},${r.category},${r.amount},${r.note}`
  ).join('\n');
  
  return csv;
}

// 生成可视化图表
async function generateCharts(records) {
  // 饼图：支出分类占比
  // 折线图：每日支出趋势
  // 柱状图：月度对比
}
```

## 数据存储方案

### 飞书多维表格
```
| 字段名 | 类型 | 说明 |
|--------|------|------|
| 日期 | 日期 | 交易日期 |
| 类型 | 单选 | 收入/支出 |
| 金额 | 数字 | 交易金额 |
| 类别 | 单选 | 餐饮/交通/购物等 |
| 账户 | 单选 | 支付宝/微信/现金等 |
| 备注 | 文本 | 详细说明 |
```

### Obsidian 方案
```markdown
# 2024-01 账单

## 2024-01-15
- 午餐 35 元 #餐饮 #支付宝
- 地铁 6 元 #交通 #微信
- 咖啡 28 元 #餐饮 #支付宝
- 晚餐 45 元 #餐饮 #微信

## 本月统计
- 总支出：3,560 元
- 总收入：15,000 元
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 飞书 | 可选 | https://feishu.cn |
| Obsidian | 可选 | https://obsidian.md |

## 隐私说明

- 记账数据存储在用户自己的设备或账户中
- 不会上传到第三方服务器
- 建议定期备份账单数据

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [飞书多维表格技能](https://clawhub.com/skills/feishu-bitable)
- [记账最佳实践](https://www.reddit.com/r/personalfinance/wiki/budgeting)
