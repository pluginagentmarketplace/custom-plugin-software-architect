---
name: backend-development
description: Build scalable backend systems with Node.js, Python, Java, Go, PHP, and GraphQL. Learn server architecture, database design, API development, authentication, microservices, and deployment. Use when building APIs, backend services, or server-side applications.
---

# Backend Development Skill

## Quick Start

Build production-ready backend systems with modern frameworks and best practices.

### Core Path: Node.js/Python → Databases → APIs → Microservices

```python
# Python FastAPI REST API
from fastapi import FastAPI, HTTPException
from sqlalchemy import create_engine
from typing import List
import uvicorn

app = FastAPI()

# Example: GET /users/{user_id}
@app.get("/users/{user_id}")
async def get_user(user_id: int):
    # Database query logic
    return {"id": user_id, "name": "John Doe"}

# Example: POST /users
@app.post("/users")
async def create_user(user: dict):
    # Validation and database insert
    return {"status": "created", "user": user}

if __name__ == "__main__":
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

## What You'll Learn

### Foundation Level (Weeks 1-12)
- **Server Concepts:** HTTP, request/response, REST principles
- **Choose Language:** Node.js, Python, Java, Go, or PHP
- **Web Frameworks:** Express (Node), Django (Python), Spring Boot (Java)
- **Databases:** SQL basics, NoSQL introduction, ORM patterns

### Intermediate Level (Weeks 13-32)
- **APIs:** RESTful design, OpenAPI, GraphQL introduction
- **Authentication:** JWT, OAuth 2.0, API keys, authorization
- **Database Integration:** Complex queries, transactions, indexing
- **Backend Patterns:** Middleware, logging, error handling

### Advanced Level (Weeks 33-52+)
- **Microservices:** Service communication, event-driven architecture
- **Performance:** Caching, rate limiting, optimization
- **DevOps:** Docker, Kubernetes, CI/CD pipelines
- **Cloud:** AWS, GCP, Azure services and deployment
- **GraphQL:** Schema design, resolvers, subscriptions

## Technologies by Language

**Node.js Ecosystem:**
- Express, Fastify, NestJS
- Sequelize, TypeORM, Prisma
- GraphQL Apollo, Socket.io

**Python Ecosystem:**
- Django, FastAPI, Flask
- SQLAlchemy, Django ORM
- Celery (async tasks)

**Java Ecosystem:**
- Spring Boot, Spring Cloud
- Hibernate, MyBatis
- Kafka, RabbitMQ

**Go Ecosystem:**
- Gin, Echo, gRPC
- GORM, sqlc
- Built-in concurrency

**PHP Ecosystem:**
- Laravel, Symfony
- Eloquent ORM, Doctrine
- Blade templating

## Architecture Patterns

**Monolithic:** Single codebase, all-in-one deployment
**Microservices:** Distributed services, independent scaling
**Serverless:** FaaS (Functions as a Service)
**Event-Driven:** Async communication via events
**CQRS:** Command Query Responsibility Segregation

## Learning Outcomes

After completing this skill:

✅ Design and build RESTful APIs
✅ Implement GraphQL services
✅ Master database design and optimization
✅ Secure applications with authentication/authorization
✅ Build microservices architectures
✅ Optimize performance and caching
✅ Deploy to production
✅ Monitor and debug backend systems

## Project Examples

1. **Blog API** - CRUD operations, user authentication
2. **E-commerce Backend** - Product catalog, orders, payments
3. **Real-time Chat API** - WebSockets, user management
4. **GraphQL API** - Schema design, resolvers
5. **Microservices System** - Multiple services, API Gateway

## Database Patterns

```python
# Repository Pattern
class UserRepository:
    def __init__(self, db_session):
        self.db = db_session

    def get_by_id(self, user_id):
        return self.db.query(User).filter(User.id == user_id).first()

    def create(self, user_data):
        user = User(**user_data)
        self.db.add(user)
        self.db.commit()
        return user
```

## When to Use This Skill

- Building web APIs and services
- Developing microservices
- Creating GraphQL endpoints
- Database design and optimization
- System architecture planning
- Deploying applications
- Performance optimization
- Team backend training

## Related Agents

- **Frontend Agent** - Full-stack integration
- **Database Agent** - Advanced data modeling
- **Infrastructure Agent** - Deployment and scaling
- **Data Science Agent** - ML model serving

## Resources

**Official Documentation:**
- Express: https://expressjs.com
- FastAPI: https://fastapi.tiangolo.com
- Spring Boot: https://spring.io/projects/spring-boot
- Go: https://golang.org

**Books:**
- *Building Microservices* (Sam Newman)
- *Designing Data-Intensive Applications* (Martin Kleppmann)
- *RESTful Web Services* (Leonard Richardson)

**Courses:**
- Udemy Backend Courses
- Pluralsight
- Linux Academy
- A Cloud Guru

---

**Status:** Comprehensive backend skill covering 10 roles and 1,073+ topics
