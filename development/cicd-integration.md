# CI/CD 集成

## 真实来源

- **平台**：GitHub Actions、GitLab CI、Jenkins
- **工具**：gh CLI（GitHub）
- **官方文档**：
  - https://docs.github.com/en/actions
  - https://docs.gitlab.com/ee/ci/
  - https://www.jenkins.io/doc/

---

## 干什么
使用 OpenClaw 集成 CI/CD 流程，自动化构建、测试、部署等任务。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要 CI/CD 平台配置
- 需要相应的访问权限

### 2. 执行步骤

#### 方式一：监控 CI 状态
```
用户：检查最新的 CI 运行状态
OpenClaw：[调用 GitHub API] 
当前状态：
- build: ✅ 通过
- test: ✅ 通过
- deploy: 🔄 进行中
```

#### 方式二：触发 CI 流程
```bash
# 使用 gh CLI 触发 workflow
gh workflow run build.yml

# 查看运行状态
gh run list --limit 5
```

### 3. 效果展示

**CI 状态监控：**
```
📊 CI/CD 状态概览

最近运行：
1. build #123 ✅ 2 分钟前
2. test #122 ❌ 1 小时前
3. deploy #121 ✅ 3 小时前

失败任务：
- test #122: test_user_auth.py 失败
```

## GitHub Actions 配置

### 基本配置

```yaml
# .github/workflows/ci.yml
name: CI
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run build
      - run: npm test
```

### 自动部署

```yaml
# .github/workflows/deploy.yml
name: Deploy
on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Deploy to production
        run: |
          echo "Deploying to production..."
          # 部署命令
```

## GitLab CI 配置

```yaml
# .gitlab-ci.yml
stages:
  - build
  - test
  - deploy

build:
  stage: build
  script:
    - npm install
    - npm run build
  artifacts:
    paths:
      - dist/

test:
  stage: test
  script:
    - npm test
  dependencies:
    - build

deploy:
  stage: deploy
  script:
    - npm run deploy
  only:
    - main
```

## Jenkins 配置

```groovy
// Jenkinsfile
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'npm install'
        sh 'npm run build'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
      }
    }
    stage('Deploy') {
      when {
        branch 'main'
      }
      steps {
        sh 'npm run deploy'
      }
    }
  }
}
```

## 高级用法

### 1. CI 通知集成

在 CI 失败时发送通知：

```javascript
// OpenClaw 可以监控 CI 状态并发送通知
async function notifyOnFailure(run) {
  if (run.conclusion === 'failure') {
    await message({
      action: "send",
      channel: "slack",
      target: "#dev-alerts",
      message: `⚠️ CI 失败：${run.name}\n${run.html_url}`
    });
  }
}
```

### 2. 部署前检查

```javascript
// 部署前自动检查
async function preDeployCheck() {
  const checks = [
    { name: '测试通过', check: () => allTestsPassed() },
    { name: '代码审查', check: () => hasApproval() },
    { name: '无冲突', check: () => noMergeConflicts() },
    { name: '版本更新', check: () => versionBumped() }
  ];

  for (const { name, check } of checks) {
    if (!await check()) {
      throw new Error(`部署检查失败：${name}`);
    }
  }
}
```

### 3. 环境管理

```yaml
# 多环境部署配置
environments:
  development:
    branch: develop
    auto_deploy: true
  staging:
    branch: staging
    auto_deploy: true
  production:
    branch: main
    auto_deploy: false
    require_approval: true
```

## GitHub CLI 常用命令

```bash
# 查看 workflow 列表
gh workflow list

# 触发 workflow
gh workflow run <workflow-name>

# 查看运行列表
gh run list --limit 10

# 查看运行详情
gh run view <run-id>

# 查看运行日志
gh run view <run-id> --log

# 重新运行
gh run rerun <run-id>
```

## 最佳实践

1. **失败快速反馈**：CI 失败立即通知
2. **最小化构建时间**：缓存依赖、并行执行
3. **安全检查**：代码扫描、依赖审计
4. **环境隔离**：开发、测试、生产分离
5. **回滚机制**：快速回滚到上一版本

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| GitHub CLI | GitHub 操作 | `brew install gh` |
| CI/CD 平台 | 运行流水线 | GitHub/GitLab/Jenkins |

## 来源

- **平台**：GitHub Actions、GitLab CI、Jenkins
- **工具**：gh CLI（https://cli.github.com/）
- **官方文档**：
  - https://docs.github.com/en/actions
  - https://docs.gitlab.com/ee/ci/
  - https://www.jenkins.io/doc/

## 相关资源

- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [GitLab CI 文档](https://docs.gitlab.com/ee/ci/)
- [CI/CD 最佳实践](https://www.atlassian.com/continuous-delivery)
- [GitHub 集成](tools/github-integration.md)
