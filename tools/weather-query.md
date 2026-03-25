# 天气查询

## 真实来源

- **技能**：weather
- **数据源**：wttr.in / Open-Meteo
- **API Key**：无需

---

## 干什么
查询任意城市的当前天气和天气预报，无需 API Key。

## 怎么干

### 1. 准备工作

- OpenClaw 版本：>= 1.0.0
- curl 命令（系统自带）

### 2. 执行步骤

**方式一：当前天气**

```bash
# 简洁格式
curl "wttr.in/Shanghai?format=3"
# 输出：Shanghai: ☀️ +25°C

# 详细当前天气
curl "wttr.in/Shanghai?0"
```

**方式二：天气预报**

```bash
# 3 天预报
curl "wttr.in/Shanghai"

# 明天天气
curl "wttr.in/Shanghai?1"

# 后天天气
curl "wttr.in/Shanghai?2"
```

**方式三：特定信息**

```bash
# 自定义格式
curl "wttr.in/Shanghai?format=%l:+%c+%t+(feels+like+%f),+%w+wind,+%h+humidity"

# 只看温度
curl "wttr.in/Shanghai?format=%t"

# 是否会下雨
curl "wttr.in/Shanghai?format=%p"
```

**方式四：JSON 输出**

```bash
curl "wttr.in/Shanghai?format=j1"
```

### 3. 格式代码

| 代码 | 说明 |
|------|------|
| `%c` | 天气图标 |
| `%t` | 温度 |
| `%f` | 体感温度 |
| `%w` | 风速 |
| `%h` | 湿度 |
| `%p` | 降水概率 |
| `%l` | 位置 |

### 4. 常用查询模板

```bash
# 完整天气摘要
curl -s "wttr.in/Shanghai?format=%l:+%c+%t+(feels+like+%f),+%w+wind,+%h+humidity"

# 是否会下雨
curl -s "wttr.in/Shanghai?format=%l:+%c+%p"

# 周末预报
curl "wttr.in/Shanghai?format=v2"
```

### 5. 效果展示

```
天气查询完成！

当前天气：
- 位置：上海
- 天气：☀️ 晴
- 温度：25°C（体感 27°C）
- 风速：12 km/h
- 湿度：65%

3 天预报：
今天：☀️ 晴，18°C - 28°C
明天：⛅ 多云，17°C - 26°C
后天：🌧️ 小雨，15°C - 23°C

降水概率：
- 今天：5%
- 明天：20%
- 后天：80%

建议：后天记得带伞！
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| curl | HTTP 客户端 | 系统自带 |

## 支持的城市

- 全球大多数城市
- 支持机场代码：`curl wttr.in/PVG`（浦东机场）
- 支持地区：`curl wttr.in/California`

## 相关资源

- [wttr.in 帮助](https://wttr.in/:help)
- OpenClaw 技能：weather
