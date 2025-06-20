[English](README_EN.md) | [Simplified Chinese](README.md)

# Video to MP3 Microservice System

## Project Overview
This is a microservices-based video to MP3 conversion system using Flask as the backend framework, with container orchestration and management via Kubernetes. The system includes multiple microservice modules such as authentication, gateway, conversion, and notification.

## Project Source
This project is inspired by the tutorial: [Microservice Architecture and System Design with Python & Kubernetes – Full Course](https://www.youtube.com/watch?v=hmkF77F9TLw).

## Tech Stack
- Backend Framework: Flask
- Containerization: Docker
- Orchestration: Kubernetes
- Message Queue: RabbitMQ
- Databases:
  - MySQL (User Authentication)
  - MongoDB (File Storage)
- Monitoring Tool: k9s
- Development Cluster: minikube

## System Architecture
```
User Request → Ingress → Gateway →
    ├─ Auth Service (Authentication)
    ├─ Converter Service (Conversion)
    └─ Notification Service (Notification)
```

## Environment Requirements
- Kubernetes
- Docker
- MySQL
- MongoDB
- minikube

## Installation & Deployment

### 1. Create Virtual Environment and Install Dependencies
Execute in each service directory:
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

### 2. Build Docker Image
```bash
docker build -t your-username/service-name .
```

### 3. Push to Alibaba Cloud ACR
```bash
docker login --username=your-username registry.cn-hangzhou.aliyuncs.com
docker tag your-username/service-name registry.cn-hangzhou.aliyuncs.com/your-namespace/service-namedocker push registry.cn-hangzhou.aliyuncs.com/your-namespace/service-name
```

### 4. Kubernetes Deployment
```bash
kubectl apply -f manifests/
```

## API Documentation

### Authentication
- `POST /login` - User login
- `POST /validate` - Validate token

### File Handling
- `POST /upload` - Upload video file
- `GET /download` - Download converted MP3 file

## Monitoring
Monitor cluster status using k9s tool:
```bash
k9s
```

## Notes
1. Ensure all dependent services (MongoDB, MySQL, RabbitMQ) are properly configured
2. Modify Kubernetes manifests in each service before deployment
3. Use more secure secret management methods in production environments