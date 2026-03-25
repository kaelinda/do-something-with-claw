# 数据报告生成

## 真实来源

- **工具**：OpenClaw exec + read + write
- **辅助**：feishu-doc 技能、gemini 技能
- **数据处理**：jq、awk、Python

---

## 干什么
自动分析数据源并生成结构化数据报告，支持多种数据格式和输出渠道。

## 怎么干

### 1. 准备工作

- OpenClaw 版本：>= 1.0.0
- 数据源（CSV/Excel/JSON/API/数据库）

### 2. 执行步骤

**方式一：从 CSV/Excel 分析**

```
分析这份销售数据：
~/Documents/data/sales-2026-Q1.csv

生成报告：
1. 销售趋势分析
2. Top 10 产品
3. 区域分布
4. 环比增长率
```

**方式二：从 JSON 日志分析**

```
分析应用日志：
~/logs/app-2026-03.json

统计：
- 错误类型分布
- 错误趋势（按小时）
- Top 5 错误详情
```

**方式三：从 API 获取数据**

```
从飞书多维表格生成报告：
- 表格：[飞书多维表格链接]
- 分析字段：需求状态、优先级分布
- 输出：需求进展报告
```

**方式四：定时报告**

```
设置每周一 9:00 自动生成周报：
- 数据源：GitHub Issues
- 范围：上周创建/关闭的 Issue
- 发送到：飞书群
```

### 3. 数据处理命令

```bash
# CSV 数据统计
awk -F',' '{sum+=$3; count++} END {print "Total:", sum, "Count:", count, "Avg:", sum/count}' data.csv

# JSON 日志分析
cat logs.json | jq -r 'select(.level == "ERROR") | .type' | sort | uniq -c | sort -rn

# 按时间统计
cat data.csv | awk -F',' '{print $1}' | cut -d' ' -f1 | sort | uniq -c
```

### 4. 报告模板

```markdown
# [报告标题]

生成时间：YYYY-MM-DD HH:mm
数据范围：[起始时间] - [结束时间]

## 概览
- 总量：X
- 增长率：+Y%
- 关键指标：Z

## 趋势分析
[趋势描述]

## 分布分析
### 按类型
| 类型 | 数量 | 占比 |
|------|------|------|
| A | 100 | 50% |
| B | 80 | 40% |
| C | 20 | 10% |

### 按时间
[时间趋势]

## Top 排名
1. 项目 A - 100
2. 项目 B - 80
3. 项目 C - 60

## 洞察与建议
1. [洞察 1]
2. [洞察 2]
3. [建议]
```

### 5. 效果展示

```
数据报告生成完成！

报告信息：
- 标题：Q1 销售数据报告
- 数据源：sales-2026-Q1.csv
- 记录数：1,234 条
- 分析维度：4 个

概览：
- 总销售额：¥1,234,567
- 环比增长：+23.5%
- 同比增长：+45.2%

Top 10 产品：
1. 产品 A - ¥234,567 (19.0%)
2. 产品 B - ¥198,765 (16.1%)
3. 产品 C - ¥156,789 (12.7%)
...

区域分布：
- 华东：35%
- 华南：28%
- 华北：22%
- 其他：15%

报告已保存：
- Markdown：~/reports/sales-Q1.md
- 飞书文档：https://feishu.cn/docx/xxx
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| jq | JSON 处理 | `brew install jq` |
| feishu-doc | 可选，飞书输出 | 技能安装 |

## 相关资源

- OpenClaw 工具：exec、read、write
- OpenClaw 技能：feishu-doc
- OpenClaw 技能：gemini（分析解读）
