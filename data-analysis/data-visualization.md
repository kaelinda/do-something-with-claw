# 数据可视化

## 真实来源

- **工具**：exec（调用 Python 可视化库）
- **Python 库**：matplotlib, seaborn, plotly
- **安装方式**：`pip install matplotlib seaborn plotly`

---

## 干什么
让 OpenClaw 调用 Python 可视化库，将数据转换为图表，支持折线图、柱状图、饼图、散点图等多种类型。

## 怎么干

### 1. 准备工作

- OpenClaw 版本：>= 1.0.0
- Python 环境：>= 3.8
- 安装依赖：`pip install matplotlib seaborn plotly pandas`

### 2. 执行步骤

**方式一：从数据生成图表**

```
将以下销售数据可视化：

月份,销售额,订单数
2024-01,125000,450
2024-02,138000,520
2024-03,142000,485
2024-04,156000,510

要求：
- 生成柱状图展示销售额
- 生成折线图展示趋势
- 添加标题和图例
```

**OpenClaw 会生成 Python 脚本并执行：**

```python
import matplotlib.pyplot as plt
import pandas as pd

# 数据
data = {
    '月份': ['2024-01', '2024-02', '2024-03', '2024-04'],
    '销售额': [125000, 138000, 142000, 156000],
    '订单数': [450, 520, 485, 510]
}
df = pd.DataFrame(data)

# 创建柱状图
fig, ax = plt.subplots(figsize=(10, 6))
ax.bar(df['月份'], df['销售额'], color='steelblue')
ax.set_xlabel('月份')
ax.set_ylabel('销售额')
ax.set_title('月度销售额')

plt.savefig('/tmp/sales_chart.png')
plt.close()
```

**方式二：使用 exec 工具**

```bash
# OpenClaw 执行 Python 脚本
openclaw exec -- python3 << 'EOF'
import matplotlib.pyplot as plt
import pandas as pd

data = {'月份': ['1月', '2月', '3月', '4月'], 
        '销售额': [125000, 138000, 142000, 156000]}
df = pd.DataFrame(data)

plt.figure(figsize=(10, 6))
plt.bar(df['月份'], df['销售额'])
plt.title('月度销售额')
plt.savefig('/tmp/chart.png')
EOF
```

### 3. 效果展示

**柱状图输出：**
```
销售额月度对比

销售额
160K ┤              ████
150K ┤         ████ ████
140K ┤    ████ ████ ████
130K ┤███ ████ ████ ████ ████
120K ┤███ ████ ████ ████ ████
     └────────────────────
       1月  2月  3月  4月

数据标注：
1月：125,000
2月：138,000 (+10.4%)
3月：142,000 (+2.9%)
4月：156,000 (+9.9%)
```

## 常用图表类型

### 柱状图

```python
import matplotlib.pyplot as plt

categories = ['A', 'B', 'C', 'D']
values = [23, 45, 56, 78]

plt.bar(categories, values)
plt.title('柱状图示例')
plt.savefig('/tmp/bar_chart.png')
```

### 折线图

```python
import matplotlib.pyplot as plt

months = ['1月', '2月', '3月', '4月']
sales = [100, 120, 115, 140]

plt.plot(months, sales, marker='o')
plt.title('月度趋势')
plt.savefig('/tmp/line_chart.png')
```

### 饼图

```python
import matplotlib.pyplot as plt

labels = ['餐饮', '交通', '购物', '娱乐']
sizes = [30, 15, 25, 30]

plt.pie(sizes, labels=labels, autopct='%1.1f%%')
plt.title('支出占比')
plt.savefig('/tmp/pie_chart.png')
```

### 散点图

```python
import matplotlib.pyplot as plt
import numpy as np

x = np.random.rand(50)
y = np.random.rand(50)

plt.scatter(x, y)
plt.title('散点图示例')
plt.savefig('/tmp/scatter_chart.png')
```

## 高级用法

### 多子图

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(2, 2, figsize=(12, 10))

# 子图1：柱状图
axes[0, 0].bar(['A', 'B', 'C'], [10, 20, 15])
axes[0, 0].set_title('柱状图')

# 子图2：折线图
axes[0, 1].plot([1, 2, 3, 4], [10, 15, 13, 18])
axes[0, 1].set_title('折线图')

# 子图3：饼图
axes[1, 0].pie([30, 40, 30], labels=['X', 'Y', 'Z'])
axes[1, 0].set_title('饼图')

# 子图4：散点图
axes[1, 1].scatter([1, 2, 3], [3, 2, 4])
axes[1, 1].set_title('散点图')

plt.tight_layout()
plt.savefig('/tmp/multi_chart.png')
```

### Seaborn 热力图

```python
import seaborn as sns
import matplotlib.pyplot as plt

data = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
sns.heatmap(data, annot=True, cmap='coolwarm')
plt.title('热力图')
plt.savefig('/tmp/heatmap.png')
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Python | >= 3.8 | 系统安装 |
| matplotlib | 可视化库 | `pip install matplotlib` |
| seaborn | 高级图表 | `pip install seaborn` |
| plotly | 交互图表 | `pip install plotly` |

## 相关资源

- [Matplotlib 官方文档](https://matplotlib.org/)
- [Seaborn 官方文档](https://seaborn.pydata.org/)
- [Plotly 官方文档](https://plotly.com/python/)
