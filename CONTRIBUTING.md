# 贡献指南

感谢你想要分享用 OpenClaw 做的事情！

## 快速开始

### 1. Fork 仓库
点击右上角 Fork 按钮。

### 2. 选择分类
根据你的使用场景，选择合适的目录：

| 分类 | 适用场景 |
|------|----------|
| `automation/` | 自动化任务、定时任务、批处理 |
| `content-creation/` | 写作、翻译、内容生成 |
| `development/` | 代码审查、PR 管理、CI/CD |
| `data-analysis/` | 数据处理、报告生成 |
| `personal-assistant/` | 日程管理、备忘、邮件 |
| `learning/` | 学习笔记、知识整理 |
| `tools/` | 第三方工具集成 |

### 3. 创建案例文件
文件名格式：`小写字母-用连字符连接.md`

例如：`daily-standup-report.md`

### 4. 使用模板

```markdown
# [案例名称]

## 干什么
<!-- 一句话描述 -->

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：
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
|  |  |  |

## 来源

- 贡献者：
- 来源：
- 日期：

## 相关资源

- 
```

### 5. 提交 PR

```bash
git checkout -b feature/your-case-name
git add .
git commit -m "feat: 添加 xxx 案例"
git push origin feature/your-case-name
```

然后创建 Pull Request。

## 贡献规范

### ✅ 欢迎
- 真实的使用案例
- 清晰的步骤说明
- 可复现的配置
- **脱敏处理**：不包含具体的个人信息、路径、日期

### ❌ 不接受
- 虚假内容
- 重复案例
- 侵犯版权的内容
- **泄露个人信息**：如具体路径、用户身份、敏感日期等

## 问题反馈

如有问题，请创建 [Issue](https://github.com/kaelinda/do-some-thing-with-claw/issues)。

---

感谢你的贡献！🎉
