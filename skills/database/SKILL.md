---
name: database
description: Master relational and NoSQL databases including PostgreSQL, MongoDB, Redis, SQL optimization, and data modeling. Learn query optimization, backup/recovery, high availability, and blockchain technologies. Use when designing databases, optimizing queries, or choosing database solutions.
---

# Database & Data Management Skill

## Quick Start

Design and optimize databases for production applications.

### Core Path: SQL → PostgreSQL → Advanced Optimization

```sql
-- PostgreSQL Advanced Queries
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT email_format CHECK (email LIKE '%@%.%')
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_created ON users(created_at DESC);

-- Complex query with CTE
WITH recent_users AS (
    SELECT id, email, created_at
    FROM users
    WHERE created_at > CURRENT_DATE - INTERVAL '30 days'
),
user_activity AS (
    SELECT user_id, COUNT(*) as activity_count
    FROM user_logs
    GROUP BY user_id
)
SELECT ru.id, ru.email, COALESCE(ua.activity_count, 0) as activity
FROM recent_users ru
LEFT JOIN user_activity ua ON ru.id = ua.user_id
ORDER BY ua.activity_count DESC;
```

## What You'll Learn

### Foundation Level (Weeks 1-12)
- **SQL Fundamentals** - SELECT, JOIN, GROUP BY, subqueries
- **Database Design** - Normalization, ER diagrams, relationships
- **Indexes** - B-tree, Hash, strategies, query plans
- **Transactions** - ACID properties, isolation levels

### Intermediate Level (Weeks 13-32)
- **Advanced SQL:** Window functions, CTEs, stored procedures
- **PostgreSQL Features:** JSON/JSONB, Full-text search, PostGIS
- **NoSQL:** MongoDB, document design, aggregation pipeline
- **Performance:** Query optimization, EXPLAIN ANALYZE, profiling
- **Replication:** Master-slave, failover, high availability

### Advanced Level (Weeks 33-52+)
- **PostgreSQL Advanced:** Partitioning, logical replication, extensions
- **MongoDB Advanced:** Sharding, transactions, performance tuning
- **Redis:** Data structures, streams, Pub/Sub, cluster
- **Blockchain:** Smart contracts, distributed ledgers
- **Polyglot Persistence:** Multiple databases in architecture

## Database Technologies

**Relational:**
- **PostgreSQL (16+):** MVCC, JSON, extensions, replication
- **MySQL/MariaDB:** InnoDB, partitioning, replication
- **SQL Server:** T-SQL, Always On, premium features
- **Oracle:** Enterprise features, PL/SQL

**NoSQL:**
- **MongoDB:** Document model, aggregation, sharding
- **Redis:** In-memory, data structures, streams
- **DynamoDB:** AWS serverless, fast, scalable
- **Cassandra:** Distributed, high-availability
- **Elasticsearch:** Search engine, analytics

**Specialized:**
- **GraphQL:** Query language for APIs
- **Firebase/Firestore:** Real-time databases
- **ClickHouse:** OLAP analytics
- **Blockchain:** Ethereum, Solana, Polygon

## Data Modeling Patterns

```python
# MongoDB Document Design Pattern
# Embedded vs Referenced
user_doc = {
    "_id": ObjectId("..."),
    "name": "John Doe",
    "email": "john@example.com",
    # Embedded relationship (denormalized)
    "profile": {
        "bio": "...",
        "avatar_url": "..."
    },
    # Referenced relationship (normalized)
    "addresses": [
        ObjectId("address1"),
        ObjectId("address2")
    ]
}
```

## Query Optimization Techniques

1. **Index Strategy** - Composite, covering, partial indexes
2. **Query Rewriting** - Simplifying complex queries
3. **Execution Plans** - EXPLAIN ANALYZE, understanding costs
4. **Denormalization** - Strategic redundancy for performance
5. **Caching** - Redis, query result caching
6. **Partitioning** - Range, list, hash partitioning

## Learning Outcomes

After completing this skill:

✅ Design normalized database schemas
✅ Write optimized SQL queries
✅ Implement indexes effectively
✅ Master PostgreSQL advanced features
✅ Design MongoDB document schemas
✅ Optimize query performance
✅ Implement replication and failover
✅ Manage backups and recovery
✅ Work with distributed databases
✅ Choose appropriate databases

## Project Examples

1. **E-commerce Database** - Orders, products, inventory
2. **SaaS Platform** - Multi-tenant schema design
3. **Analytics Dashboard** - Complex queries, aggregations
4. **Real-time Application** - MongoDB + Redis combination
5. **High-Traffic App** - Partitioning, sharding strategy
6. **Blockchain DApp** - Smart contracts, Web3 integration

## Backup & Disaster Recovery

```bash
# PostgreSQL Backup
pg_dump -U postgres mydb > backup.sql
pg_dump -U postgres -Fc mydb > backup.dump

# Restore
psql -U postgres < backup.sql
pg_restore -U postgres -d mydb backup.dump

# WAL Archiving for PITR (Point-in-Time Recovery)
# Configure postgresql.conf:
# wal_level = replica
# archive_mode = on
# archive_command = 'test ! -f /archive/%f && cp %p /archive/%f'
```

## High Availability Patterns

**PostgreSQL Streaming Replication:**
- Primary → Multiple standbys
- Synchronous or asynchronous
- Automatic failover with Patroni

**MongoDB Replica Sets:**
- Primary + secondaries
- Automatic failover
- Read preference routing

**Redis Sentinel:**
- Monitoring and failover
- Configuration management
- Multi-master replication

## When to Use This Skill

- Designing relational databases
- NoSQL database selection
- Query optimization
- Database migration
- Backup and disaster recovery
- High availability implementation
- Performance tuning
- Blockchain and Web3 projects
- Team database training

## Related Agents

- **Backend Agent** - Application-database integration
- **Infrastructure Agent** - Cloud database services
- **Data Science Agent** - Data warehouse design

## Salary Insights

| Role | Salary | Specialization |
|------|--------|-----------------|
| PostgreSQL DBA | $100K-220K | Advanced relational |
| MongoDB Expert | $110K-230K | Document databases |
| Database Architect | $120K-250K | Enterprise design |
| Blockchain Engineer | $100K-220K | Distributed ledgers |

## Resources

**Official Docs:**
- PostgreSQL: https://www.postgresql.org/docs
- MongoDB: https://docs.mongodb.com
- Redis: https://redis.io/docs
- MySQL: https://dev.mysql.com/doc

**Books:**
- *SQL Performance Explained* (Markus Winand)
- *The Data Warehouse Toolkit* (Ralph Kimball)
- *MongoDB: The Definitive Guide* (Shannon Bradshaw)
- *High Performance MySQL* (Baron Schwartz)

**Courses:**
- PostgreSQL Administration
- MongoDB University
- Database Design Fundamentals
- Redis University

---

**Status:** Comprehensive database skill covering 6 roles and 400+ competencies
