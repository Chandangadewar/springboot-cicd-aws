# 🚀 Scalable Backend API — Spring Boot + CI/CD + AWS

![Build and Push](https://img.shields.io/github/actions/workflow/status/Chandangadewar/springboot-cicd-aws/build-push.yml?branch=main&label=CI%2FCD%20Build&logo=github-actions&logoColor=white)
![Deploy to EC2](https://img.shields.io/github/actions/workflow/status/Chandangadewar/springboot-cicd-aws/deploy.yml?branch=main&label=Deploy%20to%20EC2&logo=amazon-aws&logoColor=white)
![Docker Pulls](https://img.shields.io/docker/pulls/chandan240603/springboot-cicd-aws?logo=docker&logoColor=white&color=blue)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.14-brightgreen?logo=springboot&logoColor=white)
![Java](https://img.shields.io/badge/Java-17-orange?logo=openjdk&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-6.0-green?logo=mongodb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue?logo=docker&logoColor=white)
![AWS EC2](https://img.shields.io/badge/AWS-EC2%20Deployed-FF9900?logo=amazon-aws&logoColor=white)
![Prometheus](https://img.shields.io/badge/Prometheus-Monitored-E6522C?logo=prometheus&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-Dashboard-F46800?logo=grafana&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## 📌 Project Overview

A **production-grade RESTful backend API** built with Spring Boot, following a layered **Controller → Service → Repository** architecture. The project demonstrates a complete DevOps lifecycle — from local development to containerization, automated CI/CD pipelines, cloud deployment on AWS EC2, and live monitoring with Prometheus and Grafana.

> 🎯 Built to demonstrate Backend + DevOps skills for Junior Cloud/DevOps Engineer roles.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Developer Machine                     │
│  Spring Boot API ──► Docker ──► GitHub Push             │
└─────────────────────────┬───────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                   GitHub Actions CI/CD                   │
│  build-push.yml ──► Build JAR ──► Docker Image ──►      │
│  Push to Docker Hub ──► Trigger deploy.yml              │
└─────────────────────────┬───────────────────────────────┘
                          │
                          ▼
┌─────────────────────────────────────────────────────────┐
│                   AWS EC2 (ap-south-1)                   │
│  docker-compose up ──► App + MongoDB + Prometheus +      │
│  Grafana running as containers                          │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Category | Technology |
|---|---|
| Backend | Spring Boot 3.5.14, Java 17 |
| Database | MongoDB 6.0 |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions |
| Cloud | AWS EC2 (t2.micro, ap-south-1) |
| Monitoring | Spring Actuator, Prometheus, Grafana |
| Build Tool | Maven |

---

## 📁 Project Structure

```
springboot-cicd-aws/
├── src/
│   └── main/java/com/Scalable/Backend/springboot_api/
│       ├── controller/        # REST API endpoints
│       ├── service/           # Business logic
│       ├── repository/        # MongoDB data access
│       ├── model/             # Data models
│       ├── dto/               # Data Transfer Objects
│       └── exception/         # Global exception handling
├── monitoring/
│   └── prometheus.yml         # Prometheus scrape config
├── .github/
│   └── workflows/
│       ├── build-push.yml     # CI - Build & Push to Docker Hub
│       └── deploy.yml         # CD - Auto deploy to AWS EC2
├── Dockerfile                 # Multi-stage Docker build
├── docker-compose.yml         # App + MongoDB + Prometheus + Grafana
└── pom.xml                    # Maven dependencies
```

---

## 🚀 6 Phases of Development

### ✅ Phase 1 — Spring Boot REST API
- Built RESTful CRUD API using layered architecture
- Controller → Service → Repository pattern
- Request validation using `@Valid`, `@NotBlank`, `@NotNull`
- Global exception handling with `@RestControllerAdvice`
- Connected to MongoDB with Spring Data

### ✅ Phase 2 — Dockerization
- Multi-stage `Dockerfile` (Maven build → JRE runtime)
- `docker-compose.yml` with app + MongoDB containers
- Tested full stack locally via Docker Compose

### ✅ Phase 3 — CI/CD Pipeline (GitHub Actions)
- `build-push.yml` triggers on every push to `main`
- Automatically builds JAR, builds Docker image
- Pushes image to Docker Hub: `chandan240603/springboot-cicd-aws:latest`

### ✅ Phase 4 — AWS EC2 Deployment
- Launched Ubuntu 22.04 t2.micro EC2 instance (ap-south-1)
- Installed Docker on EC2
- Deployed app via `docker-compose up -d`
- API live at `http://13.207.1.156:8080/api/products`

### ✅ Phase 5 — Auto Deploy Pipeline
- `deploy.yml` triggers automatically after build succeeds
- SSHs into EC2, pulls latest image, restarts containers
- Zero manual steps after every `git push`

### ✅ Phase 6 — Monitoring
- Spring Actuator exposes `/actuator/health` and `/actuator/prometheus`
- Prometheus scrapes metrics every 15 seconds
- Grafana dashboard visualizing JVM metrics, CPU usage, memory, HTTP requests

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/products` | Get all products |
| `GET` | `/api/products/{id}` | Get product by ID |
| `POST` | `/api/products` | Create new product |
| `PUT` | `/api/products/{id}` | Update product |
| `DELETE` | `/api/products/{id}` | Delete product |
| `GET` | `/actuator/health` | App health check |
| `GET` | `/actuator/prometheus` | Prometheus metrics |

---

## 🔄 CI/CD Pipeline Flow

```
git push to main
      │
      ▼
build-push.yml
      ├── Checkout code
      ├── Setup Java 17
      ├── mvn clean package
      ├── Docker login
      └── Build & Push image to Docker Hub
                │
                ▼
          deploy.yml
                ├── SSH into EC2
                ├── docker-compose pull
                ├── docker-compose up -d
                └── docker image prune -f
```

---

## 📊 Monitoring Stack

| Tool | URL | Purpose |
|---|---|---|
| Spring Actuator | `/actuator/health` | App health check |
| Prometheus | `localhost:9090` | Metrics collection |
| Grafana | `localhost:3000` | Metrics visualization |

**Metrics monitored:**
- JVM Heap & Non-Heap memory usage
- CPU usage (system + process)
- HTTP request rate, duration, errors
- MongoDB connection pool
- Application uptime

---

## 🏃 How to Run Locally

### Prerequisites
- Java 17
- Docker & Docker Compose
- Maven

### Run with Docker Compose
```bash
# Clone the repo
git clone https://github.com/Chandangadewar/springboot-cicd-aws.git
cd springboot-cicd-aws

# Start all services
docker-compose up --build

# API available at
curl http://localhost:8080/api/products

# Grafana at http://localhost:3000 (admin/admin)
# Prometheus at http://localhost:9090
```

### Run locally (without Docker)
```bash
# Start MongoDB
docker start mongodb

# Run Spring Boot app
mvn spring-boot:run

# Test
curl http://localhost:8080/api/products
```

---

## 🔐 GitHub Secrets Required

| Secret | Description |
|---|---|
| `DOCKER_USERNAME` | Docker Hub username |
| `DOCKER_PASSWORD` | Docker Hub password |
| `EC2_HOST` | EC2 public IP address |
| `EC2_SSH_KEY` | EC2 private key (PEM content) |

---

## 🐳 Docker Hub

Image: [`chandan240603/springboot-cicd-aws:latest`](https://hub.docker.com/r/chandan240603/springboot-cicd-aws)

```bash
docker pull chandan240603/springboot-cicd-aws:latest
```

---

## 📝 Sample API Request

```bash
# Create a product
curl -X POST http://localhost:8080/api/products \
  -H "Content-Type: application/json" \
  -d '{"name":"Laptop","category":"Electronics","price":75000}'

# Response
{"id":"69f8d08212076af55a677d56","name":"Laptop","category":"Electronics","price":75000.0}
```

---

## 👨‍💻 Author

**Chandan Gadewar**
- GitHub: [@Chandangadewar](https://github.com/Chandangadewar)
- Docker Hub: [chandan240603](https://hub.docker.com/u/chandan240603)

---

## ⭐ If you found this project helpful, give it a star!
