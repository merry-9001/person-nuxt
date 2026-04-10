# Nuxt 3 Demo with Docker CI/CD

这是一个最小可用的 Nuxt 3 示例项目，包含：

- 页面跳转：首页、关于页、文章列表页、动态文章详情页
- GitHub Actions CI/CD：单工作流完成安装依赖、类型检查、构建、镜像发布和远程部署

## 1. 本地启动

```bash
npm install
npm run dev
```

默认访问地址：

```bash
http://localhost:3000
```

## 2. 页面结构

```text
/
/about
/posts
/posts/nuxt-demo
```

## 3. GitHub Actions Secrets

在 GitHub 仓库 `Settings -> Secrets and variables -> Actions` 中配置：

- `DOCKERHUB_USERNAME`: Docker Hub 用户名
- `DOCKERHUB_TOKEN`: Docker Hub Access Token
- `SERVER_HOST`: 服务器 IP 或域名
- `SERVER_USERNAME`: 服务器 SSH 用户名
- `SERVER_SSH_KEY`: 服务器 SSH 私钥
- `SERVER_PORT`: 服务器 SSH 端口，通常是 `22`

## 4. 服务器准备

服务器建议使用 Ubuntu，并提前安装 Docker 与 Docker Compose：

```bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
newgrp docker
docker --version
docker compose version
```

创建部署目录：

```bash
sudo mkdir -p /opt/nuxt3-demo
sudo chown -R $USER:$USER /opt/nuxt3-demo
cd /opt/nuxt3-demo
```

## 5. 工作流说明

- `cd.yml`: 唯一的 CI/CD 工作流
- `pull_request`: 只执行安装、类型检查、构建
- `push`: 先执行构建校验，若分支是 `main` 则继续部署
- `workflow_dispatch`: 支持在 GitHub Actions 页面手动触发部署

## 6. 部署流程

1. 本地初始化 git 仓库并推送到 GitHub
2. 在 GitHub 配置好 Docker Hub 和服务器相关 Secrets
3. 确保服务器存在 `/opt/nuxt3-demo` 目录，并且 SSH 用户有写入权限
4. 推送到 `main` 分支后，GitHub Actions 会自动构建并推送镜像
5. 工作流会把 `docker-compose.prod.yml` 上传到服务器
6. 工作流随后通过 SSH 登录服务器，直接执行 Docker Compose 拉取最新镜像并重启容器

## 7. 容器端口

当前 `docker-compose.prod.yml` 映射为：

```yaml
ports:
  - "3000:3000"
```

如果你希望对外暴露 `80` 或 `8080`，可以改成：

```yaml
ports:
  - "80:3000"
```

或：

```yaml
ports:
  - "8080:3000"
```
