# Twitter/X 发推集成

## 干什么
使用 OpenClaw 自动发布推文、回复、转发，管理 Twitter/X 账号互动。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要 X API 凭证（API Key, API Secret, Access Token, Access Secret）
- xurl 技能

### 2. 执行步骤

#### 步骤 1：获取 X API 凭证
1. 访问 https://developer.twitter.com/
2. 创建项目和应用
3. 获取 API Key 和 Secret
4. 生成 Access Token 和 Secret
5. 配置 OAuth 2.0（可选）

#### 步骤 2：配置 OpenClaw
```yaml
# config.yaml
twitter:
  api_key: "your-api-key"
  api_secret: "your-api-secret"
  access_token: "your-access-token"
  access_secret: "your-access-secret"
```

#### 步骤 3：发送推文
```bash
# 使用 xurl 技能
openclaw xurl post-tweet --text "Hello from OpenClaw! 🤖"
```

### 3. 效果展示

**发推示例：**
```bash
$ openclaw xurl post-tweet --text "今天学到了一个新技能！"

输出：
✅ 推文发布成功
ID: 1234567890
URL: https://twitter.com/user/status/1234567890
```

## 常用功能

### 1. 发布推文
```javascript
// 基础推文
await xurl.postTweet({ text: "这是一条推文" });

// 带图片的推文
await xurl.postTweet({
  text: "看这张图片！",
  media: ["image1.jpg", "image2.jpg"]  // 最多4张
});
```

### 2. 回复推文
```javascript
await xurl.reply({
  tweetId: "original_tweet_id",
  text: "这是一条回复"
});
```

### 3. 转发推文
```javascript
await xurl.retweet({ tweetId: "tweet_id" });
```

### 4. 点赞推文
```javascript
await xurl.like({ tweetId: "tweet_id" });
```

### 5. 引用推文
```javascript
await xurl.quote({
  tweetId: "original_tweet_id",
  text: "我的评论"
});
```

## 高级用法

### 1. 线程推文
```javascript
// 发布推文线程
const tweets = [
  "第一推：今天要分享一个重要的话题",
  "第二推：这个话题关于...",
  "第三推：总结一下..."
];

let replyTo = null;
for (const text of tweets) {
  const result = await xurl.postTweet({
    text,
    replyTo
  });
  replyTo = result.id;
}
```

### 2. 定时发布
```javascript
// 使用定时任务
schedule.scheduleJob("0 9 * * *", async () => {
  await xurl.postTweet({ text: "早安！新的一天开始了 🌅" });
});
```

### 3. 搜索推文
```javascript
const results = await xurl.searchTweets({
  query: "#OpenClaw",
  count: 10
});
```

### 4. 获取用户时间线
```javascript
const timeline = await xurl.getUserTimeline({
  username: "username",
  count: 20
});
```

### 5. 发送私信
```javascript
await xurl.sendDM({
  userId: "recipient_id",
  text: "这是一条私信"
});
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| X Developer 账号 | API 访问权限 | https://developer.twitter.com |
| xurl 技能 | Twitter API 工具 | ClawHub 安装 |

## API 层级说明

| 层级 | 推文限制 | 月费 |
|------|----------|------|
| Free | 1,500 推文/月 | 免费 |
| Basic | 3,000 推文/月 | $100/月 |
| Pro | 50,000 推文/月 | $5,000/月 |

## 注意事项

1. **推文长度限制**：280 字符（中文约 140 字）
2. **图片限制**：最多 4 张，支持 JPG、PNG、GIF
3. **视频限制**：最大 512MB，最长 2 分 20 秒
4. **速率限制**：注意 API 调用频率限制

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区，xurl 技能文档
- 日期：2024

## 相关资源

- [Twitter API 文档](https://developer.twitter.com/en/docs)
- [xurl 技能](https://clawhub.com/skills/xurl)
- [Twitter 开发者门户](https://developer.twitter.com/)
