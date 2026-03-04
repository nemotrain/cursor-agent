---
name: docker-china-mirror
description: Configures Docker to use Chinese registry mirrors when pulling images. Use when downloading Docker images, pulling images, or when the user mentions Docker image download issues, slow pulls, or China network access.
---

# Docker 中国镜像站配置

## 使用场景

当需要拉取 Docker 镜像时，优先检查并配置中国镜像站，以加速 pull 并避免网络不可达。

**触发条件**：用户执行 `docker pull`、安装/运行 Docker 镜像、或提及镜像拉取慢/失败时应用本技能。

## 操作流程

### 1. 检查当前配置

在执行 `docker pull` 前，先检查是否已配置镜像加速：

```bash
docker info | grep -A 5 "Registry Mirrors"
```

若输出为空或未包含国内镜像，则需配置。

### 2. 配置镜像站

使用以下命令更新 Docker 配置，添加中国镜像源：

```bash
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://dockerpull.com","https://docker.1panel.live","https://dockerproxy.cn","https://docker.hpcloud.cloud"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

### 3. 验证配置

重启后验证镜像站是否生效：

```bash
docker info
```

在输出中确认 `Registry Mirrors` 已列出上述镜像地址。

### 4. 拉取镜像

配置完成后执行拉取：

```bash
docker pull <镜像名>:<标签>
```

## 注意事项

- 若已有 `daemon.json`，需合并 `registry-mirrors` 字段，避免覆盖其他配置
- 修改配置后必须执行 `systemctl restart docker` 才能生效
- 镜像站可用性会随时间变化，可定期检查或替换失效地址
