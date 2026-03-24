# 代码学习与解释

## 干什么
让 AI 解释代码逻辑、分析架构设计、生成文档注释，帮助快速理解复杂代码库。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的技能：无特殊要求
- 需要的配置：无

### 2. 执行步骤

**方式一：解释单个文件**

```
帮我解释这个文件的代码逻辑：
~/projects/my-app/src/auth/login.ts

重点关注：
- 核心函数的作用
- 数据流向
- 异常处理逻辑
```

**方式二：分析项目架构**

```
分析这个项目的架构：
~/projects/my-app/

需要了解：
- 目录结构设计
- 模块划分逻辑
- 技术栈选择
```

**方式三：生成代码文档**

```
为这个函数生成文档注释：
[粘贴代码]

格式要求：
- JSDoc 格式
- 包含参数说明
- 包含返回值说明
- 包含使用示例
```

**方式四：对比学习**

```
对比这两段代码的差异：
[代码 A]
[代码 B]

分析：
- 实现思路差异
- 性能差异
- 各自优缺点
```

**OpenClaw 会自动：**
1. 解析代码结构
2. 识别关键逻辑
3. 生成通俗易懂的解释
4. 提供相关最佳实践建议

### 3. 效果展示

```markdown
# 代码分析报告 | login.ts

## 文件概述
用户登录模块，处理认证、Token 管理、权限校验。

## 核心函数

### 1. `login(credentials: LoginParams): Promise<AuthResult>`

**作用**：处理用户登录请求

**流程**：
1. 校验输入参数（邮箱格式、密码长度）
2. 调用后端 API 进行认证
3. 成功后存储 Token 到 localStorage
4. 设置用户状态到全局 Store

**关键代码**：
```typescript
const response = await api.post('/auth/login', credentials);
const { token, user } = response.data;
localStorage.setItem('token', token);
store.setUser(user);
```

**异常处理**：
- 401：用户名或密码错误
- 429：请求过于频繁，触发限流
- 500：服务器错误，记录日志

### 2. `refreshToken(): Promise<string>`

**作用**：刷新访问令牌

**策略**：
- 在 Token 过期前 5 分钟自动刷新
- 失败后跳转登录页
- 支持并发请求合并

## 数据流向
```
用户输入 → 参数校验 → API 请求 → Token 存储 → 状态更新 → 页面跳转
```

## 最佳实践建议
1. Token 应使用 HttpOnly Cookie 存储，避免 XSS 攻击
2. 添加请求重试机制
3. 敏感操作需二次验证
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |

## 来源

- 贡献者：Community
- 来源：代码学习实践
- 日期：2024

## 相关资源

- [代码阅读技巧](https://openclaw.ai/docs/code-reading)
