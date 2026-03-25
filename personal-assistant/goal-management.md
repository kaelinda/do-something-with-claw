# 目标管理

## 真实来源

- **技能**：things-mac
- **位置**：`/opt/homebrew/lib/node_modules/openclaw/skills/things-mac/`
- **CLI 工具**：things CLI
- **方法论**：SMART 目标原则

---

## 干什么
使用 OpenClaw 进行目标管理，包括目标设定、进度追踪、里程碑提醒等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 可选：Things 3（things CLI）
- 可选：Obsidian、飞书多维表格

### 2. 执行步骤

#### 方式一：对话式管理
```
用户：帮我把「完成项目上线」拆分成可执行的里程碑
OpenClaw：已拆分目标「完成项目上线」：

1. 需求评审（预计 3 天）
2. 设计确认（预计 2 天）
3. 开发完成（预计 10 天）
4. 测试验收（预计 5 天）
5. 正式上线（预计 1 天）

预计总时长：21 天
需要我帮你创建任务吗？
```

#### 方式二：使用 Things 3

```bash
# 创建项目
things add "完成项目上线" --list "项目"

# 创建项目中的任务
things add "需求评审" --list "项目" --heading "完成项目上线"
things add "设计确认" --list "项目" --heading "完成项目上线"
things add "开发完成" --list "项目" --heading "完成项目上线"
things add "测试验收" --list "项目" --heading "完成项目上线"
things add "正式上线" --list "项目" --heading "完成项目上线"

# 查看项目进度
things show "完成项目上线"
```

### 3. 效果展示

**目标看板：**
```
🎯 目标管理看板

年度目标：
├── 技术成长
│   ├── 学习 Rust（进度：60%）
│   ├── 完成开源项目（进度：30%）
│   └── 写 12 篇技术博客（进度：75%）
│
├── 健康管理
│   ├── 减重 5kg（进度：40%）
│   ├── 每周运动 3 次（进度：80%）
│   └── 完成马拉松（进度：0%）
│
└── 财务规划
    ├── 存款目标（进度：50%）
    └── 投资学习（进度：100%）

总进度：54%
```

## SMART 目标设定

SMART 原则是目标管理的经典方法：

| 原则 | 说明 | 示例 |
|------|------|------|
| Specific（具体） | 目标要明确具体 | "学习 Rust" 而非 "学习新技术" |
| Measurable（可衡量） | 目标要可量化 | "完成 3 个 Rust 项目" 而非 "学会 Rust" |
| Achievable（可实现） | 目标要有挑战但可实现 | 根据自身能力设定 |
| Relevant（相关性） | 目标与整体方向一致 | 与职业发展相关 |
| Time-bound（有时限） | 目标要有截止日期 | "在 Q2 结束前完成" |

## Things CLI 目标管理

### 创建项目型目标

```bash
# 创建项目
things add "完成开源项目" --list "目标"

# 添加里程碑
things add "确定项目方向" --list "目标" --heading "完成开源项目" --deadline 2024-02-15
things add "完成核心功能" --list "目标" --heading "完成开源项目" --deadline 2024-03-15
things add "发布 1.0 版本" --list "目标" --heading "完成开源项目" --deadline 2024-04-15

# 添加到区域（年度目标）
things add "技术成长" --list "Areas"
```

### 设置截止日期

```bash
# 设置截止日期
things add "完成论文" --deadline 2024-06-01

# 设置开始日期
things add "开始新项目" --when 2024-03-01 --deadline 2024-06-01
```

### 使用标签分类

```bash
# 创建目标标签
things add "完成项目" --tags "目标,2024"

# 按标签查询
things search "#目标"
```

## OKR 管理

OKR（Objectives and Key Results）是另一种目标管理方法：

```markdown
# Q1 OKR

## Objective: 提升产品用户体验

### Key Results:
- [ ] 用户满意度从 80% 提升到 90%（当前：85%）
- [ ] 页面加载时间降低 50%（当前：降低 30%）
- [ ] 用户留存率提升 10%（当前：提升 5%）

### 进度追踪：
| 周次 | KR1 | KR2 | KR3 | 备注 |
|------|-----|-----|-----|------|
| W1   | 82% | 20% | 2%  |      |
| W2   | 84% | 25% | 3%  |      |
| W3   | 85% | 30% | 5%  |      |
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Things 3 | 可选 | App Store |
| Obsidian | 可选 | https://obsidian.md |

## 来源

- **技能路径**：`/opt/homebrew/lib/node_modules/openclaw/skills/things-mac/SKILL.md`
- **方法论**：SMART 目标原则、OKR 管理方法
- **Things CLI 项目**：https://github.com/ossianhempel/things3-cli

## 相关资源

- [SMART 目标原则](https://www.mindtools.com/a4wo118/smart-goals)
- [OKR 管理方法](https://www.whatmatters.com/)
- [Things 3 任务管理](tools/things-integration.md)
- [习惯追踪](personal-assistant/habit-tracking.md)
