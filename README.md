# Do Something with Claw

> 收集大家用 OpenClaw 做什么的开源仓库。

## 目录结构

```
├── automation/          # 自动化场景
│   ├── daily-report/    # 每日报告
│   ├── content-sync/    # 内容同步
│   └── ...
├── content-creation/    # 内容创作
│   ├── blog-writing/    # 博客写作
│   ├── translation/     # 翻译
│   └── ...
├── development/         # 开发辅助
│   ├── code-review/     # 代码审查
│   ├── pr-management/   # PR 管理
│   └── ...
├── data-analysis/       # 数据分析
├── personal-assistant/  # 个人助理
├── learning/            # 学习辅助
└── tools/               # 工具集成
```

## 如何贡献

### 1. 选择目录
根据你的使用场景，选择合适的目录分类。

### 2. 创建案例文件
每个案例一个 Markdown 文件，文件名用英文小写+连字符，如 `daily-standup-report.md`。

### 3. 填写模板

```markdown
# [案例名称]

## 干什么
<!-- 一句话描述你要做的事 -->

## 怎么干
<!-- 具体步骤、配置、命令等 -->

### 1. 准备工作
- 需要 OpenClaw 版本：x.x.x
- 需要的技能/插件：
- 需要的配置：

### 2. 执行步骤
1. 
2. 
3. 

### 3. 效果展示
<!-- 截图、日志、输出示例 -->

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= x.x.x | 官方安装 |
| xxx | xxx | xxx |

## 来源

- 贡献者：[你的名字]
- 来源：[原始链接/讨论/灵感]
- 日期：YYYY-MM-DD

## 相关资源

- [相关文档]()
- [相关技能]()
- [相关讨论]()
```

### 4. 提交 PR
1. Fork 本仓库
2. 创建分支：`git checkout -b feature/your-case-name`
3. 提交更改：`git commit -m 'feat: 添加 xxx 案例'`
4. 推送分支：`git push origin feature/your-case-name`
5. 创建 Pull Request

## 分类说明

| 分类 | 说明 | 示例 |
|------|------|------|
| automation | 自动化场景 | 定时报告、自动同步、监控告警 |
| content-creation | 内容创作 | 博客写作、翻译、文案生成 |
| development | 开发辅助 | 代码审查、PR 管理、CI/CD |
| data-analysis | 数据分析 | 数据清洗、报告生成、可视化 |
| personal-assistant | 个人助理 | 日程管理、邮件处理、备忘录 |
| learning | 学习辅助 | 笔记整理、知识问答、学习计划 |
| tools | 工具集成 | 第三方服务集成、API 调用 |

## 许可证

MIT License

---

**OpenClaw**: https://github.com/openclaw/openclaw
**文档**: https://docs.openclaw.ai
**社区**: https://discord.com/invite/clawd
