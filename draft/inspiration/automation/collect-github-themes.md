# 自动收集 GitHub 开源主题

## 干什么
让 OpenClaw 自动搜索、筛选、下载 GitHub 上的开源主题文件，并整理到本地仓库。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：无特殊要求
- 需要的配置：无

### 2. 执行步骤

**给 OpenClaw 发送指令：**

```
我要补充 Markdown 主题，帮我找：
1. 代码高亮向的主题
2. 暗色主题
3. 极简主题

收录标准：
- Stars > 1000
- MIT 许可
- 单文件 CSS
```

**OpenClaw 会自动：**
1. 搜索 GitHub 相关主题
2. 筛选符合标准的主题
3. 下载 CSS 文件到指定目录
4. 更新文档（README、来源清单等）
5. 提交并推送到远端

### 3. 效果展示

```
新增主题（5 套）：
- prism-vsc-dark-plus.css (VS Code 暗色)
- prism-atom-dark.css (Atom 暗色)
- prism-one-dark.css (One Dark)
- prism-darcula.css (IntelliJ Darcula)
- prism-ghcolors.css (GitHub 风格)

Commit: e896678
已推送到远端
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Git 仓库 | 存放主题 | GitHub 创建 |

## 来源

- 贡献者：Community
- 来源：Markdown Theme Hub 项目
- 日期：2024

## 相关资源

- [Markdown Theme Hub](https://github.com/kaelinda/markdown-theme-hub)
