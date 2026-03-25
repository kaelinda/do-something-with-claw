# 小红书内容发布

## 真实来源

- **技能**：xiaohongshu、xiaohongshu-publisher
- **MCP**：xiaohongshu-mcp
- **GitHub**：https://github.com/xpzouying/xiaohongshu-mcp

---

## 干什么
通过 OpenClaw 自动发布内容到小红书平台，支持图文笔记和视频笔记。

## 怎么干

### 1. 准备工作

```bash
# 1. 安装 xiaohongshu-mcp（Docker）
docker pull xpzouying/xiaohongshu-mcp:latest

# 2. 启动服务
docker run -d -p 18060:18060 \
  -v ~/xiaohongshu-mcp/data:/app/data \
  xpzouying/xiaohongshu-mcp:latest

# 3. 配置登录
# 将小红书 cookies 保存到 ~/xiaohongshu-mcp/data/cookies.json
```

### 2. 执行步骤

**方式一：搜索小红书内容**

```
搜索小红书内容：
- 关键词：AI 办公
- 限制：10 条
- 输出：标题 + 作者 + 互动数据
```

**方式二：获取帖子详情**

```
获取这个小红书帖子的详情：
- URL：https://www.xiaohongshu.com/explore/xxx

提取：
- 标题
- 正文
- 点赞/收藏数
- 评论列表
```

**方式三：发布图文笔记**

```
发布一篇小红书图文笔记：

标题：Gemini 3 Pro 炸场了！
正文：
🔥 Gemini 3 Pro 炸场了！核心亮点：

🏆 推理能力第一
📊 上下文窗口 100 万 tokens
🚀 多模态能力升级

适合场景：
✅ 复杂推理任务
✅ 长文档分析
✅ 代码生成

#AI #Gemini #科技前沿

图片：/path/to/cover.png
```

**方式四：自动格式转换**

```
将这篇文章转换为小红书格式并发布：

原文：
[paste long article]

要求：
- 标题 ≤ 20 字
- 正文 ≤ 1000 字
- emoji 风格
- 添加热门标签
```

**方式五：发表评论**

```
在这个小红书帖子下发表评论：
- URL：https://www.xiaohongshu.com/explore/xxx
- 内容：写得太好了，收藏了！
```

### 3. 命令参考

```bash
# 搜索内容
./search.sh "AI 办公"

# 获取推荐列表
./recommend.sh

# 获取帖子详情
./post-detail.sh <feed_id> <xsec_token>

# 发表评论
./comment.sh <feed_id> <xsec_token> "评论内容"

# 发布笔记
python3 simple_publish.py "标题" "正文内容"
```

### 4. 发布限制

| 限制项 | 说明 |
|--------|------|
| 标题 | 最多 20 字 |
| 正文 | 最多 1000 字（含 emoji） |
| 图片 | 最多 9 张 |
| 日发布 | 最多 50 条 |

### 5. 效果展示

```
小红书操作完成！

搜索结果（10 条）：
1. 🔥 AI 办公效率翻倍！这 5 个工具必须知道
   - 作者：职场小达人
   - 点赞：1.2万  收藏：8千
2. 💡 用 AI 写周报，领导都夸我效率高
   - 作者：效率控
   - 点赞：8千  收藏：5千
...

帖子详情：
- 标题：AI 办公效率翻倍！
- 点赞：12,345
- 收藏：8,765
- 评论：234 条

发布笔记：
- 标题：Gemini 3 Pro 炸场了！
- 正文：256 字（含 emoji）
- 图片：1 张
- 状态：发布成功 ✅
- 链接：https://www.xiaohongshu.com/explore/xxx

格式转换：
- 原文：3,456 字
- 转换后：987 字
- 压缩率：71%
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| xiaohongshu-mcp | MCP 服务 | Docker 安装 |
| 小红书账号 | 发布账号 | 小红书注册 |
| Cookies | 登录凭证 | 浏览器导出 |

## 相关资源

- [xiaohongshu-mcp GitHub](https://github.com/xpzouying/xiaohongshu-mcp)
- OpenClaw 技能：xiaohongshu、xiaohongshu-publisher
