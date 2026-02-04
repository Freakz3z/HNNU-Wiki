# Docker

## 什么是 Docker？

Docker 是一个开源的容器化平台，可以让开发者打包应用及其依赖到一个可移植的容器中，然后发布到任何流行的 Linux 机器上。

### 核心概念

- **容器（Container）**：轻量级、独立运行的软件包，包含运行应用所需的一切
- **镜像（Image）**：容器的只读模板，用于创建容器
- **Dockerfile**：用于构建Docker镜像的文本文件

### 为什么使用 Docker？

1. **环境一致性** - "在我机器上能跑"不再成为问题
2. **快速部署** - 秒级启动应用
3. **资源隔离** - 应用间互不干扰
4. **易于迁移** - 一次构建，到处运行

## 安装 Docker

### Windows
1. 下载 [Docker Desktop for Windows](https://www.docker.com/products/docker-desktop/)
2. 启用 WSL 2 功能
3. 运行安装程序并重启

### macOS
```bash
# 使用 Homebrew 安装
brew install --cask docker

# 或下载安装包
# https://www.docker.com/products/docker-desktop/
```

### Linux (Ubuntu/Debian)
```bash
# 安装依赖
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg

# 添加 Docker 官方 GPG 密钥
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# 设置仓库
sudo chmod a+r /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# 安装 Docker Engine
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# 验证安装
sudo docker run hello-world
```

## Docker 基本命令

### 镜像管理

```bash
# 搜索镜像
docker search nginx

# 拉取镜像
docker pull nginx:latest

# 查看本地镜像
docker images

# 删除镜像
docker rmi nginx:latest

# 构建镜像
docker build -t myapp:1.0 .
```

### 容器管理

```bash
# 运行容器
docker run -d -p 80:80 --name my-nginx nginx

# 查看运行中的容器
docker ps

# 查看所有容器（包括停止的）
docker ps -a

# 停止容器
docker stop my-nginx

# 启动已停止的容器
docker start my-nginx

# 重启容器
docker restart my-nginx

# 删除容器
docker rm my-nginx

# 强制删除运行中的容器
docker rm -f my-nginx

# 查看容器日志
docker logs my-nginx

# 实时查看日志
docker logs -f my-nginx

# 进入容器
docker exec -it my-nginx /bin/bash
```

### 参数说明

```bash
docker run [选项] 镜像 [命令]

常用选项：
-d, --detach          # 后台运行
-p, --publish list    # 发布端口（主机:容器）
--name string         # 指定容器名称
-v, --volume list     # 挂载卷（主机:容器）
-e, --env list        # 设置环境变量
--rm                  # 容器停止后自动删除
-it                   # 交互式终端
```

## 实战案例

### 案例 1：运行个人网站

```bash
# 拉取 nginx 镜像
docker pull nginx

# 创建静态文件目录
mkdir -p ~/my-website
echo "<h1>Hello Docker!</h1>" > ~/my-website/index.html

# 运行 nginx 容器
docker run -d \
  --name my-website \
  -p 8080:80 \
  -v ~/my-website:/usr/share/nginx/html \
  nginx

# 访问 http://localhost:8080
```

### 案例 2：运行 MySQL 数据库

```bash
# 运行 MySQL
docker run -d \
  --name mysql-server \
  -e MYSQL_ROOT_PASSWORD=my-secret-pw \
  -e MYSQL_DATABASE=myapp \
  -p 3306:3306 \
  -v mysql-data:/var/lib/mysql \
  mysql:8.0

# 进入 MySQL
docker exec -it mysql-server mysql -uroot -pmy-secret-pw

# 停止并删除
docker stop mysql-server
docker rm mysql-server
docker volume rm mysql-data
```

### 案例 3：运行 Python Web 应用

```bash
# 运行 Python 容器
docker run -d \
  --name python-app \
  -p 5000:5000 \
  -v $(pwd):/app \
  -w /app \
  python:3.11-slim \
  python -m http.server 5000
```

## Dockerfile 入门

### 什么是 Dockerfile？

Dockerfile 是一个文本文件，包含了构建 Docker 镜像的所有指令。

### 基础示例

```dockerfile
# 使用官方 Python 运行时作为基础镜像
FROM python:3.11-slim

# 设置工作目录
WORKDIR /app

# 复制依赖文件
COPY requirements.txt .

# 安装依赖
RUN pip install --no-cache-dir -r requirements.txt

# 复制应用代码
COPY . .

# 暴露端口
EXPOSE 5000

# 设置环境变量
ENV FLASK_APP=app.py
ENV FLASK_ENV=production

# 运行命令
CMD ["flask", "run", "--host=0.0.0.0"]
```

### 构建和运行

```bash
# 构建镜像
docker build -t myapp:1.0 .

# 运行容器
docker run -d -p 5000:5000 --name myapp myapp:1.0
```

### Dockerfile 最佳实践

```dockerfile
# 1. 使用具体版本标签
FROM python:3.11.2-slim

# 2. 合并 RUN 指令减少层数
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        gcc \
        && rm -rf /var/lib/apt/lists/*

# 3. 利用缓存（先复制依赖文件）
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .

# 4. 使用 .dockerignore
# 创建 .dockerignore 文件：
# .git
# __pycache__
# *.pyc
# .env

# 5. 非 root 用户运行
RUN useradd -m appuser
USER appuser

# 6. 健康检查
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost:5000/ || exit 1
```

## Docker Compose

### 什么是 Docker Compose？

Docker Compose 用于定义和运行多容器 Docker 应用。

### 安装

Docker Desktop 已包含 Compose 插件。

Linux 单独安装：
```bash
sudo apt-get install docker-compose-plugin
```

### docker-compose.yml 示例

```yaml
version: '3.8'

services:
  # Web 应用
  web:
    build: .
    ports:
      - "5000:5000"
    environment:
      - DATABASE_URL=postgresql://dbuser:password@db:5432/myapp
    depends_on:
      - db
    volumes:
      - .:/app
    restart: always

  # PostgreSQL 数据库
  db:
    image: postgres:15
    environment:
      - POSTGRES_USER=dbuser
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=myapp
    volumes:
      - db-data:/var/lib/postgresql/data
    restart: always

  # Redis 缓存
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    restart: always

  # Nginx 反向代理
  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - web
    restart: always

volumes:
  db-data:
```

### Compose 常用命令

```bash
# 启动所有服务
docker compose up -d

# 查看服务状态
docker compose ps

# 查看日志
docker compose logs -f

# 停止所有服务
docker compose down

# 停止并删除数据卷
docker compose down -v

# 重启服务
docker compose restart

# 构建镜像
docker compose build

# 查看服务资源使用
docker compose top
```

## 常见使用场景

### 开发环境

```bash
# 使用容器运行开发环境
docker run -it --rm \
  -v $(pwd):/workspace \
  -w /workspace \
  python:3.11 \
  bash
```

### 数据持久化

```bash
# 使用卷（Volume）
docker run -v my-data:/data postgres

# 使用绑定挂载
docker run -v $(pwd)/data:/data postgres
```

### 网络配置

```bash
# 创建自定义网络
docker network create my-network

# 连接容器到网络
docker run --network my-network --name container1 myapp
docker run --network my-network --name container2 myapp

# 容器间通过名称通信
# container2 可以通过 http://container1:8080 访问 container1
```

## 常用镜像推荐

### 开发工具

```bash
# Python
docker pull python:3.11

# Node.js
docker pull node:20

# 数据库
docker pull mysql:8.0
docker pull postgres:15
docker pull mongo:7

# 缓存
docker pull redis:7-alpine
docker pull memcached:alpine

# Web 服务器
docker pull nginx:alpine
docker pull apache:2.4
```

## 故障排查

### 容器无法启动

```bash
# 查看容器日志
docker logs <container-name>

# 查看容器详细信息
docker inspect <container-name>

# 查看容器资源使用
docker stats <container-name>
```

### 磁盘空间不足

```bash
# 查看磁盘使用
docker system df

# 清理未使用的镜像
docker image prune -a

# 清理未使用的容器
docker container prune

# 清理未使用的卷
docker volume prune

# 一键清理所有未使用的资源
docker system prune -a --volumes
```

### 网络问题

```bash
# 查看网络列表
docker network ls

# 查看网络详情
docker network inspect bridge

# 测试容器连通性
docker exec <container> ping <other-container>
```

## 安全建议

1. **不要在镜像中存储敏感信息** - 使用环境变量或 secrets
2. **使用非 root 用户** - Dockerfile 中添加 `USER` 指令
3. **定期更新镜像** - `docker pull` 获取最新版本
4. **扫描镜像漏洞** - 使用 `docker scan` 命令
5. **限制容器资源** - 使用 `--memory` 和 `--cpus` 参数

## 学习资源

- [Docker 官方文档](https://docs.docker.com/)
- [Dockerfile 最佳实践](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
- [Docker Compose 参考](https://docs.docker.com/compose/compose-file/)

## 下一步学习

完成本教程后，你可以：

1. **学习 Kubernetes** - 容器编排平台
2. **学习 CI/CD** - Jenkins、GitLab CI、GitHub Actions
3. **学习微服务架构** - 使用 Docker 构建微服务

祝你学习愉快！🐳
