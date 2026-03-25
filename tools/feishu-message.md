# 飞书消息发送

## 真实来源

- **工具**：message（channel=feishu）
- **技能**：feishu-doc、feishu-chat、feishu-bitable-*
- **API**：飞书开放平台 API
- **配置**：`channels.feishu` 配置项

---

## 干什么
通过 OpenClaw 发送飞书消息，包括文本、卡片、文件，支持私聊和群聊。

## 怎么干

### 1. 准备工作

1. 创建飞书应用（https://open.feishu.cn）
2. 配置应用权限（im:message, im:message:send_as_bot）
3. 配置 OpenClaw：`channels.feishu.appId` + `channels.feishu.appSecret`

### 2. 执行步骤

**方式一：发送文本消息**

```json
{
  "action": "send",
  "channel": "feishu",
  "target": "user:ou_xxx",
  "message": "你好，这是一条来自 OpenClaw 的消息！"
}
```

**方式二：发送群消息**

```json
{
  "action": "send",
  "channel": "feishu",
  "target": "chat:oc_xxx",
  "message": "📋 今日站会提醒\n\n时间：10:00\n地点：会议室 A"
}
```

**方式三：发送富文本消息**

```
发送飞书富文本消息：

接收人：开发群
内容：
## 🔔 系统部署完成

- **环境**：生产环境
- **版本**：v1.2.3
- **时间**：2026-03-25 15:30
- **状态**：成功 ✅

[查看详情](https://example.com/deploy/123)
```

**方式四：发送文件**

```json
{
  "action": "send",
  "channel": "feishu",
  "target": "chat:oc_xxx",
  "message": "报告附件",
  "media": "file:///tmp/report.pdf"
}
```

**方式五：发送卡片消息**

飞书支持交互式卡片，可以包含按钮、表单等交互元素。

### 3. 目标格式

| 格式 | 说明 |
|------|------|
| `user:ou_xxx` | 私聊用户（open_id） |
| `user:user_id:xxx` | 私聊用户（user_id） |
| `chat:oc_xxx` | 群聊（chat_id） |

### 4. 效果展示

```
飞书消息发送完成！

消息信息：
- 渠道：feishu
- 目标：chat:oc_xxx（开发群）
- 类型：富文本
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
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 飞书企业账号 | 企业协作平台 | 企业注册 |
| 飞书应用 | App ID + Secret | [飞书开放平台](https://open.feishu.cn) |
| 权限配置 | im:message 等权限 | 应用后台配置 |

## 相关资源

- [飞书开放平台](https://open.feishu.cn)
- [飞书消息 API](https://open.feishu.cn/document/ukTMukTMukTM/uUjNz4SN2MjL1YzM)
- OpenClaw 工具：message（channel=feishu）
- OpenClaw 技能：feishu-doc、feishu-chat
