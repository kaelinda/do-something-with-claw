# Twitter/X 发推集成

## 真实来源

- **技能**：xurl
- **CLI**：xurl（X API 客户端）
- **安装**：`brew install xdevplatform/tap/xurl`

---

## 干什么
使用 OpenClaw 自动发布推文、回复、转发、搜索，管理 Twitter/X 账号互动。

## 怎么干

### 1. 准备工作

```bash
# 安装 xurl
brew install xdevplatform/tap/xurl

# 验证安装
xurl --help

# 认证（需用户手动在本地执行）
xurl auth oauth2

# 检查认证状态
xurl auth status
```

### 2. 执行步骤

**方式一：发布推文**

```bash
# 简单推文
xurl post "Hello from OpenClaw! 🤖"

# 带图片
xurl media upload photo.jpg
xurl post "Check this out!" --media-id MEDIA_ID
```

**方式二：回复推文**

```bash
# 回复
xurl reply 1234567890 "Great point!"

# 支持 URL
xurl reply https://x.com/user/status/1234567890 "Agreed!"
```

**方式三：引用推文**

```bash
xurl quote 1234567890 "My thoughts on this..."
```

**方式四：互动操作**

```bash
# 点赞
xurl like 1234567890

# 转发
xurl repost 1234567890

# 收藏
xurl bookmark 1234567890
```

**方式五：搜索推文**

```bash
# 搜索
xurl search "OpenClaw" -n 10

# 高级搜索
xurl search "from:elonmusk" -n 20
xurl search "#buildinpublic lang:en" -n 15
```

**方式六：用户操作**

```bash
# 查看自己
xurl whoami

# 查看用户
xurl user @XDevelopers

# 关注/取消关注
xurl follow @XDevelopers
xurl unfollow @XDevelopers

# 列出关注者
xurl followers -n 50
xurl following -n 50
```

**方式七：私信**

```bash
# 发送私信
xurl dm @someuser "Hey, saw your post!"

# 列出私信
xurl dms -n 10
```

### 3. 常用命令速查

| 操作 | 命令 |
|------|------|
| 发推 | `xurl post "text"` |
| 回复 | `xurl reply ID "text"` |
| 引用 | `xurl quote ID "text"` |
| 删除 | `xurl delete ID` |
| 点赞 | `xurl like ID` |
| 转发 | `xurl repost ID` |
| 搜索 | `xurl search "query" -n 10` |
| 用户 | `xurl user @handle` |
| 时间线 | `xurl timeline -n 20` |
| 提及 | `xurl mentions -n 10` |

### 4. 效果展示

```
X/Twitter 操作完成！

发推：
- ID: 1234567890
- 文本：Hello from OpenClaw! 🤖
- URL: https://x.com/user/status/1234567890

搜索结果（10 条）：
1. @user1: "Just discovered OpenClaw..."
2. @user2: "OpenClaw is amazing for..."
3. @user3: "Using OpenClaw to automate..."

用户信息：
- 名称：X Developers
- 关注者：1.2M
- 关注：12
- 推文：3,456
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| xurl | CLI 工具 | `brew install xdevplatform/tap/xurl` |
| X Developer 账号 | API 访问 | [developer.twitter.com](https://developer.twitter.com) |

## API 层级

| 层级 | 推文限制 | 月费 |
|------|----------|------|
| Free | 1,500 推文/月 | 免费 |
| Basic | 3,000 推文/月 | $100/月 |
| Pro | 50,000 推文/月 | $5,000/月 |

## 注意事项

- **安全**：不要在代理会话中使用 `--verbose` 或内联凭证
- **凭证文件**：`~/.xurl` 不要发送到 LLM 上下文
- **推文长度**：280 字符（中文约 140 字）
- **图片限制**：最多 4 张

## 相关资源

- [X API 文档](https://developer.twitter.com/en/docs)
- [xurl GitHub](https://github.com/xdevplatform/xurl)
- OpenClaw 技能：xurl
