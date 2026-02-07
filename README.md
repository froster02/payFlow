# PayFlow – End-to-End Payment Processing Platform

PayFlow is a **cloud-agnostic, event-driven payment processing system** inspired by real-world platforms like **Stripe / Uber Payments**.  
It is designed to simulate **bank-grade payment flows** while giving deep **hands-on exposure** to Java, Spring Boot, Spring Security, Kafka, SQL, Redis, Batch processing, and System Design concepts required for **SDE-2 / FAANG interviews**.

---

## 🎯 What This Project Demonstrates

- Payment Authorization, Capture, Refund
- Ledger-based accounting (immutable entries)
- Tokenization & encryption of sensitive data
- Event-driven architecture using Kafka
- Idempotent REST APIs
- Batch settlement & reconciliation
- Secure microservices with JWT & RBAC
- Concurrency, thread safety, async processing
- Clean LLD & HLD aligned with interview expectations

---

## 🧠 System Design Artifacts

| Type | File |
|----|----|
| Logical HLD | `docs/hld.md` |
| Payment Service LLD | `docs/lld-payment-service.md` |
| API Contracts | `docs/api-contracts.md` |
| Database Schema | `docs/db-schema.md` |
| Build Plan (8 Weeks) | `docs/build-plan.md` |

---

## 🏗️ High-Level Architecture (Logical, Cloud-Agnostic)

```mermaid
flowchart LR
    UI[React Web App]
    GW[API Gateway]

    Auth[Auth Service]
    Pay[Payment Service]
    Token[Tokenization Service]
    Ledger[Ledger Service]

    Kafka[Event Bus]
    Notify[Notification Service]
    Batch[Settlement Service]

    UI --> GW
    GW --> Auth
    GW --> Pay

    Pay --> Token
    Pay --> Ledger
    Pay --> Kafka

    Kafka --> Notify
    Kafka --> Ledger
    Kafka --> Batch
