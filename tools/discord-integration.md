# Discord 机器人集成

## 真实来源

- **技能**：discord
- **工具**：message（channel=discord）
- **配置**：`channels.discord.token`

---

## 干什么
使用 OpenClaw 通过 message 工具操作 Discord，实现消息发送、反应、置顶、投票等功能。

## 怎么干

### 1. 准备工作

1. 访问 https://discord.com/developers/applications
2. 创建应用 → 添加 Bot → 复制 Token
3. 在 OAuth2 > URL Generator 生成邀请链接
4. 配置 OpenClaw：`channels.discord.token`

### 2. 执行步骤

**方式一：发送消息**

```json
{
  "action": "send",
  "channel": "discord",
  "to": "channel:123",
  "message": "Hello from OpenClaw!"
}
```

**方式二：静默发送**

```json
{
  "action": "send",
  "channel": "discord",
  "to": "channel:123",
  "message": "后台通知",
  "silent": true
}
```

**方式三：发送带附件**

```json
{
  "action": "send",
  "channel": "discord",
  "to": "channel:123",
  "message": "报告附件",
  "media": "file:///tmp/report.pdf"
}
```

**方式四：添加反应**

```json
{
  "action": "react",
  "channel": "discord",
  "channelId": "123",
  "messageId": "456",
  "emoji": "✅"
}
```

**方式五：创建投票**

```json
{
  "action": "poll",
  "channel": "discord",
  "to": "channel:123",
  "pollQuestion": "午餐吃什么？",
  "pollOption": ["披萨", "寿司", "沙拉"],
  "pollMulti": false,
  "pollDurationHours": 24
}
```

**方式六：创建线程**

```json
{
  "action": "thread-create",
  "channel": "discord",
  "channelId": "123",
  "messageId": "456",
  "threadName": "Bug 讨论"
}
```

**方式七：置顶消息**

```json
{
  "action": "pin",
  "channel": "discord",
  "channelId": "123",
  "messageId": "456"
}
```

**方式八：搜索消息**

```json
{
  "action": "search",
  "channel": "discord",
  "guildId": "999",
  "query": "release notes",
  "limit": 10
}
```

### 3. 可用操作

| Action | 说明 |
|--------|------|
| `send` | 发送消息 |
| `edit` | 编辑消息 |
| `delete` | 删除消息 |
| `read` | 读取消息 |
| `react` | 添加反应 |
| `pin` | 置顶消息 |
| `unpin` | 取消置顶 |
| `poll` | 创建投票 |
| `thread-create` | 创建线程 |
| `search` | 搜索消息 |

### 4. Discord 写作风格

- 简短、口语化、低仪式感
- 避免 Markdown 表格
- 提及用户：`<@USER_ID>`

### 5. 效果展示

```
Discord 操作完成！

消息发送：
- 频道：#general
- 内容：🚀 新版本已发布！
- 状态：已发送

投票创建：
- 问题：午餐吃什么？
- 选项：披萨、寿司、沙拉
- 时长：24 小时
- 投票链接：[已创建]

线程创建：
- 频道：#bugs
- 原消息：Bug 报告 #123
- 线程名：Bug 讨论
- 状态：已创建
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Discord Bot Token | Bot 令牌 | [开发者平台](https://discord.com/developers/applications) |
| 服务器权限 | 添加 Bot 到服务器 | 服务器设置 |

## 相关资源

- [Discord 开发者文档](https://discord.com/developers/docs)
- OpenClaw 技能：discord
