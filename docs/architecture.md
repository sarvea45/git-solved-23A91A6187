# System Architecture

## Overview

DevOps Simulator follows a microservices and event-driven architecture designed for high availability, scalability, and fast innovation. This document covers **production**, **development**, and **experimental** (AI/multi-cloud/chaos) architectures as enabled by environment.

---

## Components

### 1. Application Server

#### Production
- **Tech**: Node.js + Express
- **Port**: 8080
- **Scaling**: Horizontal auto-scaling
- **Debug**: Chrome DevTools debugger (limited)

#### Development
- **Tech Enhancements**: Hot reload, improved logs
- **Port**: 3000
- **Scaling**: Manual (single instance)
- **Debug Mode**: Fully enabled

#### Experimental
- **Tech Stack**: Node.js + Express + TensorFlow.js
- **Ports**: 9000 (main), 9001 (metrics), 9002 (AI API)
- **Scaling**: AI-powered predictive auto-scaling
- **Intelligence**: Real-time ML inference on traffic/usages
- **Message Queue**: Apache Kafka for event streaming

---

### 2. Database Layer

#### Production
- **Database**: PostgreSQL 14
- **Configuration**: Master-slave replication
- **Backup**: Daily automated backups

#### Development
- **Database**: PostgreSQL 14 single instance, local
- **Seed Data**: Auto-seed with dev/test data
- **Backup**: Manual only

#### Experimental
- **Architecture**: Multi-master PostgreSQL 14 cluster (5 nodes), Redis cluster cache
- **Advanced**: AI-powered query optimization, index suggestions, ML-based cache use
- **Replication**: Multi-region, continuous geo-redundant backups

---

### 3. Monitoring & Observability

#### Production
- **Tools**: Prometheus + Grafana, email notification alerts
- **Metrics**: CPU, Memory, Disk, Network
- **Logs**: Centralized, secure

#### Development
- **Tools**: Console logging, optional Prometheus, web dashboard in progress
- **Metrics**: Includes build time, more verbose

#### Experimental
- **Metrics**: Prometheus + Thanos (historical), advanced ML forecasting
- **Logs**: ELK stack + AI log analysis
- **AI/ML**: LSTM anomaly detection, load prediction (XGBoost), reinforcement learning for auto-scaling
- **Predictive Monitoring**: AI auto-scaling triggers, predictive dashboard

---

### 4. Container & Cloud Orchestration

#### Dev Only
- **Tool**: Docker Compose for app, database, cache
- **Volume Mounts**: For hot reload

#### Experimental
- **Orchestrator**: Kubernetes with custom resources (CRDs)
- **Multi-cloud**: AWS, Azure, GCP, DigitalOcean
- **Load Balancing**: Global anycast + GeoDNS, cross-cloud failover
- **Chaos Engineering**: Built-in chaos monkey for resilience

---

### 5. Authentication (Experimental in Dev)

- **Method**: OAuth2 + JWT for login
- **Providers**: Google, GitHub (dev)
- **Sessions**: Redis-based storage

---

## Deployment Strategy

### Production
- **Method**: Rolling updates
- **Zero-downtime**: Yes
- **Rollback**: Automated

### Development
- **Method**: Docker Compose with hot reload
- **Rollback**: `git checkout <commit>`
- **Testing**: Auto-seed, run unit tests, frequent commits

### Experimental
- **Method**: Canary/multi-cloud, AI-assisted deployments
- **Failover**: Automatic and cross-region/cloud
- **Chaos**: Fault injection, continuous resilience validation

---

## Security

### Production
- SSL/TLS for app and DB
- Secure credential handling
- Security audits

### Development
- SSL/TLS disabled
- Plain text credentials (do not use in production)
- Exposed debug/CORS endpoints

### Experimental
- Zero-trust cloud networking
- AES-256 encryption, comprehensive audit logs

---

## Development & Testing Workflow
- Make code changes (auto reload in dev/exp)
- Run unit tests & code analysis tools
- Check logs and dashboards
- Commit changes frequently
- Use `experimental` for AI/ML/multi-cloud/chaos features (these may be unstable)

---

## Experimental Features (Not Production Ready, Use With Caution)

- Multi-cloud deployment
- AI-powered log, traffic, and anomaly analysis (including auto-scaling triggers)
- Chaos engineering/fault injection
- Automatic rollback on anomaly detection

---

**Note:** All experimental and AI features should be *commented out*, toggled by env flags, or used only in non-production scenarios!
