# Lab 3 - Containers, Kubernetes & Orchestration

## Overview
Lab 3 focuses on containerization fundamentals, Kubernetes deployment, and container orchestration concepts.

## Topics Covered

### Container Internals
- **Namespaces**: Process isolation (PID, Network, Mount, UTS, IPC namespaces)
- **Cgroups**: Resource limitation and control groups
- **Filesystem Management**: Overlay filesystems and snapshot capabilities
- **Image Architecture**: Layer-based image construction

### Docker Setup
Comprehensive exploration of Docker architecture including:
- Container lifecycle management
- Image building and optimization
- Volume and network management
- Docker build metrics analysis

## Key Concepts

### Namespaces vs Cgroups
**Namespaces alone** only isolate processes but don't limit resource usage → processes can still consume unlimited CPU/memory.

**Cgroups** enforce limits on CPU, memory, etc. → preventing one container from starving others → improves stability.

### Image Layering Benefits
Image layering enables:
- **Caching**: Reuse of layers across builds
- **Efficiency**: Smaller updates and faster deployments
- **Storage Optimization**: Reduced disk usage at scale

### Kubernetes Concepts
- **Desired State**: Kubernetes maintains the system to match a defined configuration automatically (e.g., always 3 running Pods)
- **Self-Healing**: Automatic recovery (restart/replace Pods) → unlike manual intervention in traditional systems

### Health Checks
- **Readiness Probe**: Is app ready to serve traffic?
- **Liveness Probe**: Is app still alive?
→ Different purposes, not interchangeable

### Single-Node Limitation
Single-node limitation: no real scheduling decisions → cannot observe distribution, load balancing, or multi-node placement behavior

## Docker Commands Used
- `docker ps`: List running containers
- `docker inspect`: Examine container configuration
- `docker logs`: View container logs
- `docker exec`: Execute commands in containers
- `docker build`: Build custom images

## Kubernetes Artifacts
- Pod deployments and lifecycle management
- Service discovery and networking
- ConfigMaps and Secrets management
- Persistent volumes and storage

## Terminal Outputs
Demonstrates:
- Container resource inspection
- Process namespace isolation
- Memory and CPU metrics
- Network interface configuration
- Kubernetes cluster interactions

## Learning Outcomes
- Mastering containerization fundamentals
- Understanding kernel-level isolation mechanisms
- Deploying applications with Kubernetes
- Implementing self-healing and desired state
- Monitoring container health and metrics
