# iMessage/SMS 消息发送

## 真实来源

- **技能**：imsg
- **CLI**：imsg（macOS 专属）
- **平台**：macOS only
- **安装**：`brew install steipete/tap/imsg`

---

## 干什么
通过 OpenClaw 在 macOS 上发送 iMessage 和 SMS 消息。

## 怎么干

### 1. 准备工作

```bash
# 安装 imsg
brew install steipete/tap/imsg

# 授权
# 1. 终端需要"完全磁盘访问"权限
# 2. Messages.app 需要登录 Apple ID
```

### 2. 执行步骤

**方式一：列出聊天**

```bash
# 列出最近的聊天
imsg chats --limit 10 --json
```

**方式二：查看聊天记录**

```bash
# 按 chat_id 查看
imsg history --chat-id 1 --limit 20 --json

# 包含附件信息
imsg history --chat-id 1 --limit 20 --attachments --json
```

**方式三：发送消息**

```bash
# 发送文本
imsg send --to "+14155551212" --text "Hello from OpenClaw!"

# 发送带附件
imsg send --to "+14155551212" --text "Check this out" --file /path/to/image.jpg

# 指定服务类型
imsg send --to "+14155551212" --text "Hi" --service imessage  # iMessage
imsg send --to "+14155551212" --text "Hi" --service sms       # SMS
```

**方式四：监控新消息**

```bash
# 实时监控
imsg watch --chat-id 1 --attachments
```

### 3. 常用命令

| 命令 | 说明 |
|------|------|
| `imsg chats --limit N` | 列出最近 N 个聊天 |
| `imsg history --chat-id N` | 查看聊天记录 |
| `imsg send --to PHONE --text MSG` | 发送消息 |
| `imsg watch --chat-id N` | 监控新消息 |

### 4. 服务类型

| 选项 | 说明 |
|------|------|
| `--service imessage` | 强制 iMessage（蓝泡） |
| `--service sms` | 强制 SMS（绿泡） |
| `--service auto` | 自动选择（默认） |

### 5. 效果展示

```
iMessage 操作完成！

聊天列表：
1. Mom - +1555123456
2. Dad - +1555234567
3. Work Group - +1555345678

发送消息：
- 接收人：+1555123456
- 内容：我会晚点到
- 服务：iMessage
- 状态：已发送 ✅

监控模式：
- 聊天：Mom
- 等待新消息...
- 收到新消息：[消息内容]
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| macOS | 操作系统 | Apple 设备 |
| Messages.app | 系统应用 | macOS 自带 |
| Apple ID | 登录账户 | Apple 注册 |
| imsg | CLI 工具 | `brew install steipete/tap/imsg` |
| 完全磁盘访问 | 权限 | 系统偏好设置 |

## 安全注意

1. 发送前确认接收人和内容
2. 不向未知号码发送消息
3. 确认附件路径存在
4. 避免频繁发送（防骚扰）

## 相关资源

- [imsg 官网](https://imsg.to)
- [imsg GitHub](https://github.com/steipete/imsg)
- OpenClaw 技能：imsg
