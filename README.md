# TRACE — Transaction Risk and Anomaly Classification Engine

A production-style microservices backend system that detects fraudulent 
and high-risk financial transactions in real time using a rule-based engine.

## Architecture

Client → API Gateway (8080) → User Service (8081)
→ Transaction Service (8082)
↓ Kafka
→ Risk Engine Service
↓ Kafka
→ Alert Service (Email)
→ Audit Log Service (MongoDB)

## Services

| Service | Port | Description |
|---|---|---|
| discovery-server | 8761 | Eureka service registry |
| api-gateway | 8080 | JWT auth + routing |
| user-service | 8081 | Register, login, JWT |
| transaction-service | 8082 | Submit transactions |
| risk-engine-service | - | Rule-based fraud detection |
| alert-service | - | Email alerts via Kafka |
| audit-log-service | - | MongoDB audit trail |

## Tech Stack

- Java 17 + Spring Boot 3.4.5
- Spring Cloud Gateway + Eureka
- Spring Security + JWT
- Apache Kafka
- PostgreSQL + MongoDB
- Swagger / OpenAPI 3
- Docker + Docker Compose

## Running Locally

### Prerequisites
- Java 17+
- PostgreSQL
- MongoDB
- Kafka + Zookeeper

### Start order
1. discovery-server
2. api-gateway
3. user-service
4. transaction-service
5. risk-engine-service
6. alert-service
7. audit-log-service

## API Documentation

Swagger UI: `http://localhost:8080/webjars/swagger-ui/index.html`

## Environment Variables

| Variable | Description |
|---|---|
| JWT_SECRET | Secret key for JWT signing |
| DB_USERNAME | PostgreSQL username |
| DB_PASSWORD | PostgreSQL password |