# TRACE — Transaction Risk and Anomaly Classification Engine

> Real-time financial transaction risk scoring system built with Java Spring Boot microservices, Kafka event streaming, JWT authentication, and a rule-based fraud detection engine.

![Java](https://img.shields.io/badge/Java-17-orange?style=flat-square&logo=openjdk)
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.5-brightgreen?style=flat-square&logo=springboot)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-event--driven-black?style=flat-square&logo=apachekafka)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-database-blue?style=flat-square&logo=postgresql)
![MongoDB](https://img.shields.io/badge/MongoDB-audit--log-green?style=flat-square&logo=mongodb)
![License](https://img.shields.io/badge/license-MIT-lightgrey?style=flat-square)

---

## Architecture

![TRACE Architecture](./docs/trace-architecture.svg)

A transaction submitted by a client travels through the API Gateway (JWT-authenticated), gets processed by the Transaction Service, and is published onto the **Kafka event bus**. Two downstream consumers act independently:

- **Risk Engine Service** — applies rule-based fraud detection and emits alerts for suspicious activity
- **Audit Log Service** — persists every event to MongoDB for a full immutable audit trail

High-risk transactions trigger the **Alert Service**, which sends email notifications in real time.

---

## Services

| Service | Port | Responsibility |
|---|---|---|
| `discovery-server` | 8761 | Eureka service registry |
| `api-gateway` | 8080 | JWT auth + request routing |
| `user-service` | 8081 | Registration, login, JWT issuance |
| `transaction-service` | 8082 | Transaction submission + Kafka publish |
| `risk-engine-service` | — | Rule-based fraud scoring |
| `alert-service` | — | Email alerts via Kafka consumer |
| `audit-log-service` | — | MongoDB audit trail |

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 17 |
| Framework | Spring Boot 3.4.5 |
| API Gateway | Spring Cloud Gateway |
| Service Discovery | Netflix Eureka |
| Security | Spring Security + JWT |
| Messaging | Apache Kafka |
| Databases | PostgreSQL + MongoDB |
| API Docs | Swagger / OpenAPI 3 |
| Containerisation | Docker + Docker Compose |

---

## Getting Started

### Prerequisites

- Java 17+
- Docker & Docker Compose

### Run with Docker Compose

```bash
git clone https://github.com/ritik-hedau18/TRACE-Transaction-Risk-and-Anomaly-Classification-Engine.git
cd TRACE-Transaction-Risk-and-Anomaly-Classification-Engine
docker-compose up --build
```

### Manual startup order

```
1. discovery-server   → :8761
2. api-gateway        → :8080
3. user-service       → :8081
4. transaction-service → :8082
5. risk-engine-service
6. alert-service
7. audit-log-service
```

---

## API Documentation

Swagger UI is available once the gateway is running:

```
http://localhost:8080/webjars/swagger-ui/index.html
```

---

## Environment Variables

| Variable | Description |
|---|---|
| `JWT_SECRET` | Secret key for JWT signing |
| `DB_USERNAME` | PostgreSQL username |
| `DB_PASSWORD` | PostgreSQL password |