# WhatsApp 消息发送

## 真实来源

- **工具**：message（channel=whatsapp）
- **API**：WhatsApp Business API
- **配置**：`channels.whatsapp` 配置项

---

## 干什么
通过 OpenClaw 发送 WhatsApp 消息，支持文本、图片、文件等消息类型。

## 怎么干

### 1. 准备工作

1. 创建 WhatsApp Business 账号
2. 配置 WhatsApp Business API
3. 配置 OpenClaw：`channels.whatsapp` 配置项

### 2. 执行步骤

**方式一：发送文本消息**

```json
{
  "action": "send",
  "channel": "whatsapp",
  "target": "+14155551212",
  "message": "Hello from OpenClaw!"
}
```

**方式二：发送带格式的消息**

```
发送 WhatsApp 消息：

接收人：+14155551212
内容：
*加粗文本*
_斜体文本_
~删除线~
```代码```

支持 Markdown 格式
```

**方式三：发送图片**

```json
{
  "action": "send",
  "channel": "whatsapp",
  "target": "+14155551212",
  "message": "看看这张图片",
  "media": "file:///tmp/image.jpg"
}
```

**方式四：发送文件**

```json
{
  "action": "send",
  "channel": "whatsapp",
  "target": "+14155551212",
  "message": "报告附件",
  "media": "file:///tmp/report.pdf"
}
```

**方式五：发送位置**

```
发送位置信息：

接收人：+14155551212
位置：
- 名称：公司总部
- 地址：北京市朝阳区xxx
- 经纬度：39.9042, 116.4074
```

### 3. 消息格式

WhatsApp 支持 Markdown 格式：

| 格式 | 写法 |
|------|------|
| 加粗 | `*文本*` |
| 斜体 | `_文本_` |
| 删除线 | `~文本~` |
| 代码 | ``` `代码` ``` |

### 4. 效果展示

```
WhatsApp 消息发送完成！

消息信息：
- 渠道：whatsapp
- 目标：+14155551212
- 类型：文本
- 时间：2026-03-25 15:30:00

消息内容：
Hello from OpenClaw!

状态：已发送 ✅
消息 ID：wamid.xxx

发送图片：
- 文件：image.jpg
- 大小：1.2 MB
- 状态：已发送 ✅
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| WhatsApp Business 账号 | 企业账号 | [WhatsApp Business](https://www.whatsapp.com/business) |
| WhatsApp Business API | API 访问 | Meta 开发者平台 |

## 相关资源

- [WhatsApp Business API](https://developers.facebook.com/docs/whatsapp)
- [WhatsApp 格式指南](https://faq.whatsapp.com/539178204879377)
- OpenClaw 工具：message（channel=whatsapp）
