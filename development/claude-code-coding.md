# 使用 Claude Code 自动编写代码

## 干什么
让 Anthropic Claude Code CLI 自动编写代码、修复 bug、重构项目。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要安装：`claude` CLI
- 需要配置：Anthropic API Key

### 2. 执行步骤

**给 OpenClaw 发送指令：**

```
用 Claude Code 帮我在 ~/Projects/myapp 中重构 API 调用模块
```

**OpenClaw 会执行：**

```bash
# 前台执行（推荐）
claude --permission-mode bypassPermissions --print 'Refactor the API calls with better error handling'

# 后台执行（长时间任务）
claude --permission-mode bypassPermissions --print 'Your task' &
```

### 3. 效果展示

```
Claude Code 正在执行...
- 分析现有 API 调用代码
- 识别重复模式
- 创建统一的 API 客户端
- 添加错误处理和重试逻辑
- 更新所有调用点

✅ 完成！重构了 12 个文件，减少了 300 行重复代码。
```

## 常用命令

| 场景 | 命令 |
|------|------|
| 快速执行 | `claude --print "你的任务"` |
| 跳过权限确认 | `claude --permission-mode bypassPermissions --print "任务"` |
| 后台运行 | 添加 `&` 或使用 `background:true` |

## Codex vs Claude Code

| 特性 | Codex | Claude Code |
|------|-------|-------------|
| PTY 模式 | 需要 | 不需要 |
| 权限模式 | `--full-auto` | `--permission-mode bypassPermissions` |
| 输出模式 | 默认 | `--print` |

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Claude CLI | Anthropic 代码助手 | Anthropic 官网 |
| Anthropic API Key | 调用 Claude 模型 | Anthropic 官网 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 技能文档
- 日期：2024

## 相关资源

- [Claude Code 文档](https://docs.anthropic.com/claude-code)
- [coding-agent 技能](https://clawhub.com/skills/coding-agent)
