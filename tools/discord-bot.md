# Discord 机器人操作

## 干什么
使用 OpenClaw 操作 Discord：发送消息、创建投票、管理频道、设置状态等。

## 怎么干

### 1. 配置 Discord 频道

```yaml
# ~/.openclaw/config.yaml
channels:
  discord:
    - name: my-server
      token: "${DISCORD_BOT_TOKEN}"
      # 可选：启用高级功能
      actions:
        roles: true        # 角色管理
        moderation: true   # 消息管理
        presence: true     # 状态设置
```

### 2. 发送消息

```
用户：在 Discord 的 general 频道发一条消息：今晚 8 点有会议
```

**OpenClaw 执行：**
```json
{
  "action": "send",
  "channel": "discord",
  "to": "channel:123456789",
  "message": "📢 今晚 8 点有会议，请大家准时参加！",
  "silent": true
}
```

### 3. 创建投票

```
用户：在 Discord 创建一个投票：中午吃什么？选项：火锅、烧烤、寿司
```

**OpenClaw 执行：**
```json
{
  "action": "poll",
  "channel": "discord",
  "to": "channel:123456789",
  "pollQuestion": "中午吃什么？",
  "pollOption": ["🍲 火锅", "🍖 烧烤", "🍣 寿司"],
  "pollMulti": false,
  "pollDurationHours": 2
}
```

### 4. 发送带图消息

```
用户：把 /tmp/report.png 发到 Discord 的 dev 频道
```

**OpenClaw 执行：**
```json
{
  "action": "send",
  "channel": "discord",
  "to": "channel:987654321",
  "message": "📊 本周数据报告",
  "media": "file:///tmp/report.png"
}
```

### 5. 消息反应

```
用户：给那个消息加个 ✅ 反应
```

**OpenClaw 执行：**
```json
{
  "action": "react",
  "channel": "discord",
  "channelId": "123456789",
  "messageId": "987654321",
  "emoji": "✅"
}
```

### 6. 创建帖子

```
用户：把那个 bug 报告转成帖子讨论
```

**OpenClaw 执行：**
```json
{
  "action": "thread-create",
  "channel": "discord",
  "channelId": "123456789",
  "messageId": "987654321",
  "threadName": "🐛 Bug 修复讨论"
}
```

### 7. 设置状态

```
用户：设置 Discord 状态为：正在写代码
```

**OpenClaw 执行：**
```json
{
  "action": "set-presence",
  "channel": "discord",
  "activityType": "playing",
  "activityName": "写代码",
  "status": "online"
}
```

## 常用功能速查

| 功能 | action | 示例 |
|------|--------|------|
| 发送消息 | `send` | `"message": "hello"` |
| 发送图片 | `send` | `"media": "file:///path"` |
| 创建投票 | `poll` | `"pollQuestion": "..."` |
| 添加反应 | `react` | `"emoji": "✅"` |
| 创建帖子 | `thread-create` | `"threadName": "..."` |
| 置顶消息 | `pin` | `"messageId": "..."` |
| 搜索消息 | `search` | `"query": "关键词"` |
| 设置状态 | `set-presence` | `"activityName": "..."` |

## 提及用户

```json
{
  "action": "send",
  "channel": "discord",
  "to": "channel:123",
  "message": "<@987654321> 请查看这个 PR"
}
```

## 静默发送

```json
{
  "action": "send",
  "channel": "discord",
  "to": "channel:123",
  "message": "更新完成",
  "silent": true
}
```

> `silent: true` 不会触发用户通知，适合批量更新。

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Discord Bot Token | 机器人令牌 | Discord Developer Portal |
| 服务器权限 | 邀请 Bot 加入服务器 | Discord 服务器设置 |

## 创建 Discord Bot

1. 访问 https://discord.com/developers/applications
2. 创建 New Application
3. 进入 Bot → Add Bot
4. 复制 Token
5. OAuth2 → URL Generator → 选择 bot 权限
6. 生成的链接邀请 Bot 加入服务器

## 来源

- 贡献者：Community
- 来源：discord 技能文档
- 日期：2024

## 相关资源

- [Discord Developer Portal](https://discord.com/developers/applications)
- [Discord API 文档](https://discord.com/developers/docs/intro)
