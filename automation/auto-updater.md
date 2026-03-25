# 自动更新 OpenClaw 和技能

## 真实来源

- **技能**：auto-updater
- **CLI**：clawhub
- **功能**：自动检查并更新 OpenClaw 本体和已安装技能

---

## 干什么
设置定时任务，自动检查并更新 OpenClaw 本体和已安装的技能包。

## 怎么干

### 1. 准备工作

- OpenClaw 版本：>= 1.0.0
- auto-updater 技能已安装
- Cron 定时任务

### 2. 执行步骤

**方式一：手动检查更新**

```
检查 OpenClaw 和技能更新：
- 检查本体版本
- 检查已安装技能
- 列出可用更新
```

**方式二：自动更新配置**

```
配置自动更新：
- 更新频率：每天凌晨 3:00
- 更新范围：本体 + 所有技能
- 更新前备份：是
- 更新后通知：飞书消息
- 失败时回滚：是
```

**方式三：选择性更新**

```
只更新指定技能：
- 技能列表：obsidian-cli, feishu-doc
- 排除技能：experimental-skill
```

### 3. clawhub 命令

```bash
# 查看已安装技能
clawhub list

# 检查更新
clawhub outdated

# 更新所有技能
clawhub update

# 更新指定技能
clawhub update skill-name

# 查看技能详情
clawhub info skill-name
```

### 4. 自动化配置

```bash
# 添加 cron 任务
# crontab -e

# 每天凌晨 3 点自动更新
0 3 * * * /usr/local/bin/clawhub update --all >> ~/.openclaw/logs/update.log 2>&1

# 每周日备份后更新
0 3 * * 0 /usr/local/bin/clawhub backup && /usr/local/bin/clawhub update --all
```

### 5. 效果展示

```
自动更新完成！

更新时间：2026-03-25 03:00:15

本体更新：
- OpenClaw: 1.2.0 → 1.2.1
- 变更：修复内存泄漏问题

技能更新：
- obsidian-cli: 2.1.0 → 2.2.0
  - 新增：批量重命名功能
- feishu-doc: 1.3.0 → 1.3.1
  - 修复：权限校验问题

跳过更新：
- experimental-skill（用户配置排除）

更新日志：
- 备份位置：~/.openclaw/backups/2026-03-25
- 回滚命令：openclaw rollback 2026-03-25

通知已发送到飞书。
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| auto-updater | 自动更新技能 | 技能安装 |
| Cron | 定时任务 | 系统自带 |

## 相关资源

- OpenClaw 技能：auto-updater
- [ClawHub 技能市场](https://clawhub.com)
