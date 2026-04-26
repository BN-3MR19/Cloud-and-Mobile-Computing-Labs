# Lab 4 - Microservices Architecture

## Overview
Lab 4 demonstrates microservices architecture principles using Docker Compose with multiple independent services communicating over HTTP.

## Architecture Overview

### Services Implemented
1. **Product Service** (Port 5001)
   - Manages product catalog
   - Provides product information and pricing
   - Endpoint: `http://localhost:5001`

2. **Order Service** (Port 5002)
   - Handles order creation and processing
   - Depends on Product Service for pricing
   - Endpoint: `http://localhost:5002`

## Key Microservices Principles

### Microservices Benefits
- Each service is independent and can be deployed or scaled separately
- Enables team scalability and technology diversity
- Improves fault isolation at service boundaries

### Complexity Introduced
- Requires inter-service communication
- Network handling and failure management
- Distributed tracing and debugging
- Service discovery and load balancing

### Failure Impact
If product-service fails, order-service cannot complete requests → demonstrates service dependency and failure cascading in distributed systems.

## 12-Factor Principles Applied
- **Config via Environment Variables**: Services configured without hardcoding
- **Stateless Services**: No session state stored locally
- **Isolated Dependencies**: Each service manages its own dependencies
- **Process Isolation**: Services run in separate containers
- **Port Binding**: Services are self-contained HTTP servers

## API Endpoints

### Product Service
- `GET /health`: Health check
- `GET /products/<id>`: Retrieve product details
- Returns: `{"id": "1", "name": "Laptop", "price": 1200}`

### Order Service
- `GET /health`: Health check
- `POST /orders`: Create new order
  - Body: `{"product_id": "1", "quantity": 2}`
  - Response: `{"message": "Order created", "product": "Laptop", "quantity": 2, "total_price": 2400}`

## Commands Executed
```bash
# Start services
docker-compose up -d

# Check service status
docker ps

# Test product service
curl http://localhost:5001/health
curl http://localhost:5001/products/1

# Create orders
curl -X POST http://localhost:5002/orders \
  -H "Content-Type: application/json" \
  -d '{"product_id":"1","quantity":2}'

# Test failure scenario
docker stop product-service
curl -X POST http://localhost:5002/orders \
  -H "Content-Type: application/json" \
  -d '{"product_id":"2","quantity":1}'
# Returns: {"error":"product-service unavailable"}
```

## Docker Compose Configuration
```yaml
version: '3'
services:
  product-service:
    image: weeklid-lab-product-service:latest
    container_name: product-service
    ports:
      - "5001:5001"
    environment:
      - PORT=5001
  
  order-service:
    image: weeklid-lab-order-service:latest
    container_name: order-service
    ports:
      - "5002:5002"
    environment:
      - PORT=5002
      - PRODUCT_SERVICE_URL=http://product-service:5001
    depends_on:
      - product-service
```

## Build Metrics
- Product Service: ~1.8s build time
- Order Service: ~5.3s build time
- Layer caching utilized for faster subsequent builds

## Lessons Learned

### Service Dependencies
- Order Service depends on Product Service availability
- Network failures directly impact dependent services
- Graceful degradation and fallbacks needed

### Distributed Communication
- HTTP-based synchronous communication
- Latency and timeout considerations
- Error handling and retry logic essential

### Configuration Management
- Environment variables for service discovery
- Port configuration for multi-service setup
- Health checks for service availability

## Testing Scenarios
1. **Normal Operation**: Both services running, orders processed successfully
2. **Service Failure**: Product service stops, order service returns error
3. **Service Recovery**: Product service restarts, order service resumes normal operation

## Learning Outcomes
- Understanding microservices architecture patterns
- Implementing service-to-service communication
- Handling distributed system failures
- Following 12-factor application principles
- Docker Compose for multi-service orchestration
