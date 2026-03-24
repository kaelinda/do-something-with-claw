# Discord 机器人集成

## 干什么
使用 OpenClaw 创建 Discord 机器人，实现自动回复、消息推送、频道管理等功能。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要 Discord Bot Token
- 需要配置 Discord Gateway 连接

### 2. 执行步骤

#### 步骤 1：创建 Discord 应用
1. 访问 https://discord.com/developers/applications
2. 点击 "New Application" 创建应用
3. 进入 Bot 页面，点击 "Add Bot"
4. 复制 Bot Token
5. 在 OAuth2 > URL Generator 中生成邀请链接

#### 步骤 2：配置 OpenClaw
```yaml
# config.yaml
discord:
  token: "your-bot-token"
  prefix: "!"
  intents:
    - messages
    - guilds
    - message_content
```

#### 步骤 3：启动机器人
```bash
openclaw discord start
```

### 3. 效果展示

**对话示例：**
```
用户：!help
Bot：
📚 可用命令：
!help - 显示帮助
!ping - 测试连接
!info - 查看信息
!translate <文本> - 翻译文本

用户：!translate Hello World
Bot：翻译结果：你好世界
```

## 常用功能

### 1. 自动回复
```javascript
// 配置自动回复规则
const replies = {
  "hello": "你好！有什么可以帮助你的？",
  "thanks": "不客气！",
  "bye": "再见！"
};
```

### 2. 定时推送
```javascript
// 定时发送消息到频道
schedule.scheduleJob("0 9 * * *", async () => {
  await discord.sendMessage(channelId, "早安！新的一天开始了 🌅");
});
```

### 3. 关键词监控
```javascript
// 监控特定关键词
discord.onMessage(async (message) => {
  if (message.content.includes("紧急")) {
    await message.reply("已收到紧急消息，立即处理！");
    // 触发通知流程
  }
});
```

### 4. 斜杠命令
```javascript
// 注册斜杠命令
discord.registerCommand({
  name: "weather",
  description: "查询天气",
  options: [{
    name: "city",
    type: "STRING",
    description: "城市名称",
    required: true
  }]
});
```

## 高级用法

### 1. 多服务器管理
```javascript
// 在多个服务器运行
const guilds = await discord.getGuilds();
for (const guild of guilds) {
  await discord.setConfig(guild.id, customConfig);
}
```

### 2. Embed 消息
```javascript
// 发送富文本消息
await discord.sendEmbed(channelId, {
  title: "每日报告",
  description: "今日数据摘要",
  fields: [
    { name: "新增用户", value: "128", inline: true },
    { name: "活跃用户", value: "512", inline: true }
  ],
  color: 0x00ff00,
  footer: { text: "OpenClaw Bot" }
});
```

### 3. 按钮/菜单交互
```javascript
// 发送带按钮的消息
await discord.sendComponents(channelId, {
  content: "请选择操作",
  components: [
    {
      type: "ACTION_ROW",
      components: [
        { type: "BUTTON", label: "确认", style: "SUCCESS", customId: "confirm" },
        { type: "BUTTON", label: "取消", style: "DANGER", customId: "cancel" }
      ]
    }
  ]
});
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Discord Bot Token | 机器人令牌 | Discord 开发者平台 |
| 服务器权限 | 管理服务器权限 | 服务器设置 |

## 权限说明

| 权限 | 用途 |
|------|------|
| Send Messages | 发送消息 |
| Read Messages | 读取消息 |
| Embed Links | 发送嵌入链接 |
| Manage Messages | 管理消息（删除等） |
| Administrator | 管理员权限 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [Discord 开发者文档](https://discord.com/developers/docs)
- [Discord.js 指南](https://discordjs.guide/)
- [Bot 最佳实践](https://discord.com/developers/docs/topics/best-practices)
