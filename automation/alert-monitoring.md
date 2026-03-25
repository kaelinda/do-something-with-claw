# 监控告警

## 真实来源

- **技能**：healthcheck
- **位置**：`/opt/homebrew/lib/node_modules/openclaw/skills/healthcheck/`
- **工具**：OpenClaw security audit
- **工具**：openclaw cron

---

## 干什么
让 OpenClaw 自动监控系统状态，在异常发生时发送告警通知，支持多种监控指标和通知渠道。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的配置：监控规则、告警渠道
- 需要的权限：系统监控权限

### 2. 执行步骤

#### 方式一：系统安全审计

```bash
# 运行安全审计
openclaw security audit

# 深度审计
openclaw security audit --deep

# JSON 输出
openclaw security audit --json

# 自动修复安全配置
openclaw security audit --fix
```

#### 方式二：定时监控

使用 openclaw cron 设置定期检查：

```bash
# 添加定时任务
openclaw cron add --name "healthcheck:security-audit" \
  --schedule "0 9 * * *" \
  --command "openclaw security audit --deep"

# 查看定时任务
openclaw cron list

# 查看运行记录
openclaw cron runs
```

### 3. 效果展示

**安全审计结果：**
```
🔐 OpenClaw 安全审计

✅ 通过项：
- 文件权限配置正确
- 敏感文件已保护
- 网络配置安全

⚠️ 警告项：
- SSH 密钥未加密
- 部分端口对外开放

❌ 风险项：
- 发现 2 个高危漏洞

建议操作：
1. 加密 SSH 密钥
2. 关闭不必要的端口
3. 更新系统补丁
```

## healthcheck 技能功能

### 风险等级

| 等级 | 说明 |
|------|------|
| Home/Workstation Balanced | 家庭/工作站平衡模式 |
| VPS Hardened | VPS 加固模式 |
| Developer Convenience | 开发者便利模式 |
| Custom | 自定义模式 |

### 检查项目

1. **OS 和版本**：Linux/macOS/Windows，容器 vs 主机
2. **权限级别**：root/admin vs 用户
3. **访问路径**：本地控制台、SSH、RDP、tailnet
4. **网络暴露**：公网 IP、反向代理、隧道
5. **OpenClaw 网关状态**：绑定地址
6. **备份系统**：Time Machine、系统镜像、快照
7. **磁盘加密**：FileVault/LUKS/BitLocker
8. **自动更新**：安全更新状态

### 安全加固步骤

```bash
# 1. 查看当前状态
openclaw security audit --deep

# 2. 应用安全修复
openclaw security audit --fix

# 3. 检查版本状态
openclaw update status

# 4. 设置定期检查
openclaw cron add --name "healthcheck:security-audit" \
  --schedule "0 9 * * *" \
  --command "openclaw security audit --deep"
```

## 系统监控命令

### macOS

```bash
# 查看 CPU 使用率
top -l 1 | grep "CPU usage"

# 查看内存使用
vm_stat

# 查看磁盘使用
df -h

# 查看网络连接
lsof -nP -iTCP -sTCP:LISTEN

# 查看防火墙状态
/usr/libexec/ApplicationFirewall/socketfilterfw --getglobalstate
```

### Linux

```bash
# 查看 CPU 使用率
top -bn1 | grep "Cpu(s)"

# 查看内存使用
free -h

# 查看磁盘使用
df -h

# 查看监听端口
ss -ltnup

# 查看防火墙状态
ufw status
```

## 告警通知

### 飞书告警

```json
{
  "action": "send",
  "channel": "feishu",
  "to": "chat_id",
  "message": "🚨 系统告警\n\nCPU 使用率：92%\n阈值：80%\n持续时间：8 分钟"
}
```

### 企业微信告警

```json
{
  "action": "send",
  "channel": "wechat-work",
  "to": "chat_id",
  "message": "🚨 系统告警\n\nCPU 使用率：92%"
}
```

### Slack 告警

```json
{
  "action": "send",
  "channel": "slack",
  "to": "#alerts",
  "message": "🚨 系统告警\n\nCPU 使用率：92%"
}
```

## 定期监控配置

### 每日安全审计

```bash
openclaw cron add --name "healthcheck:security-audit" \
  --schedule "0 9 * * *" \
  --command "openclaw security audit --deep"
```

### 每周版本检查

```bash
openclaw cron add --name "healthcheck:update-status" \
  --schedule "0 10 * * 1" \
  --command "openclaw update status"
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 通知渠道 | 飞书/企微/Slack | 配置 webhook |
| 监控权限 | 系统访问 | 服务器配置 |

## 来源

- **技能路径**：`/opt/homebrew/lib/node_modules/openclaw/skills/healthcheck/SKILL.md`
- **工具**：openclaw security audit
- **工具**：openclaw cron

## 相关资源

- [监控最佳实践](https://docs.openclaw.ai/monitoring-best-practices)
- [定时任务配置](https://docs.openclaw.ai/scheduled-tasks)
- [飞书集成](tools/feishu-integration.md)
