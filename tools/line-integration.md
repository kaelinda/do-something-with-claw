# Line 消息发送

## 真实来源

- **工具**：message（channel=line）
- **API**：LINE Messaging API
- **配置**：`channels.line` 配置项

---

## 干什么
通过 OpenClaw 发送 Line 消息，支持文本、图片、卡片等消息类型。

## 怎么干

### 1. 准备工作

1. 创建 LINE Developers 账号
2. 创建 Messaging API Channel
3. 获取 Channel Access Token
4. 配置 OpenClaw：`channels.line` 配置项

### 2. 执行步骤

**方式一：发送文本消息**

```json
{
  "action": "send",
  "channel": "line",
  "target": "user:xxx",
  "message": "Hello from OpenClaw!"
}
```

**方式二：发送群消息**

```json
{
  "action": "send",
  "channel": "line",
  "target": "group:xxx",
  "message": "团队通知：今天下午3点开会"
}
```

**方式三：发送图片**

```json
{
  "action": "send",
  "channel": "line",
  "target": "user:xxx",
  "message": "看看这张图片",
  "media": "file:///tmp/image.jpg"
}
```

**方式四：发送 Flex 消息**

Line 支持 Flex Message，可以创建丰富的卡片式消息。

```
发送 Line Flex 消息：

接收人：user:xxx
类型：Flex Message
内容：
- 标题：部署通知
- 正文：生产环境部署成功
- 图片：[缩略图]
- 按钮：[查看详情]
```

### 3. 消息类型

| 类型 | 说明 |
|------|------|
| text | 文本消息 |
| image | 图片消息 |
| video | 视频消息 |
| audio | 音频消息 |
| location | 位置消息 |
| sticker | 表情贴图 |
| flex | Flex 消息（卡片） |

### 4. 效果展示

```
Line 消息发送完成！

消息信息：
- 渠道：line
- 目标：user:xxx
- 类型：文本
- 时间：2026-03-25 15:30:00

消息内容：
Hello from OpenClaw!

状态：已发送 ✅
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| LINE Developers 账号 | 开发者账号 | [LINE Developers](https://developers.line.biz) |
| Messaging API Channel | 消息通道 | LINE Developers 创建 |

## 相关资源

- [LINE Developers](https://developers.line.biz)
- [LINE Messaging API](https://developers.line.biz/en/docs/messaging-api/)
- OpenClaw 工具：message（channel=line）
