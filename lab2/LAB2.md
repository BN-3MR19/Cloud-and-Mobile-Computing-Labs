# Lab 2 - Distributed Systems & CAP Theorem

## Overview
Lab 2 explores distributed systems principles, focusing on Redis and etcd implementations, and demonstrates the CAP theorem through practical examples.

## Docker Compose Configuration
The lab uses Docker Compose to orchestrate multiple services:

```yaml
version: '3'

services:
  redis-node1:
    image: redis:7
    container_name: redis-node1
    ports:
      - "6379:6379"
  
  redis-node2:
    image: redis:7
    container_name: redis-node2
    command: redis-server --replicaof redis-node1 6379
    ports:
      - "6380:6379"
  
  etcd:
    image: quay.io/coreos/etcd:v3.5.0
    container_name: etcd
    command: >
      /usr/local/bin/etcd
      --name node1
      --data-dir /etcd-data
      --advertise-client-urls http://0.0.0.0:2379
      --listen-client-urls http://0.0.0.0:2379
    ports:
      - "2379:2379"
```

## Services Deployed
- **Redis Node 1**: Primary Redis instance (master)
- **Redis Node 2**: Replica Redis instance (slave)
- **etcd**: Distributed key-value store with consensus

## Terminal Outputs
Demonstrates:
- Docker Compose service orchestration
- Container startup and configuration
- Service health checks
- Port mappings and network connectivity
- etcd endpoint status verification

## Key Concepts

### Redis & CAP Theorem
Redis replication demonstrates **eventual consistency** because updates from the master node are asynchronously propagated to replicas. During network partition, the system continues to accept writes, prioritizing **availability over consistency**. Once the partition is resolved, replicas synchronize data.

**System Type**: AP (Availability + Partition Tolerance)

### etcd & Raft Consensus
etcd uses the **Raft consensus algorithm** where a leader node is responsible for handling client requests. When the leader fails, a new leader is elected automatically by the remaining nodes. This ensures **high availability** and **strong consistency**.

**System Type**: CP (Consistency + Partition Tolerance)

## Important Commands Executed
- `docker-compose up -d`: Start all services in detached mode
- `docker ps`: List running containers
- `docker exec -it redis-node1 redis-cli`: Connect to Redis
- `docker exec -it etcd etcdctl endpoint status`: Check etcd status
- PUT/GET operations on etcd data store

## Learning Outcomes
- Understanding CAP theorem trade-offs in practice
- Implementing master-replica replication patterns
- Deploying consensus-based distributed systems
- Service orchestration using Docker Compose
- Network partitioning and failure scenarios
