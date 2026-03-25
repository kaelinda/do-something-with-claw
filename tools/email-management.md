# 邮件管理

## 真实来源

- **技能**：himalaya
- **CLI**：himalaya
- **安装**：`brew install himalaya`

---

## 干什么
通过 OpenClaw 管理电子邮件，包括查看、发送、回复、搜索、归档等操作。

## 怎么干

### 1. 准备工作

```bash
# 安装 himalaya
brew install himalaya

# 配置账户（交互式）
himalaya account configure

# 或手动创建配置
mkdir -p ~/.config/himalaya
```

配置文件 `~/.config/himalaya/config.toml`：

```toml
[accounts.personal]
email = "you@example.com"
display-name = "Your Name"
default = true

backend.type = "imap"
backend.host = "imap.example.com"
backend.port = 993
backend.encryption.type = "tls"
backend.login = "you@example.com"
backend.auth.type = "password"
backend.auth.cmd = "pass show email/imap"

message.send.backend.type = "smtp"
message.send.backend.host = "smtp.example.com"
message.send.backend.port = 587
```

### 2. 执行步骤

**方式一：查看邮件列表**

```bash
# 收件箱
himalaya envelope list

# 指定文件夹
himalaya envelope list --folder "Sent"

# 分页
himalaya envelope list --page 1 --page-size 20
```

**方式二：阅读邮件**

```bash
# 读取邮件
himalaya message read 42

# 导出原始 MIME
himalaya message export 42 --full
```

**方式三：搜索邮件**

```bash
# 搜索
himalaya envelope list from john@example.com subject meeting
```

**方式四：发送邮件**

```bash
# 交互式撰写
himalaya message write

# 直接发送
himalaya message write -H "To:recipient@example.com" -H "Subject:Test" "Message body"

# 使用模板
cat << 'EOF' | himalaya template send
From: you@example.com
To: recipient@example.com
Subject: Test Message

Hello from OpenClaw!
EOF
```

**方式五：回复邮件**

```bash
# 回复
himalaya message reply 42

# 回复所有
himalaya message reply 42 --all

# 转发
himalaya message forward 42
```

**方式六：管理邮件**

```bash
# 移动
himalaya message move 42 "Archive"

# 复制
himalaya message copy 42 "Important"

# 删除
himalaya message delete 42

# 标记已读
himalaya flag add 42 --flag seen
```

**方式七：附件**

```bash
# 下载附件
himalaya attachment download 42

# 指定目录
himalaya attachment download 42 --dir ~/Downloads
```

### 3. 多账户

```bash
# 列出账户
himalaya account list

# 使用指定账户
himalaya --account work envelope list
```

### 4. 效果展示

```
邮件管理完成！

收件箱（最新 5 封）：
1. [未读] 项目更新 - 张三 (2026-03-25 10:30)
2. [已读] 会议邀请 - 李四 (2026-03-25 09:15)
3. [已读] 周报提醒 - 系统 (2026-03-24 18:00)
4. [未读] 客户反馈 - 王五 (2026-03-24 15:20)
5. [已读] 系统通知 - Admin (2026-03-24 12:00)

邮件发送：
- 收件人：team@example.com
- 主题：项目进度更新
- 状态：已发送 ✅

附件下载：
- 文件：report.pdf
- 大小：2.3 MB
- 位置：~/Downloads/
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| himalaya | CLI 工具 | `brew install himalaya` |
| 邮箱账户 | IMAP/SMTP | 邮箱服务商 |

## 相关资源

- [Himalaya GitHub](https://github.com/pimalaya/himalaya)
- OpenClaw 技能：himalaya
