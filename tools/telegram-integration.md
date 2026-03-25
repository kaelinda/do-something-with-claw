# Telegram 机器人集成

## 真实来源

- **工具**：message（channel=telegram）
- **配置**：`channels.telegram` 配置项
- **API**：Telegram Bot API

---

## 干什么
使用 OpenClaw 通过 message 工具操作 Telegram，实现消息发送、投票、文件分享等功能。

## 怎么干

### 1. 准备工作

1. 访问 https://t.me/BotFather 创建 Bot
2. 获取 Bot Token
3. 配置 OpenClaw：`channels.telegram.token`

### 2. 执行步骤

**方式一：发送消息**

```json
{
  "action": "send",
  "channel": "telegram",
  "target": "chat_id_or_username",
  "message": "Hello from OpenClaw!"
}
```

**方式二：发送带格式消息**

```json
{
  "action": "send",
  "channel": "telegram",
  "target": "chat_id",
  "message": "*加粗* _斜体_ `代码`",
  "parseMode": "Markdown"
}
```

**方式三：发送文件**

```json
{
  "action": "send",
  "channel": "telegram",
  "target": "chat_id",
  "message": "报告附件",
  "media": "file:///tmp/report.pdf"
}
```

**方式四：创建投票**

```json
{
  "action": "poll",
  "channel": "telegram",
  "target": "chat_id",
  "pollQuestion": "午餐吃什么？",
  "pollOption": ["披萨", "寿司", "沙拉"],
  "pollMulti": false
}
```

**方式五：回复消息**

```json
{
  "action": "send",
  "channel": "telegram",
  "target": "chat_id",
  "message": "回复内容",
  "replyTo": "message_id"
}
```

### 3. Telegram 格式

```markdown
*加粗文本*
_斜体文本_
`代码`
[链接](https://example.com)
```

### 4. 效果展示

```
Telegram 消息发送完成！

发送消息：
- 聊天：@mygroup
- 内容：🚀 新版本已发布！
- 时间戳：1711287600
- 消息 ID：12345

发送文件：
- 文件：report.pdf
- 大小：2.3 MB
- 状态：已发送 ✅

创建投票：
- 问题：午餐吃什么？
- 选项：披萨、寿司、沙拉
- 状态：已创建
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Telegram Bot Token | Bot 令牌 | [@BotFather](https://t.me/BotFather) |
| Chat ID | 目标聊天 | 与 Bot 对话获取 |

## 获取 Chat ID

```bash
# 方法一：使用 @userinfobot
# 发送消息给 @userinfobot，它会返回你的 Chat ID

# 方法二：使用 API
curl "https://api.telegram.org/bot<TOKEN>/getUpdates"
```

## 相关资源

- [Telegram Bot API](https://core.telegram.org/bots/api)
- [BotFather 指南](https://core.telegram.org/bots#6-botfather)
- OpenClaw 工具：message（channel=telegram）
