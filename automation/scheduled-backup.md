# 定时备份

## 真实来源

- **工具**：rsync、tar、cron
- **工具**：openclaw cron
- **云存储**：S3/OSS/COS

---

## 干什么
让 OpenClaw 自动执行定时备份任务，支持文件备份、数据库备份、配置备份等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要的配置：备份目标路径、备份源路径
- 需要的权限：文件读写权限

### 2. 执行步骤

#### 方式一：使用 openclaw cron

```bash
# 添加每日备份任务
openclaw cron add --name "backup:daily" \
  --schedule "0 2 * * *" \
  --command "/path/to/backup.sh"

# 查看定时任务
openclaw cron list

# 查看运行记录
openclaw cron runs
```

#### 方式二：使用系统 cron

```bash
# 编辑 crontab
crontab -e

# 添加备份任务（每天凌晨2点）
0 2 * * * /path/to/backup.sh >> /var/log/backup.log 2>&1
```

### 3. 效果展示

**备份执行报告：**
```
✅ 备份任务完成

任务：项目文档备份
执行时间：2024-03-24 02:00:00
耗时：3 分 25 秒

备份详情：
- 文件数量：1,234 个
- 总大小：256 MB
- 压缩后：89 MB
- 备份位置：/backup/projects/2024-03-24/

保留策略：
- 当前保留：7 个备份
- 最早备份：2024-03-18
- 已清理：0 个过期备份

下次执行：2024-03-25 02:00:00
```

## 文件备份脚本

### 基本备份脚本

```bash
#!/bin/bash
# backup.sh

# 配置
SOURCE="/path/to/source"
TARGET="/backup"
DATE=$(date +%Y-%m-%d)
BACKUP_DIR="${TARGET}/${DATE}"

# 创建备份目录
mkdir -p "$BACKUP_DIR"

# 使用 rsync 同步
rsync -av --delete "$SOURCE/" "$BACKUP_DIR/"

# 压缩备份
tar -czf "${BACKUP_DIR}.tar.gz" -C "$TARGET" "$DATE"
rm -rf "$BACKUP_DIR"

# 清理旧备份（保留7天）
find "$TARGET" -name "*.tar.gz" -mtime +7 -delete

echo "备份完成: ${BACKUP_DIR}.tar.gz"
```

### 增量备份脚本

```bash
#!/bin/bash
# incremental-backup.sh

SOURCE="/path/to/source"
TARGET="/backup/incremental"
DATE=$(date +%Y-%m-%d)
LATEST_LINK=$(find "$TARGET" -maxdepth 1 -type d -name "2*" | sort | tail -n1)

# 增量备份
rsync -av --link-dest="$LATEST_LINK" "$SOURCE/" "${TARGET}/${DATE}/"

echo "增量备份完成: ${TARGET}/${DATE}/"
```

## 数据库备份

### PostgreSQL 备份

```bash
#!/bin/bash
# postgres-backup.sh

DATE=$(date +%Y-%m-%d)
BACKUP_DIR="/backup/database"
DB_NAME="production_db"

# 创建备份目录
mkdir -p "$BACKUP_DIR"

# 备份数据库
pg_dump "$DB_NAME" | gzip > "${BACKUP_DIR}/${DB_NAME}_${DATE}.sql.gz"

# 清理旧备份（保留30天）
find "$BACKUP_DIR" -name "*.sql.gz" -mtime +30 -delete

echo "数据库备份完成: ${DB_NAME}_${DATE}.sql.gz"
```

### MySQL 备份

```bash
#!/bin/bash
# mysql-backup.sh

DATE=$(date +%Y-%m-%d)
BACKUP_DIR="/backup/database"
DB_NAME="production_db"
DB_USER="backup_user"
DB_PASS="password"

# 创建备份目录
mkdir -p "$BACKUP_DIR"

# 备份数据库
mysqldump -u "$DB_USER" -p"$DB_PASS" "$DB_NAME" | gzip > "${BACKUP_DIR}/${DB_NAME}_${DATE}.sql.gz"

# 清理旧备份
find "$BACKUP_DIR" -name "*.sql.gz" -mtime +30 -delete

echo "数据库备份完成: ${DB_NAME}_${DATE}.sql.gz"
```

## 云存储备份

### AWS S3 同步

```bash
#!/bin/bash
# s3-backup.sh

LOCAL_BACKUP="/backup"
S3_BUCKET="s3://my-backup-bucket"

# 同步到 S3
aws s3 sync "$LOCAL_BACKUP" "$S3_BUCKET" \
  --storage-class STANDARD_IA \
  --exclude "*.tmp"

echo "S3 同步完成"
```

### 阿里云 OSS 同步

```bash
#!/bin/bash
# oss-backup.sh

LOCAL_BACKUP="/backup"
OSS_BUCKET="oss://my-backup-bucket"

# 同步到 OSS
ossutil cp -r "$LOCAL_BACKUP" "$OSS_BUCKET" --update

echo "OSS 同步完成"
```

## 备份验证

```bash
#!/bin/bash
# verify-backup.sh

BACKUP_FILE="/backup/database/db_2024-03-24.sql.gz"

# 验证压缩文件完整性
if gzip -t "$BACKUP_FILE" 2>/dev/null; then
    echo "✅ 备份文件完整性验证通过"
else
    echo "❌ 备份文件已损坏"
    exit 1
fi

# 验证数据库备份内容
if zcat "$BACKUP_FILE" | head -n 1 | grep -q "PostgreSQL"; then
    echo "✅ 数据库备份格式正确"
else
    echo "❌ 数据库备份格式异常"
    exit 1
fi
```

## 备份通知

使用 OpenClaw 发送备份通知：

```json
{
  "action": "send",
  "channel": "feishu",
  "to": "chat_id",
  "message": "✅ 备份任务完成\n\n任务：项目文档备份\n文件数：1,234 个\n大小：256 MB\n压缩后：89 MB"
}
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| 存储空间 | 备份存储 | 本地或云端 |
| 可选：云存储 | S3/OSS/COS | 云服务商 |

## 来源

- **工具**：rsync、tar、cron（系统内置）
- **工具**：openclaw cron（OpenClaw 内置）
- **云存储**：AWS S3 / 阿里云 OSS / 腾讯云 COS

## 相关资源

- [rsync 文档](https://linux.die.net/man/1/rsync)
- [PostgreSQL 备份](https://www.postgresql.org/docs/current/backup.html)
- [MySQL 备份](https://dev.mysql.com/doc/refman/8.0/en/backup-and-recovery.html)
