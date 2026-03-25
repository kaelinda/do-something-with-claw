# 自动收集 GitHub 开源主题

## 真实来源

- **技能**：github
- **工具**：exec（调用 gh CLI）
- **技能位置**：`/opt/homebrew/lib/node_modules/openclaw/skills/github/`
- **CLI**：GitHub CLI (`gh`)

---

## 干什么
让 OpenClaw 使用 GitHub CLI 自动搜索、筛选、下载 GitHub 上的开源主题文件，并整理到本地仓库。

## 怎么干

### 1. 准备工作

- OpenClaw 版本：>= 1.0.0
- GitHub CLI：已安装并登录
- Git 仓库：用于存放主题

### 2. 执行步骤

**方式一：搜索主题仓库**

```bash
# 使用 gh CLI 搜索仓库
gh search repos "prism theme" --stars ">1000" --limit 10

# 搜索语法高亮主题
gh search repos "syntax highlighting theme css" --stars ">500" --limit 20
```

**方式二：获取仓库内容**

```bash
# 获取仓库文件列表
gh api repos/PrismJS/prism/contents/themes --jq '.[].name'

# 下载特定文件
gh api repos/PrismJS/prism/contents/themes/prism-tomorrow.css \
  --jq '.content' | base64 -d > prism-tomorrow.css
```

**方式三：OpenClaw 指令**

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

## 常用 gh CLI 命令

### 搜索仓库

```bash
# 按星标数搜索
gh search repos "markdown theme" --stars ">1000"

# 按语言搜索
gh search repos "css theme" --language css

# 按许可证搜索
gh search repos "prism theme" --license mit

# 组合搜索
gh search repos "syntax theme css" --stars ">500" --license mit --limit 20
```

### 获取仓库信息

```bash
# 查看仓库详情
gh repo view PrismJS/prism

# 获取 README
gh repo view PrismJS/prism --json readme

# 获取许可证
gh repo view PrismJS/prism --json licenseInfo
```

### 下载文件

```bash
# 下载单个文件
gh api repos/owner/repo/contents/path/to/file --jq '.content' | base64 -d > local-file

# 克隆仓库
gh repo clone owner/repo --depth 1

# 下载发布文件
gh release download v1.0.0 --repo owner/repo
```

## 自动化脚本示例

```bash
#!/bin/bash
# 收集 Prism 主题

# 搜索仓库
repos=$(gh search repos "prism theme css" --stars ">100" --json name,owner --jq '.[] | "\(.owner.login)/\(.name)"')

for repo in $repos; do
  echo "处理仓库: $repo"
  
  # 检查许可证
  license=$(gh repo view $repo --json licenseInfo --jq '.licenseInfo.spdxId')
  if [[ "$license" != "MIT" && "$license" != "Apache-2.0" ]]; then
    echo "跳过：许可证不兼容 ($license)"
    continue
  fi
  
  # 获取主题文件列表
  files=$(gh api repos/$repo/contents/themes --jq '.[].name' 2>/dev/null)
  
  for file in $files; do
    if [[ "$file" == *.css ]]; then
      echo "下载: $file"
      gh api repos/$repo/contents/themes/$file --jq '.content' | base64 -d > "themes/$file"
    fi
  done
done

# 提交更改
git add themes/
git commit -m "feat: 添加新主题"
git push
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| GitHub CLI | gh 命令 | `brew install gh` |
| Git 仓库 | 存放主题 | GitHub 创建 |

## gh CLI 登录

```bash
# 登录 GitHub
gh auth login

# 验证登录状态
gh auth status
```

## 相关资源

- [GitHub CLI 文档](https://cli.github.com/manual/)
- [GitHub 技能文档](https://openclaw.ai/skills/github)
- [Markdown Theme Hub](https://github.com/kaelinda/markdown-theme-hub)
