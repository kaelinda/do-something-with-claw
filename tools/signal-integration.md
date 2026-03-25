# Signal 消息发送

## 眞实来源

- **工具**：message（channel=signal）
- **配置**：`channels.signal` 配置项

---

## 干什么
通过 OpenClaw 发送 Signal 消息，支持文本、图片、文件等消息类型。

## 怎么干

### 1. 准备工作

1. 安装 Signal Desktop
2. 配置 Signal CLI 或 signaling 服务
3. 配置 OpenClaw：`channels.signal` 配置项

### 2. 执行步骤

**方式一：发送文本消息**

```json
{
  "action": "send",
  "channel": "signal",
  "target": "+14155551212",
  "message": "Hello from OpenClaw!"
}
```

**方式二：发送群消息**

```json
{
  "action": "send",
  "channel": "signal",
  "target": "group:xxx",
  "message": "团队通知：今天下午3点开会"
}
```

**方式三：发送图片**

```json
{
  "action": "send",
  "channel": "signal",
  "target": "+14155551212",
  "message": "看看这张图片",
  "media": "file:///tmp/image.jpg"
}
```

**方式四：发送文件**

```json
{
  "action": "send",
  "channel": "signal",
  "target": "+14155551212",
  "message": "报告附件",
  "media": "file:///tmp/report.pdf"
}
```

### 3. Signal 特性

- 端到端加密
- 隐私保护
- 自动删除消息
- 无需绑定手机号（可选）

### 4. 效果展示

```
Signal 消息发送完成！

消息信息：
- 渠道：signal
- 目标：+14155551212
- 类型：文本
- 时间：2026-03-25 15:30:00
- 加密：端到端加密 ✅

消息内容：
Hello from OpenClaw!

状态：已发送 ✅
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Signal Desktop | 桌面客户端 | [Signal 官网](https://signal.org) |
| Signal 账号 | 注册账号 | Signal 注册 |

## 相关资源

- [Signal 官网](https://signal.org)
- [Signal CLI](https://github.com/AsamK/signal-cli)
- OpenClaw 工具：message（channel=signal）
