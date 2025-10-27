# System Architecture

## Overview
DevOps Simulator follows a microservices architecture designed for high availability and scalability. This document covers both production and development (experimental features) configurations.

## Components

### 1. Application Server
- **Technology**: Node.js + Express (hot reload in development)
- **Production Port**: 8080
- **Development Port**: 3000
- **Scaling**: Horizontal auto-scaling (production), manual (dev)
- **Debug**: Chrome DevTools debugger enabled in development

### 2. Database Layer
- **Database**: PostgreSQL 14
- **Production**: Master-slave replication with daily automated backups
- **Development**: Local instance only, manual/auto seed data, no replication

### 3. Monitoring System
- **Production**: Prometheus + Grafana with email alerts for critical issues
- **Development**: Basic console logging, optional Prometheus, web dashboard in progress
- **Metrics**: CPU, Memory, Disk, Network, Build time
- **Alerts**: Email (prod), console warnings (dev)

### 4. Container Orchestration (Dev Only)
- **Tool**: Docker Compose (local only)
- **Services**: App, Database, Redis cache
- **Volume Mounts**: Code directory for hot reload

### 5. Authentication System (Experimental—Dev Only)
- **Method**: OAuth2 + JWT
- **Providers**: Google, GitHub (test setups)
- **Sessions**: Redis-based session storage

## Deployment Strategy

### Production
- **Method**: Rolling updates
- **Zero-downtime**: Yes
- **Rollback**: Automated on failure

### Development
- **Method**: Docker Compose (hot reload)
- **Zero-downtime**: Not applicable (dev)
- **Rollback**: `git checkout <commit>`

## Development Workflow
1. Make code changes (auto reload)
2. Run unit tests
3. Check logs
4. Commit when ready

## Security

### Production
- SSL/TLS encryption for app and database
- Secure credential storage
- Regular security audits

### Development
- SSL/TLS disabled
- Credentials in plain text (not for prod use!)
- CORS enabled for all origins
- Debug endpoints exposed

## Experimental Features (Development Only)
⚠️ **Warning**: The following features are experimental and should not be enabled in production:
- Multi-cloud deployment
- AI-powered log analysis
- Automatic rollback on anomaly detection
