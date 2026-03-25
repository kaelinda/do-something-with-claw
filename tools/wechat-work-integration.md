# 企业微信消息发送

## 真实来源

- **工具**：message（channel=wechat-work）
- **API**：企业微信 API
- **配置**：`channels.wechat-work` 配置项

---

## 干什么
通过 OpenClaw 发送企业微信消息，包括文本、卡片、文件，支持私聊和群聊。

## 怎么干

### 1. 准备工作

1. 创建企业微信应用（https://developer.work.weixin.qq.com）
2. 配置应用权限（消息发送权限）
3. 配置 OpenClaw：`channels.wechat-work.corpId` + `channels.wechat-work.agentId` + `channels.wechat-work.secret`

### 2. 执行步骤

**方式一：发送文本消息**

```json
{
  "action": "send",
  "channel": "wechat-work",
  "target": "user:zhangsan",
  "message": "你好，这是一条来自 OpenClaw 的消息！"
}
```

**方式二：发送群消息**

```json
{
  "action": "send",
  "channel": "wechat-work",
  "target": "chat:xxx",
  "message": "📋 今日站会提醒\n\n时间：10:00\n地点：会议室 A"
}
```

**方式三：发送 Markdown 消息**

```
发送企业微信 Markdown 消息：

接收人：开发群
内容：
## 🔔 系统部署完成

- **环境**：生产环境
- **版本**：v1.2.3
- **时间**：2026-03-25 15:30
- **状态**：成功 ✅

[查看详情](https://example.com/deploy/123)
```

**方式四：发送卡片消息**

```
发送企业微信卡片消息：

接收人：产品群
卡片类型：通知卡片
标题：🔔 系统部署完成
内容：
- 环境：生产环境
- 版本：v1.2.3
- 时间：2026-03-25 15:30
- 状态：成功

按钮：
- [查看详情] -> https://example.com/deploy/123
- [回滚] -> https://example.com/rollback
```

**方式五：发送文件**

```json
{
  "action": "send",
  "channel": "wechat-work",
  "target": "chat:xxx",
  "message": "报告附件",
  "media": "file:///tmp/report.pdf"
}
```

**方式六：群机器人 Webhook**

```
通过群机器人发送消息：

Webhook URL：https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxx
消息内容：
{
  "msgtype": "markdown",
  "markdown": {
    "content": "## 部署通知\n> 环境：生产环境\n> 状态：成功 ✅"
  }
}
```

### 3. 消息类型

| 类型 | 说明 |
|------|------|
| text | 纯文本 |
| markdown | Markdown 格式 |
| image | 图片 |
| news | 图文消息 |
| file | 文件 |
| template_card | 模板卡片 |

### 4. 效果展示

```
企业微信消息发送完成！

消息信息：
- 渠道：wechat-work
- 目标：chat:xxx（产品群）
- 类型：Markdown
- 时间：2026-03-25 15:30:00

消息内容：
📋 今日站会提醒

时间：10:00
地点：会议室 A
议程：
1. 昨日进展
2. 今日计划
3. 阻塞问题

状态：已送达 ✅

群机器人消息：
- Webhook：已调用
- 响应：success
- 消息 ID：msg_xxx
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 企业微信 | 企业账号 | 企业注册 |
| 企业微信应用 | CorpID + AgentID + Secret | [企业微信管理后台](https://developer.work.weixin.qq.com) |
| 权限配置 | 消息发送权限 | 应用后台配置 |

## 群机器人配置

1. 进入企业微信群 → 群设置 → 群机器人 → 添加机器人
2. 复制 Webhook URL
3. 使用 Webhook 发送消息

```bash
curl -X POST "https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=xxx" \
  -H "Content-Type: application/json" \
  -d '{
    "msgtype": "markdown",
    "markdown": {
      "content": "## 通知\n> 这是一条测试消息"
    }
  }'
```

## 相关资源

- [企业微信 API 文档](https://developer.work.weixin.qq.com/document)
- [群机器人配置](https://developer.work.weixin.qq.com/document/path/91770)
- OpenClaw 工具：message（channel=wechat-work）
