# Engine Infra

[![License](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

**Engine Framework Infrastructure** - Docker, Kubernetes, and deployment configurations for the AI Agent Orchestration System.

## 🚀 Overview

Complete infrastructure setup for deploying Engine Framework in development and production environments.

## 📁 Structure

```
infra/
├── docker/              # Docker configurations
│   ├── core/           # Engine Core container
│   ├── cli/            # CLI container
│   ├── web/            # Web dashboard container
│   └── docker-compose.yml
├── k8s/                # Kubernetes manifests
│   ├── base/           # Base configurations
│   ├── overlays/       # Environment overlays
│   └── helm/           # Helm charts
├── terraform/          # Infrastructure as Code
│   ├── modules/        # Reusable modules
│   └── environments/   # Environment configs
├── ci-cd/              # CI/CD pipelines
│   ├── github-actions/ # GitHub Actions
│   └── gitlab-ci/      # GitLab CI
└── monitoring/         # Observability
    ├── prometheus/     # Metrics collection
    ├── grafana/        # Dashboards
    └── logging/        # Log aggregation
```

## 🐳 Quick Start with Docker

### Development Environment

```bash
# Clone repository
git clone https://github.com/engine-agi/engine-infra.git
cd engine-infra

# Start all services
docker-compose up -d

# Access services
# - Engine Core API: http://localhost:8000
# - Web Dashboard: http://localhost:3000
# - PostgreSQL: localhost:5432
# - Redis: localhost:6379
```

### Production Deployment

```bash
# Deploy to Kubernetes
kubectl apply -f k8s/overlays/production/

# Or use Helm
helm install engine ./k8s/helm/engine
```

## 🏗️ Components

### Docker Services

#### Engine Core
- **Image**: `engine-agi/engine-core:latest`
- **Ports**: 8000 (API)
- **Dependencies**: PostgreSQL, Redis

#### Engine Web
- **Image**: `engine-agi/engine-web:latest`
- **Ports**: 3000 (Web UI)
- **Dependencies**: Engine Core API

#### Engine CLI
- **Image**: `engine-agi/engine-cli:latest`
- **Entry point**: CLI commands

### Databases

#### PostgreSQL
- **Version**: 15
- **Ports**: 5432
- **Volumes**: Persistent data

#### Redis
- **Version**: 7
- **Ports**: 6379
- **Usage**: Caching, workflows

## 🚀 Deployment Options

### 1. Docker Compose (Development)

```yaml
version: '3.8'
services:
  engine-core:
    image: engine-agi/engine-core:latest
    ports:
      - "8000:8000"
    environment:
      - DATABASE_URL=postgresql://user:pass@postgres:5432/engine
      - REDIS_URL=redis://redis:6379
    depends_on:
      - postgres
      - redis

  postgres:
    image: postgres:15
    environment:
      - POSTGRES_DB=engine
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass

  redis:
    image: redis:7-alpine
```

### 2. Kubernetes (Production)

```bash
# Deploy complete stack
kubectl apply -f k8s/overlays/production/

# Check status
kubectl get pods
kubectl get services
```

### 3. Cloud Deployment

#### AWS
```bash
# Use Terraform modules
cd terraform/environments/aws
terraform init
terraform apply
```

#### GCP
```bash
# Use Terraform modules
cd terraform/environments/gcp
terraform init
terraform apply
```

## 📊 Monitoring & Observability

### Prometheus Metrics
- Application metrics
- System resources
- Custom business metrics

### Grafana Dashboards
- Service overview
- Performance metrics
- Error tracking

### Logging
- Centralized log aggregation
- Structured logging
- Log retention policies

## 🔧 Configuration

### Environment Variables

```bash
# Database
DATABASE_URL=postgresql://user:pass@host:5432/db

# Redis
REDIS_URL=redis://host:6379

# API
API_HOST=0.0.0.0
API_PORT=8000

# Security
SECRET_KEY=your-secret-key
JWT_SECRET=your-jwt-secret
```

### Configuration Files

- `docker-compose.yml` - Local development
- `k8s/base/` - Kubernetes base configs
- `terraform/` - Infrastructure configs

## 🧪 Testing Infrastructure

### Local Testing
```bash
# Run tests with infrastructure
docker-compose -f docker-compose.test.yml up --abort-on-container-exit
```

### CI/CD Testing
- Automated testing on every PR
- Multi-environment testing
- Performance benchmarking

## 📚 Documentation

- [Deployment Guide](docs/deployment.md)
- [Configuration](docs/configuration.md)
- [Troubleshooting](docs/troubleshooting.md)

## 🤝 Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for infrastructure contribution guidelines.

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

**Part of the Engine Framework** | [engine-agi](https://github.com/engine-agi)