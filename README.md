[English](README_EN.md) | [简体中文](README.md)

# 视频转MP3微服务系统

## 项目概述
这是一个基于微服务架构的视频转MP3系统，使用Flask作为后端框架，通过Kubernetes进行容器编排和管理。系统包含认证、网关、转换和通知等多个微服务模块。

## 技术栈
- 后端框架: Flask
- 容器化: Docker
- 编排管理: Kubernetes
- 消息队列: RabbitMQ
- 数据库: 
  - MySQL (用户认证)
  - MongoDB (文件存储)
- 监控工具: k9s
- 开发集群: minikube

## 系统架构
```
用户请求 → Ingress → Gateway → 
    ├─ Auth Service (认证)
    ├─ Converter Service (转换)
    └─ Notification Service (通知)
```

## 环境要求
- Kubernetes
- Docker
- MySQL
- MongoDB
- minikube

## 安装与部署

### 1. 创建虚拟环境并安装依赖
在每个服务目录下执行:
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2. 构建Docker镜像
```bash
docker build -t your-username/service-name .
```

### 3. 推送到阿里云ACR
```bash
docker login --username=your-username registry.cn-hangzhou.aliyuncs.com
docker tag your-username/service-name registry.cn-hangzhou.aliyuncs.com/your-namespace/service-name
docker push registry.cn-hangzhou.aliyuncs.com/your-namespace/service-name
```

### 4. Kubernetes部署
```bash
kubectl apply -f manifests/
```

## API文档

### 认证
- `POST /login` - 用户登录
- `POST /validate` - 验证token

### 文件处理
- `POST /upload` - 上传视频文件
- `GET /download` - 下载转换后的MP3文件

## 监控
使用k9s工具监控集群状态:
```bash
k9s
```

## 注意事项
1. 确保所有依赖服务(MongoDB, MySQL, RabbitMQ)已正确配置
2. 部署前修改各服务的Kubernetes manifests中的配置
3. 生产环境建议使用更安全的secret管理方式