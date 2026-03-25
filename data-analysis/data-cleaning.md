# 数据清洗

## 真实来源

- **工具**：jq（JSON 处理）
- **工具**：OpenClaw exec + sed/awk
- **语言**：Python pandas、JavaScript

---

## 干什么
让 OpenClaw 自动清洗和处理数据，包括缺失值处理、异常值检测、格式标准化、数据去重等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 数据格式：CSV、JSON、Excel
- 工具：jq、sed、awk（系统内置）

### 2. 执行步骤

**方式一：使用 jq 处理 JSON 数据**

```bash
# 解析 JSON
cat data.json | jq '.'

# 提取特定字段
cat data.json | jq '.[] | {name: .name, age: .age}'

# 过滤数据
cat data.json | jq '.[] | select(.age > 18)'

# 去重
cat data.json | jq 'unique_by(.id)'

# 排序
cat data.json | jq 'sort_by(.age)'
```

**方式二：使用 sed/awk 处理文本**

```bash
# 替换文本
sed 's/old/new/g' file.txt

# 提取列
awk -F, '{print $1, $2}' file.csv

# 过滤行
awk '$3 > 100' file.csv

# 格式化输出
awk '{printf "%-10s %s\n", $1, $2}' file.txt
```

**方式三：使用 Python 脚本**

```python
import pandas as pd

# 读取数据
df = pd.read_csv('data.csv')

# 处理缺失值
df['age'].fillna(df['age'].mean(), inplace=True)
df['city'].fillna('未知', inplace=True)

# 检测异常值
q1 = df['income'].quantile(0.25)
q3 = df['income'].quantile(0.75)
iqr = q3 - q1
df = df[(df['income'] >= q1 - 1.5*iqr) & (df['income'] <= q3 + 1.5*iqr)]

# 去重
df.drop_duplicates(subset=['id'], keep='last', inplace=True)

# 格式标准化
df['date'] = pd.to_datetime(df['date']).dt.strftime('%Y-%m-%d')

# 保存
df.to_csv('cleaned_data.csv', index=False)
```

### 3. 效果展示

**清洗报告：**
```
📊 数据清洗报告

原始数据：
- 记录数：10,000 条
- 字段数：15 个
- 文件大小：2.3 MB

问题统计：
- 缺失值：245 个（占 0.16%）
- 异常值：38 个（占 0.38%）
- 重复记录：127 条
- 格式错误：89 个

处理结果：
✅ 缺失值填充：245 个已处理
✅ 异常值标记：38 个已标记
✅ 去重完成：删除 127 条重复
✅ 格式标准化：89 个已修正

清洗后数据：
- 记录数：9,873 条
- 数据完整率：99.7%
- 格式正确率：100%
```

## 常用数据清洗操作

### 1. 缺失值处理

```bash
# 使用 awk 填充缺失值
awk -F, '{
    if ($2 == "") $2 = "0"
    print $0
}' OFS=, file.csv

# 使用 jq 处理 JSON 缺失值
cat data.json | jq '.[] | .age //= 0'
```

### 2. 数据去重

```bash
# 使用 sort + uniq 去重
sort -u file.txt > unique.txt

# 使用 awk 按列去重
awk -F, '!seen[$1]++' file.csv

# 使用 jq 按 ID 去重
cat data.json | jq 'unique_by(.id)'
```

### 3. 格式标准化

```bash
# 统一日期格式
sed -E 's/([0-9]{4})\/([0-9]{2})\/([0-9]{2})/\1-\2-\3/g' file.txt

# 统一电话格式
sed -E 's/([0-9]{3})([0-9]{4})([0-9]{4})/\1-\2-\3/g' file.txt

# 使用 jq 标准化 JSON
cat data.json | jq 'map(.date = (.date | strptime("%Y/%m/%d") | strftime("%Y-%m-%d")))'
```

### 4. 异常值检测

```bash
# 使用 awk 检测数值异常
awk -F, '$3 < 0 || $3 > 100000 {print "异常行: " NR ", 值: " $3}' file.csv

# 使用 jq 检测 JSON 异常
cat data.json | jq '.[] | select(.age < 0 or .age > 150)'
```

## 数据验证

```bash
# 验证 CSV 格式
awk -F, 'NF != 5 {print "列数错误: " NR}' file.csv

# 验证数值类型
awk -F, '$2 !~ /^[0-9]+$/ {print "非数值: " NR}' file.csv

# 验证日期格式
awk -F, '$3 !~ /^[0-9]{4}-[0-9]{2}-[0-9]{2}$/ {print "日期格式错误: " NR}' file.csv
```

## 数据转换

### CSV 转 JSON

```bash
# 使用 jq 处理 CSV（需要 csvtojson 或类似工具）
# 或使用 Python
python3 -c "
import csv, json
with open('data.csv') as f:
    reader = csv.DictReader(f)
    print(json.dumps(list(reader)))
"
```

### JSON 转 CSV

```bash
# 使用 jq 转 CSV
cat data.json | jq -r '.[] | [.name, .age, .city] | @csv'
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| jq | JSON 处理 | `brew install jq` |
| sed/awk | 文本处理 | 系统内置 |
| Python pandas | 可选 | `pip install pandas` |

## 来源

- **工具**：jq（https://stedolan.github.io/jq/）
- **工具**：sed/awk（系统内置）
- **语言**：Python pandas（https://pandas.pydata.org/）

## 相关资源

- [jq 手册](https://stedolan.github.io/jq/manual/)
- [AWK 教程](https://www.gnu.org/software/gawk/manual/)
- [pandas 文档](https://pandas.pydata.org/docs/)
- [日志分析](data-analysis/log-analysis.md)
