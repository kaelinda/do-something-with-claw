# Teams 智能问答机器人

## 真实来源

- **工具**：exec（调用 curl 发送 Webhook）+ OpenClaw 对话能力
- **协议**：Microsoft Teams Incoming Webhook + Bot Framework
- **官方文档**：https://learn.microsoft.com/microsoftteams/platform/bots/how-to/

---

## 干什么
结合 OpenClaw 的 AI 能力和 Teams Webhook，实现智能问答机器人，自动回答员工的常见问题。

## 怎么干

### 1. 准备工作

**方案选择：**

| 方案 | 复杂度 | 功能 |
|------|--------|------|
| Incoming Webhook | 低 | 单向通知 |
| Bot Framework | 中 | 双向对话 |
| Power Automate | 低 | 自动化流程 |

### 2. 执行步骤

**方式一：基于知识库的自动回复**

```javascript
// 定义 FAQ 知识库
const faqKnowledgeBase = {
  "年假": {
    answer: "📅 年假计算规则：\n1. 入职满1年：5天\n2. 入职满3年：10天\n3. 入职满5年：15天",
    link: "https://wiki.company.com/hr/leave"
  },
  "VPN": {
    answer: "🔐 VPN 连接步骤：\n1. 下载 AnyConnect 客户端\n2. 服务器地址：vpn.company.com\n3. 使用域账号登录",
    link: "https://wiki.company.com/it/vpn"
  },
  "报销": {
    answer: "💰 报销流程：\n1. 登录 OA 系统\n2. 提交报销单\n3. 上传发票\n4. 等待审批",
    link: "https://oa.company.com/expense"
  }
};

// 匹配问题并返回答案
function matchFAQ(question) {
  for (const [keyword, data] of Object.entries(faqKnowledgeBase)) {
    if (question.includes(keyword)) {
      return data;
    }
  }
  return null;
}
```

**方式二：OpenClaw 智能回答**

```
用户问：年假怎么计算？

OpenClaw 分析问题 → 查询知识库 → 生成回答
```

**发送回答到 Teams：**

```bash
curl -H "Content-Type: application/json" \
  -d '{
    "type": "message",
    "attachments": [{
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "body": [{
          "type": "TextBlock",
          "text": "📅 年假计算规则",
          "size": "Medium",
          "weight": "Bolder"
        }, {
          "type": "TextBlock",
          "text": "1. 入职满1年：5天\n2. 入职满3年：10天\n3. 入职满5年：15天",
          "wrap": true
        }],
        "actions": [{
          "type": "Action.OpenUrl",
          "title": "查看详细说明",
          "url": "https://wiki.company.com/hr/leave"
        }]
      }
    }]
  }' \
  "$TEAMS_WEBHOOK_URL"
```

### 3. 效果展示

```
员工：年假怎么计算？

机器人：
📅 年假计算规则

1. 入职满1年：5天
2. 入职满3年：10天
3. 入职满5年：15天

详细说明请查看：[员工手册链接]
```

## 常见问题类型

| 问题类型 | 示例 |
|----------|------|
| 人力资源 | 年假怎么算？入职流程？ |
| IT 支持 | VPN 怎么连？密码怎么改？ |
| 行政服务 | 会议室怎么订？报销流程？ |
| 产品帮助 | 功能怎么用？常见问题？ |

## 知识库管理

### 使用飞书多维表格

```markdown
| 关键词 | 答案 | 链接 | 更新时间 |
|--------|------|------|----------|
| 年假 | 年假计算规则... | https://... | 2024-01-15 |
| VPN | VPN 连接步骤... | https://... | 2024-01-10 |
```

### 使用 Obsidian

```markdown
# FAQ 知识库

## 年假
年假计算规则：
- 入职满1年：5天
- 入职满3年：10天
- 入职满5年：15天

详见：[[员工手册#年假制度]]

## VPN
VPN 连接步骤：
1. 下载 AnyConnect
2. 输入服务器地址
3. 域账号登录
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Teams Webhook | 频道 Webhook | Teams 频道设置 |
| 知识库 | FAQ 文档 | 自行整理 |

## 相关资源

- [Teams 消息发送](teams-integration.md)
- [Teams Bot Framework](https://learn.microsoft.com/microsoftteams/platform/bots/)
- [飞书多维表格技能](https://clawhub.com/skills/feishu-bitable)
