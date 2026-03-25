# Microsoft Teams 消息发送

## 真实来源

- **工具**：exec（调用 curl 发送 Webhook）
- **协议**：Microsoft Teams Incoming Webhook
- **官方文档**：https://learn.microsoft.com/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook

---

## 干什么
通过 Microsoft Teams Incoming Webhook，让 OpenClaw 自动发送消息到 Teams 频道。

## 怎么干

### 1. 准备工作

**创建 Incoming Webhook：**

1. 打开 Teams 频道 → 点击 "..." → 连接器
2. 搜索 "Incoming Webhook" → 配置
3. 输入名称和头像 → 创建
4. 复制生成的 Webhook URL

### 2. 执行步骤

**方式一：发送简单消息**

```bash
# 使用 exec 工具发送消息
curl -H "Content-Type: application/json" \
  -d '{"text": "🚀 新版本已发布！"}' \
  "https://outlook.office.com/webhook/xxx"
```

**方式二：发送自适应卡片**

```bash
# 发送富文本卡片
curl -H "Content-Type: application/json" \
  -d '{
    "type": "message",
    "attachments": [{
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "body": [{
          "type": "TextBlock",
          "text": "构建完成通知",
          "size": "large",
          "weight": "bolder"
        }, {
          "type": "TextBlock",
          "text": "项目 **main** 分支构建成功",
          "wrap": true
        }],
        "actions": [{
          "type": "Action.OpenUrl",
          "title": "查看详情",
          "url": "https://ci.example.com/build/123"
        }]
      }
    }]
  }' \
  "https://outlook.office.com/webhook/xxx"
```

**方式三：OpenClaw 指令**

```
发送消息到 Teams 频道：今天的会议改到下午3点
```

**OpenClaw 会执行：**

```bash
openclaw exec -- curl -X POST \
  -H "Content-Type: application/json" \
  -d '{"text": "今天的会议改到下午3点"}' \
  "$TEAMS_WEBHOOK_URL"
```

### 3. 效果展示

```
✅ 消息已发送到 Teams 频道
- 频道：#general
- 时间：2024-01-15 10:30:00
- 内容：今天的会议改到下午3点
```

## 自适应卡片模板

### 构建通知卡片

```json
{
  "type": "message",
  "attachments": [{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
      "type": "AdaptiveCard",
      "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
      "version": "1.4",
      "body": [{
        "type": "TextBlock",
        "text": "🔧 构建状态",
        "size": "Medium",
        "weight": "Bolder"
      }, {
        "type": "FactSet",
        "facts": [
          { "title": "项目", "value": "my-project" },
          { "title": "分支", "value": "main" },
          { "title": "状态", "value": "✅ 成功" },
          { "title": "耗时", "value": "2m 30s" }
        ]
      }],
      "actions": [{
        "type": "Action.OpenUrl",
        "title": "查看构建日志",
        "url": "https://ci.example.com/build/123"
      }]
    }
  }]
}
```

### 告警卡片

```json
{
  "type": "message",
  "attachments": [{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
      "type": "AdaptiveCard",
      "body": [{
        "type": "TextBlock",
        "text": "🚨 系统告警",
        "size": "Large",
        "weight": "Bolder",
        "color": "Attention"
      }, {
        "type": "TextBlock",
        "text": "CPU 使用率超过 90%",
        "wrap": true
      }, {
        "type": "FactSet",
        "facts": [
          { "title": "服务器", "value": "prod-web-01" },
          { "title": "当前值", "value": "92%" },
          { "title": "阈值", "value": "80%" },
          { "title": "持续时间", "value": "8 分钟" }
        ]
      }],
      "actions": [{
        "type": "Action.OpenUrl",
        "title": "查看监控面板",
        "url": "https://monitor.example.com"
      }]
    }
  }]
}
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Teams Webhook URL | 频道 Webhook | Teams 频道设置 |
| curl | HTTP 客户端 | 系统自带 |

## 环境变量配置

```bash
# 在 ~/.openclaw/openclaw.json 中配置
{
  "env": {
    "TEAMS_WEBHOOK_URL": "https://outlook.office.com/webhook/xxx"
  }
}
```

## 相关资源

- [Teams Webhook 官方文档](https://learn.microsoft.com/microsoftteams/platform/webhooks-and-connectors/how-to/add-incoming-webhook)
- [自适应卡片设计器](https://adaptivecards.io/designer/)
- [企业微信操作](wechat-work-integration.md)
