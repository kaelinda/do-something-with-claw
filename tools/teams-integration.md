# Microsoft Teams 消息发送

## 干什么
让 OpenClaw 自动发送消息到 Microsoft Teams 频道或私聊。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要配置：Microsoft Teams 频道插件
- 需要权限：Teams 租户管理员授权

### 2. 执行步骤

**配置 Teams 频道：**

```yaml
# ~/.openclaw/config.yaml
channels:
  msteams:
    - name: work-team
      tenantId: "your-tenant-id"
      clientId: "your-client-id"
      clientSecret: "${MSTEAMS_CLIENT_SECRET}"
```

**发送消息：**

```
发送消息到 Teams 的 work-team 频道：今天的会议改到下午3点
```

**OpenClaw 会执行：**

```javascript
// 自动路由到 Teams 频道
message({
  action: "send",
  channel: "msteams",
  target: "work-team",
  message: "今天的会议改到下午3点"
})
```

### 3. 效果展示

```
✅ 消息已发送到 Teams 频道
- 频道：work-team
- 时间：2024-01-15 10:30:00
- 内容：今天的会议改到下午3点
```

## 支持的功能

| 功能 | 说明 |
|------|------|
| 频道消息 | 发送到指定频道 |
| 私聊消息 | 发送给指定用户 |
| 卡片消息 | 发送自适应卡片 |
| 文件附件 | 发送文件和图片 |

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Teams 插件 | MSTeams 频道支持 | 内置插件 |
| Azure AD 应用 | Teams API 权限 | Azure Portal |
| 租户授权 | 管理员同意 | Teams 管理员 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 文档
- 日期：2024

## 相关资源

- [OpenClaw Teams 配置文档](https://docs.openclaw.ai/channels/msteams)
- [Microsoft Teams API 文档](https://docs.microsoft.com/graph/api/resources/teams-api-overview)
