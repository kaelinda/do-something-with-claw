# CI/CD 集成

## 干什么
使用 OpenClaw 集成 CI/CD 流程，自动化构建、测试、部署等任务。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要 CI/CD 平台配置（GitHub Actions、GitLab CI 等）
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

## 常用平台配置

### 1. GitHub Actions
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

### 2. GitLab CI
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

### 3. Jenkins
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
```javascript
// CI 失败时发送通知
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

### 2. 自动修复失败
```javascript
// 检测测试失败并尝试修复
const failedTests = await getFailedTests();

for (const test of failedTests) {
  // 使用 coding-agent 修复
  await spawnAgent({
    task: `修复测试：${test.name}`,
    context: test.error
  });
}
```

### 3. 部署前检查
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

### 4. 环境管理
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

## 与 OpenClaw 结合场景

### 1. 定时构建检查
```javascript
// 每天早上检查 CI 状态
schedule.scheduleJob("0 9 * * *", async () => {
  const status = await checkCIHealth();
  if (status.failed > 0) {
    await notifyTeam(`有 ${status.failed} 个构建失败`);
  }
});
```

### 2. 自动创建发布
```javascript
// 合并到 main 后自动发布
onPushTo('main', async () => {
  const version = await getCurrentVersion();
  await createRelease(version);
  await deploy('production');
});
```

### 3. PR 自动标签
```javascript
// 根据更改自动添加标签
onPullRequest(async (pr) => {
  const changes = await getChanges(pr);
  if (changes.hasDocs) await addLabel(pr, 'documentation');
  if (changes.hasTests) await addLabel(pr, 'testing');
});
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| GitHub CLI | GitHub 操作 | `brew install gh` |
| CI/CD 平台 | 运行流水线 | GitHub/GitLab/Jenkins |

## 最佳实践

1. **失败快速反馈**：CI 失败立即通知
2. **最小化构建时间**：缓存依赖、并行执行
3. **安全检查**：代码扫描、依赖审计
4. **环境隔离**：开发、测试、生产分离
5. **回滚机制**：快速回滚到上一版本

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [GitLab CI 文档](https://docs.gitlab.com/ee/ci/)
- [CI/CD 最佳实践](https://www.atlassian.com/continuous-delivery)
