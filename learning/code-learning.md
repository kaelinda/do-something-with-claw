# 代码学习与理解

## 真实来源

- **工具**：OpenClaw read/exec 工具
- **场景**：阅读开源项目、学习新技术、代码审查

---

## 干什么
通过 OpenClaw 辅助学习代码，快速理解复杂项目结构和逻辑。

## 怎么干

### 1. 准备工作
- 目标代码库路径或 URL
- 学习目标（理解架构/学习特定功能/审查代码）

### 2. 执行步骤

**方式一：项目结构分析**

```
帮我理解这个项目的结构：
- 路径：/path/to/project
- 输出：目录结构 + 核心文件说明
- 重点：入口文件、配置文件、核心模块
```

**方式二：代码阅读辅助**

```
帮我阅读这段代码：
- 文件：src/auth/login.ts
- 目标：理解登录流程
- 输出：流程图 + 关键函数说明
```

**方式三：技术概念解释**

```
解释这个项目中使用的技术：
- 技术：React Hooks
- 代码位置：src/hooks/
- 输出：概念解释 + 项目中的实际用法
```

**方式四：代码审查建议**

```
审查这段代码并提出改进建议：
- 文件：src/utils/parser.ts
- 关注：性能、可读性、最佳实践
```

### 3. 常见学习场景

```markdown
## 学习新项目
1. "这个项目的整体架构是什么？"
2. "核心数据流是怎样的？"
3. "有哪些关键技术栈？"

## 学习新技术
1. "这个项目中 React Query 是怎么用的？"
2. "State 管理方案是什么？为什么这样选？"
3. "有哪些设计模式？"

## 代码审查
1. "这段代码有什么潜在问题？"
2. "如何优化这个函数的性能？"
3. "是否符合最佳实践？"
```

### 4. 效果展示

```
项目结构分析完成！

## 项目概览
- 名称：my-react-app
- 类型：React + TypeScript Web 应用
- 架构：前后端分离

## 目录结构
```
my-react-app/
├── src/
│   ├── components/   # UI 组件
│   ├── hooks/        # 自定义 Hooks
│   ├── services/     # API 调用
│   ├── utils/        # 工具函数
│   └── types/        # TypeScript 类型
├── public/           # 静态资源
└── tests/            # 测试文件
```

## 核心流程
1. 入口：src/index.tsx
2. 路由：src/App.tsx
3. 状态：React Query + Context
4. API：src/services/api.ts

## 关键技术
- React 18 + TypeScript
- React Query (数据请求)
- Tailwind CSS (样式)
- Vite (构建工具)

## 建议学习顺序
1. src/types/ - 理解数据结构
2. src/services/ - 理解 API 层
3. src/hooks/ - 理解业务逻辑
4. src/components/ - 理解 UI 实现
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 代码库 | 学习目标 | 本地路径或 Git URL |

## 相关资源

- OpenClaw 工具：read、exec
- OpenClaw 技能：github（查看远程仓库）
