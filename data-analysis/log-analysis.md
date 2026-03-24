# 日志分析

## 真实来源

- **工具**：OpenClaw 内置 exec 工具
- **技术**：jq、grep、awk、sed
- **格式**：JSON/文本日志

---

## 干什么
自动化分析系统日志、应用日志，提取关键信息，发现异常模式。

## 怎么干

### 1. 准备工作
- 日志文件路径
- 日志格式（JSON/文本）
- 分析目标

### 2. 执行步骤

**方式一：错误日志提取**

```
分析应用日志：
- 文件：/var/log/app.log
- 筛选：ERROR 级别
- 时间范围：最近 24 小时
- 输出：错误类型统计
```

**方式二：访问日志分析**

```
分析 Nginx 访问日志：
- 文件：/var/log/nginx/access.log
- 提取：请求路径、响应码、响应时间
- 统计：Top 10 访问路径
- 异常：响应时间 > 1s 的请求
```

**方式三：异常模式检测**

```
检测日志中的异常模式：
- 文件：应用日志
- 模式：连续错误、异常堆栈、超时
- 频率：按小时统计
```

**方式四：生成报告**

```
生成日志分析报告：
- 时间范围：最近 7 天
- 内容：错误趋势、Top 错误、建议
- 格式：Markdown
```

### 3. 常用命令

```bash
# JSON 日志分析（使用 jq）
# 统计错误类型
cat app.log | jq 'select(.level == "ERROR") | .type' | sort | uniq -c | sort -rn

# 按时间统计
cat app.log | jq -r '.timestamp[:10]' | sort | uniq -c

# 提取特定字段
cat app.log | jq 'select(.level == "ERROR") | {time: .timestamp, msg: .message, type: .type}'

# 文本日志分析
# 统计错误数量
grep -c "ERROR" app.log

# 提取错误行及上下文
grep -B 2 -A 5 "ERROR" app.log

# 按小时统计
awk '{print $1":"$2}' app.log | cut -d: -f1-2 | sort | uniq -c

# Nginx 日志分析
# Top 10 访问路径
awk '{print $7}' access.log | sort | uniq -c | sort -rn | head -10

# 响应码统计
awk '{print $9}' access.log | sort | uniq -c | sort -rn

# 响应时间 Top 10
awk '{print $NF, $7}' access.log | sort -rn | head -10
```

### 4. 效果展示

```
日志分析报告 | 2026-03-25

## 错误统计（最近 24 小时）
- ERROR: 234 次
- WARN: 1,567 次
- INFO: 45,678 次

## Top 5 错误类型
1. ConnectionTimeout: 89 次
2. DatabaseError: 67 次
3. AuthFailed: 45 次
4. ValidationError: 23 次
5. RateLimitExceeded: 10 次

## 异常模式检测
- ⚠️ 03:00-04:00 连续错误高峰（23 次/分钟）
- ⚠️ API /v1/notify 响应时间异常（平均 2.3s）

## 建议
1. 检查数据库连接池配置
2. 优化 /v1/notify 接口性能
3. 增加重试机制处理超时
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| jq | JSON 处理 | `brew install jq` |
| 日志文件 | 分析目标 | 应用生成 |

## 相关资源

- [jq 手册](https://stedolan.github.io/jq/manual/)
- OpenClaw 工具：exec
