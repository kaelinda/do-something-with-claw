# 博客/RSS 监控更新

## 真实来源

- **技能**：blogwatcher
- **CLI**：blogwatcher
- **GitHub**：https://github.com/Hyaxia/blogwatcher
- **安装**：`go install github.com/Hyaxia/blogwatcher/cmd/blogwatcher@latest`

---

## 干什么
自动监控博客和 RSS 订阅源，当有新内容更新时自动通知或执行后续操作。

## 怎么干

### 1. 准备工作

```bash
# 安装 blogwatcher
go install github.com/Hyaxia/blogwatcher/cmd/blogwatcher@latest

# 验证安装
blogwatcher --help
```

### 2. 执行步骤

**方式一：添加监控源**

```
添加博客监控：
- 博客名称：技术博客
- RSS 地址：https://example.com/feed.xml
- 检查频率：每小时
- 通知方式：飞书消息
```

**方式二：扫描更新**

```
扫描所有订阅源：
- 检查每个博客的最新文章
- 对比历史记录
- 列出新发现的文章
```

**方式三：管理订阅**

```
列出当前订阅的博客：
- 显示博客名称
- 显示 RSS 源地址
- 显示最后检查时间
```

### 3. blogwatcher 常用命令

```bash
# 添加博客
blogwatcher add "My Blog" https://example.com

# 列出所有博客
blogwatcher blogs

# 扫描更新
blogwatcher scan

# 列出文章
blogwatcher articles

# 标记文章为已读
blogwatcher read 1

# 标记所有文章为已读
blogwatcher read-all

# 移除博客
blogwatcher remove "My Blog"
```

### 4. 效果展示

```
$ blogwatcher blogs
Tracked blogs (3):

  xkcd
    URL: https://xkcd.com

  阮一峰的网络日志
    URL: https://www.ruanyifeng.com/blog/atom.xml

  美团技术团队
    URL: https://tech.meituan.com/feed

$ blogwatcher scan
Scanning 3 blog(s)...

  xkcd
    Source: RSS | Found: 4 | New: 1

  阮一峰的网络日志
    Source: Atom | Found: 5 | New: 2

  美团技术团队
    Source: RSS | Found: 8 | New: 3

Found 6 new article(s) total!
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| blogwatcher | CLI 工具 | `go install github.com/Hyaxia/blogwatcher/cmd/blogwatcher@latest` |
| Go | 运行环境 | Go 官网 |

## 相关资源

- [blogwatcher GitHub](https://github.com/Hyaxia/blogwatcher)
- OpenClaw 技能：blogwatcher
