# 使用 Codex 自动编写代码

## 干什么
让 OpenAI Codex CLI 自动编写代码、修复 bug、重构项目。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要安装：`codex` CLI (`npm install -g @openai/codex`)
- 需要配置：OpenAI API Key

### 2. 执行步骤

**给 OpenClaw 发送指令：**

```
用 Codex 帮我在 ~/Projects/myapp 中添加暗色模式切换功能
```

**OpenClaw 会执行：**

```bash
# 一键执行（自动审批）
bash pty:true workdir:~/Projects/myapp command:"codex exec --full-auto 'Add a dark mode toggle button'"

# 或后台运行（长时间任务）
bash pty:true workdir:~/Projects/myapp background:true command:"codex --yolo 'Refactor the auth module'"
```

### 3. 效果展示

```
Codex 正在执行...
- 分析项目结构
- 创建 DarkModeToggle 组件
- 添加 CSS 变量
- 更新布局文件
- 提交更改

✅ 完成！创建了 3 个文件，修改了 5 个文件。
```

## 常用命令

| 场景 | 命令 |
|------|------|
| 快速执行 | `codex exec --full-auto "你的任务"` |
| 后台运行 | `codex --yolo "你的任务"` |
| 代码审查 | `codex review --base main` |
| 指定模型 | `codex --model gpt-5.2-codex "任务"` |

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Codex CLI | OpenAI 代码助手 | `npm install -g @openai/codex` |
| OpenAI API Key | 调用 GPT 模型 | OpenAI 官网 |

## 注意事项

⚠️ **Codex 需要在 Git 仓库中运行**，不在 Git 目录会报错。

```bash
# 临时目录快速执行
SCRATCH=$(mktemp -d) && cd $SCRATCH && git init && codex exec "你的任务"
```

## 来源

- 贡献者：Community
- 来源：OpenClaw 技能文档
- 日期：2024

## 相关资源

- [Codex CLI 文档](https://github.com/openai/codex)
- [coding-agent 技能](https://clawhub.com/skills/coding-agent)
