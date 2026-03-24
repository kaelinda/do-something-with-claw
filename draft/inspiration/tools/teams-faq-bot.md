# Teams 智能问答机器人

## 干什么
在 Teams 中创建智能问答机器人，自动回答员工的常见问题。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要配置：Teams 频道插件
- 需要准备：FAQ 知识库

### 2. 执行步骤

**配置 Teams 频道自动回复：**

```yaml
# ~/.openclaw/config.yaml
channels:
  msteams:
    - name: hr-bot
      tenantId: "your-tenant-id"
      autoReply: true
      knowledgeBase: "./hr-faq.md"
```

**常见问题类型：**

| 问题类型 | 示例 |
|----------|------|
| 人力资源 | 年假怎么算？入职流程？ |
| IT 支持 | VPN 怎么连？密码怎么改？ |
| 行政服务 | 会议室怎么订？报销流程？ |
| 产品帮助 | 功能怎么用？常见问题？ |

### 3. 效果展示

```
员工：年假怎么计算？

机器人：
📅 年假计算规则：

1. 入职满1年：5天
2. 入职满3年：10天
3. 入职满5年：15天

详细说明请查看：[员工手册链接]
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Teams 插件 | Teams 频道支持 | 内置插件 |
| 知识库 | FAQ 文档 | 自行整理 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 企业应用示例
- 日期：2024

## 相关资源

- [Teams 消息发送](teams-integration.md)
- [OpenClaw 自动回复配置](https://docs.openclaw.ai/channels/auto-reply)
