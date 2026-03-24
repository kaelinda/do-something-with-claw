# Telegram 机器人集成

## 干什么
使用 OpenClaw 创建 Telegram 机器人，实现自动回复、消息推送、群组管理等功能。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要 Telegram Bot Token
- message 工具支持 Telegram 渠道

### 2. 执行步骤

#### 步骤 1：创建 Telegram 机器人
1. 在 Telegram 中搜索 @BotFather
2. 发送 `/newbot` 命令
3. 按提示设置机器人名称
4. 保存返回的 API Token

#### 步骤 2：配置 OpenClaw
```yaml
# config.yaml
telegram:
  bot_token: "your-bot-token"
  webhook_url: "https://your-domain.com/webhook"  # 可选
```

#### 步骤 3：发送消息
```javascript
// 使用 message 工具发送 Telegram 消息
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  message: "你好，这是来自 OpenClaw 的消息！"
});
```

### 3. 效果展示

**对话示例：**
```
用户：/start
Bot：
欢迎使用 OpenClaw Bot！🤖

可用命令：
/help - 显示帮助
/weather <城市> - 查询天气
/translate <文本> - 翻译文本
/summary <链接> - 总结网页内容

用户：/weather 北京
Bot：
🌤️ 北京天气
温度：22°C
天气：晴
湿度：45%
```

## 常用功能

### 1. 发送文本消息
```javascript
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  message: "这是一条测试消息"
});
```

### 2. 发送图片
```javascript
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  media: "/path/to/image.jpg",
  caption: "图片说明"
});
```

### 3. 发送文件
```javascript
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  media: "/path/to/document.pdf",
  filename: "report.pdf"
});
```

### 4. 回复消息
```javascript
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  message: "这是回复内容",
  replyTo: "original_message_id"
});
```

## 高级用法

### 1. 内联键盘
```javascript
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  message: "请选择：",
  // 通过 Telegram API 发送内联按钮
});
```

### 2. Markdown 格式
```javascript
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  message: `
*标题*
_斜体_
\`代码\`
[链接](https://example.com)
`
});
```

### 3. 群组消息
```javascript
// 发送到群组
await message({
  action: "send",
  channel: "telegram",
  target: "group_id",  // 或 @group_username
  message: "群组公告"
});
```

### 4. 投票
```javascript
await message({
  action: "send",
  channel: "telegram",
  target: "chat_id",
  pollQuestion: "你最喜欢哪个编程语言？",
  pollOptions: ["Python", "JavaScript", "Rust", "Go"],
  pollMulti: false  // 单选
});
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Telegram Bot Token | 机器人令牌 | @BotFather |
| Chat ID | 目标聊天 ID | 可通过 @userinfobot 获取 |

## 常用命令

| BotFather 命令 | 说明 |
|----------------|------|
| `/newbot` | 创建新机器人 |
| `/mybots` | 管理我的机器人 |
| `/setdescription` | 设置描述 |
| `/setabouttext` | 设置简介 |
| `/setuserpic` | 设置头像 |
| `/setcommands` | 设置命令列表 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [Telegram Bot API 文档](https://core.telegram.org/bots/api)
- [BotFather 指南](https://core.telegram.org/bots#6-botfather)
- [Telegram Bot 最佳实践](https://core.telegram.org/bots/features)
