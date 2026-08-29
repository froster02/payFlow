# TransferFlow

TransferFlow is a modular-monolith Java backend learning project built to demonstrate a legacy-to-modern-Java transition from a mainframe/COBOL background into fintech-style transfer orchestration, combining transactional correctness, distributed event flows, and production-minded operational foundations in one focused codebase.

```text
Client / legacy-system simulator
        v
Spring Boot Transfer API
        v
PostgreSQL — source of truth
        +-- Redis — cache + rate limiting
        +-- Kafka — transfer events
                     v
              Audit / reconciliation consumer
```

> **Design principle:** “PostgreSQL owns correctness, Redis improves speed, Kafka distributes events.”

## Tech stack

| Technology | Practical use |
| --- | --- |
| Java 21 | Primary language for backend domain and API logic |
| Spring Boot 3.x | Application bootstrap, dependency injection, and runtime conventions |
| PostgreSQL | Durable transfer state and correctness source of truth |
| JPA/Hibernate | ORM mapping and repository persistence layer |
| Redis | Read cache and rate-limiting support patterns |
| Kafka | Transfer event distribution and async integration boundary |
| Docker / Docker Compose | Local multi-service runtime for API + data/event dependencies |
| Testing (JUnit 5, Mockito, Testcontainers) | Unit and integration testing scaffolding |
| AWS (ECR, ECS, RDS, CloudWatch) | Target deployment and operations platform |
| Kubernetes (stretch) | Optional Week 9 deployment learning extension |

## Core API surface

| Method | Path | Purpose |
| --- | --- | --- |
| POST | `/transfers` (Idempotency-Key) | Create a simulated transfer with idempotent request semantics |
| GET | `/transfers/{id}` | Fetch latest transfer state |
| GET | `/transfers/{id}/history` | Retrieve transfer status/audit history |
| POST | `/transfers/{id}/cancel` | Attempt cancellation when business rules allow |
| GET | `/reconciliation?date=...` | Identify missing/inconsistent transfer audit events |

## Deliberately deferred

- outbox pattern
- Kafka retry/DLT
- load testing
- ElastiCache/MSK managed deployment
- full CI/CD pipeline
- legacy batch-file ingestion adapter

## Local setup (placeholder)

1. Clone the repository.
2. Start local dependencies: `docker compose up -d`.
3. Run Flyway migrations for the selected profile.
4. Start the Spring Boot app.
5. Verify health: `GET /actuator/health`.

## Interview discussion points

- Why PostgreSQL instead of Redis for transfer state?
- How did you prevent duplicate transfer requests?
- What happens if the database update succeeds but Kafka publishing fails?
- Why use a Kafka key based on transfer ID?
- What is cache invalidation?
- How does ECS deploy and scale a Docker container?
- How would you migrate this from a COBOL/mainframe flow?

## Resume line

“Built and deployed a Java Spring Boot transfer-orchestration service with PostgreSQL, Redis, Kafka, Docker, and AWS ECS; implemented idempotent APIs, transactional status management, event-driven auditing, reconciliation, and production health monitoring.”
