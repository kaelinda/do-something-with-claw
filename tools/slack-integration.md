# Slack 消息发送

## 真实来源

- **技能**：slack
- **配置**：`channels.slack` 配置项
- **权限**：chat:write, files:write

---

## 干什么
让 OpenClaw 自动发送 Slack 消息，支持频道消息、私信、反应、置顶等操作。

## 怎么干

### 1. 准备工作

- OpenClaw 版本：>= 1.0.0
- Slack Bot Token 或 Incoming Webhook
- 权限：chat:write, files:write

### 2. 执行步骤

**方式一：发送频道消息**

```json
{
  "action": "sendMessage",
  "to": "channel:C123",
  "content": "🚀 新版本已发布！"
}
```

**方式二：发送私信**

```json
{
  "action": "sendMessage",
  "to": "user:U123",
  "content": "你的 PR #123 已审核通过"
}
```

**方式三：添加反应**

```json
{
  "action": "react",
  "channelId": "C123",
  "messageId": "1712023032.1234",
  "emoji": "✅"
}
```

**方式四：读取消息**

```json
{
  "action": "readMessages",
  "channelId": "C123",
  "limit": 20
}
```

**方式五：置顶消息**

```json
{
  "action": "pinMessage",
  "channelId": "C123",
  "messageId": "1712023032.1234"
}
```

**方式六：发送带附件**

```json
{
  "action": "send",
  "channel": "slack",
  "to": "channel:C123",
  "message": "月度报告",
  "media": "file:///tmp/report.pdf"
}
```

### 3. 可用操作

| Action | 说明 |
|--------|------|
| `sendMessage` | 发送消息 |
| `editMessage` | 编辑消息 |
| `deleteMessage` | 删除消息 |
| `readMessages` | 读取消息 |
| `react` | 添加反应 |
| `reactions` | 列出反应 |
| `pinMessage` | 置顶消息 |
| `unpinMessage` | 取消置顶 |
| `listPins` | 列出置顶 |
| `memberInfo` | 成员信息 |
| `emojiList` | 表情列表 |

### 4. 效果展示

```
Slack 操作完成！

消息发送：
- 频道：#general（128 成员）
- 内容：🚀 新版本已发布！
- 时间戳：1711287600.123456
- 状态：已发送 ✅

反应添加：
- 消息：1712023032.1234
- 表情：✅
- 状态：已添加

置顶消息：
- 频道：#announcements
- 消息：版本发布通知
- 状态：已置顶
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Slack Bot Token | xoxb-xxx | Slack App 设置 |
| 或 Webhook URL | Incoming Webhook | 频道设置 |

## 相关资源

- [Slack API 文档](https://api.slack.com)
- OpenClaw 技能：slack
