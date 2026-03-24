# Docker 操作自动化

## 干什么
使用 OpenClaw 自动化 Docker 操作，包括镜像构建、容器管理、部署等。

## 怎么干

### 1. 准备工作
- 需要 OpenClaw 版本：>= 1.0.0
- 需要 Docker 安装并运行
- 需要 Docker 配置（镜像仓库凭证等）

### 2. 执行步骤

#### 方式一：命令行操作
```bash
# 查看容器状态
openclaw exec docker ps

# 构建镜像
openclaw exec docker build -t myapp:latest .

# 运行容器
openclaw exec docker run -d -p 8080:80 myapp:latest
```

#### 方式二：对话式操作
```
用户：帮我构建这个项目的 Docker 镜像
OpenClaw：[检查 Dockerfile] → [构建镜像] → [推送镜像]
✅ 镜像构建成功
镜像：myapp:v1.0.0
大小：256MB
```

### 3. 效果展示

**容器管理：**
```
🐳 Docker 容器状态

运行中：
- myapp-web (healthy) - 端口 8080
- myapp-db (healthy) - 端口 5432
- myapp-cache (healthy) - 端口 6379

资源使用：
- CPU: 25%
- 内存: 512MB / 2GB
- 磁盘: 1.2GB
```

## 常用操作

### 1. 镜像管理
```bash
# 构建镜像
docker build -t myapp:latest .

# 查看镜像
docker images

# 推送到仓库
docker push registry.example.com/myapp:latest

# 拉取镜像
docker pull nginx:alpine

# 删除镜像
docker rmi myapp:old-version
```

### 2. 容器管理
```bash
# 运行容器
docker run -d --name myapp \
  -p 8080:80 \
  -e NODE_ENV=production \
  -v /data:/app/data \
  myapp:latest

# 停止容器
docker stop myapp

# 启动容器
docker start myapp

# 重启容器
docker restart myapp

# 删除容器
docker rm myapp
```

### 3. 日志查看
```bash
# 查看日志
docker logs myapp

# 实时查看日志
docker logs -f myapp

# 查看最近 100 行
docker logs --tail 100 myapp
```

### 4. 进入容器
```bash
# 进入容器终端
docker exec -it myapp /bin/sh

# 执行命令
docker exec myapp npm test
```

## 高级用法

### 1. Docker Compose
```yaml
# docker-compose.yml
version: '3.8'
services:
  web:
    build: .
    ports:
      - "8080:80"
    environment:
      - NODE_ENV=production
    depends_on:
      - db
      - redis
  
  db:
    image: postgres:14
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_PASSWORD=secret
  
  redis:
    image: redis:alpine

volumes:
  pgdata:
```

```bash
# 启动所有服务
docker-compose up -d

# 查看服务状态
docker-compose ps

# 扩展服务
docker-compose up -d --scale web=3

# 停止所有服务
docker-compose down
```

### 2. 多阶段构建
```dockerfile
# Dockerfile 多阶段构建
# 构建阶段
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# 运行阶段
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### 3. 健康检查
```dockerfile
# Dockerfile 健康检查
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD curl -f http://localhost/health || exit 1
```

### 4. 自动化部署脚本
```bash
#!/bin/bash
# deploy.sh

# 拉取最新代码
git pull

# 构建新镜像
docker build -t myapp:$(git rev-parse --short HEAD) .

# 停止旧容器
docker stop myapp || true
docker rm myapp || true

# 启动新容器
docker run -d --name myapp \
  -p 8080:80 \
  --restart unless-stopped \
  myapp:$(git rev-parse --short HEAD)

# 清理旧镜像
docker image prune -f
```

### 5. 监控告警
```javascript
// 监控容器状态
async function monitorContainers() {
  const containers = await docker.listContainers();
  
  for (const container of containers) {
    if (container.state !== 'running') {
      await notify({
        channel: "slack",
        message: `⚠️ 容器 ${container.name} 已停止`
      });
    }
  }
}

// 每 5 分钟检查一次
setInterval(monitorContainers, 5 * 60 * 1000);
```

## 与 OpenClaw 集成场景

### 1. 自动重启失败容器
```javascript
// 监控并自动恢复
docker.on('container:stop', async (container) => {
  if (container.shouldRestart) {
    await docker.start(container.id);
    await notify(`容器 ${container.name} 已自动重启`);
  }
});
```

### 2. 定时清理
```javascript
// 每周清理未使用的镜像
schedule.scheduleJob("0 0 * * 0", async () => {
  await exec('docker system prune -af --volumes');
  await notify('Docker 清理完成');
});
```

### 3. 部署通知
```javascript
// 部署完成后通知
async function deployAndNotify() {
  await exec('docker-compose up -d');
  const status = await exec('docker-compose ps');
  await notify({
    channel: "slack",
    message: `✅ 部署完成\n\`\`\`${status}\`\`\``
  });
}
```

## 需要准备什么

| 依赖项 | 说明 | 获取方式 |
|--------|------|----------|
| OpenClaw | >= 1.0.0 | 官方安装 |
| Docker | 容器运行时 | https://docker.com |
| Docker Compose | 可选 | Docker Desktop 自带 |

## 常用命令速查

| 命令 | 说明 |
|------|------|
| `docker ps` | 查看运行中的容器 |
| `docker ps -a` | 查看所有容器 |
| `docker images` | 查看镜像列表 |
| `docker logs <容器>` | 查看日志 |
| `docker exec -it <容器> sh` | 进入容器 |
| `docker stats` | 资源使用统计 |
| `docker system prune` | 清理未使用资源 |

## 来源

- 贡献者：Community
- 来源：OpenClaw 社区
- 日期：2024

## 相关资源

- [Docker 官方文档](https://docs.docker.com/)
- [Docker Compose 指南](https://docs.docker.com/compose/)
- [Dockerfile 最佳实践](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
