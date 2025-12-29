---
name: infrastructure
description: Master cloud infrastructure, Kubernetes, Terraform, CI/CD, and DevOps. Learn containerization, infrastructure as code, cloud platforms (AWS, GCP, Azure), system design, and security hardening. Use when building infrastructure, deploying applications, or implementing DevOps.
sasmp_version: "1.3.0"
bonded_agent: 01-frontend-development
bond_type: PRIMARY_BOND
---

# Infrastructure & DevOps Skill

## Quick Start

Build scalable, reliable cloud infrastructure with modern DevOps practices.

### Core Path: Linux → Docker → Kubernetes → Cloud

```dockerfile
# Dockerfile Multi-stage Build
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
EXPOSE 3000
CMD ["node", "index.js"]
```

## What You'll Learn

### Foundation Level (Weeks 1-12)
- **Linux Fundamentals** - Command line, permissions, processes, networking
- **Version Control** - Git workflows, branching strategies
- **Containerization** - Docker basics, image creation, container management
- **Scripting** - Bash/shell scripting for automation

### Intermediate Level (Weeks 13-32)
- **Orchestration:** Kubernetes basics, deployments, services, config management
- **Infrastructure as Code:** Terraform modules, state management
- **CI/CD Pipelines:** GitHub Actions, GitLab CI, Jenkins
- **Cloud Platforms:** AWS (EC2, S3, RDS), GCP, Azure basics
- **Monitoring:** Prometheus, Grafana, ELK Stack

### Advanced Level (Weeks 33-52+)
- **Kubernetes Advanced:** Operators, Helm, networking, security
- **Multi-Cloud:** AWS, GCP, Azure mastery
- **Security:** IAM, encryption, secrets management, compliance
- **Performance:** Optimization, auto-scaling, cost management
- **SRE Practices:** Incident management, observability, reliability

## Key Technologies

**Containerization:**
- Docker (build, run, compose, registry)
- Container security (image scanning, runtime)
- Docker Swarm basics

**Orchestration:**
- Kubernetes (core concepts, workloads, networking)
- Helm charts and package management
- Operators and custom resources
- Service mesh (Istio, Linkerd basics)

**Infrastructure as Code:**
- Terraform (HCL, modules, backends)
- Ansible (playbooks, roles, idempotency)
- CloudFormation (AWS), Bicep (Azure)
- Pulumi (Python/TypeScript IaC)

**Cloud Platforms (100+ services covered):**
- **AWS:** EC2, S3, RDS, Lambda, ECS, EKS, CloudFront, IAM
- **GCP:** Compute Engine, GKE, Cloud Storage, BigQuery
- **Azure:** VMs, AKS, Azure SQL, ExpressRoute
- **Cloudflare:** DNS, CDN, Workers, R2 Storage

**CI/CD:**
- GitHub Actions, GitLab CI, Jenkins
- Docker integration, artifact management
- Deployment automation, rollback strategies

**Monitoring & Logging:**
- Prometheus (metrics), Grafana (dashboards)
- ELK Stack (Elasticsearch, Logstash, Kibana)
- CloudWatch (AWS), Stackdriver (GCP)
- Jaeger (distributed tracing)

**Security:**
- IAM and RBAC
- TLS/SSL certificates
- HashiCorp Vault
- Security scanning tools

## Architecture Patterns

```hcl
# Terraform EKS Cluster Example
resource "aws_eks_cluster" "main" {
  name    = "my-cluster"
  version = "1.28"

  vpc_config {
    subnet_ids = aws_subnet.private[*].id
  }

  depends_on = [aws_iam_role_policy_attachment.eks-service]
}

resource "aws_eks_node_group" "main" {
  cluster_name    = aws_eks_cluster.main.name
  node_group_name = "main"
  node_role_arn   = aws_iam_role.eks_node.arn
  subnet_ids      = aws_subnet.private[*].id

  scaling_config {
    desired_size = 3
    max_size     = 10
    min_size     = 1
  }
}
```

## Learning Outcomes

After completing this skill:

✅ Containerize applications with Docker
✅ Orchestrate containers with Kubernetes
✅ Write Infrastructure as Code with Terraform
✅ Build CI/CD pipelines
✅ Deploy to cloud platforms (AWS, GCP, Azure)
✅ Monitor and secure infrastructure
✅ Implement disaster recovery
✅ Optimize costs
✅ Handle incident response
✅ Lead infrastructure projects

## Project Examples

1. **Kubernetes Deployment** - Multi-service architecture
2. **Terraform AWS Setup** - VPC, EC2, RDS, auto-scaling
3. **CI/CD Pipeline** - Build, test, deploy automation
4. **Microservices** - Multiple services on Kubernetes
5. **Disaster Recovery** - Backup, replication, failover
6. **Multi-Region Deployment** - Global infrastructure
7. **Security Hardening** - Container security, IAM, encryption

## Deployment Strategies

```yaml
# Blue-Green Deployment with Kubernetes
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app-blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
      version: blue
  template:
    metadata:
      labels:
        app: myapp
        version: blue
    spec:
      containers:
      - name: app
        image: myapp:1.0
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: app-service
spec:
  selector:
    app: myapp
    version: blue  # Switch to "green" for deployment
  ports:
  - port: 80
    targetPort: 8080
```

## When to Use This Skill

- Setting up Kubernetes clusters
- Building CI/CD pipelines
- Cloud migration projects
- Infrastructure automation
- Scaling applications
- Container security
- Disaster recovery planning
- Cost optimization
- Team DevOps training

## Related Agents

- **Backend Agent** - Application deployment
- **Data Science Agent** - ML infrastructure
- **Database Agent** - Data storage solutions

## Learning Paths

**Path 1:** Linux → Docker → Kubernetes (12-18 months)
**Path 2:** Cloud Fundamentals → Terraform → AWS/GCP (12-18 months)
**Path 3:** SRE Focus (18-24 months)

## Resources

**Official Docs:**
- Docker: https://docs.docker.com
- Kubernetes: https://kubernetes.io/docs
- Terraform: https://www.terraform.io/docs
- AWS: https://docs.aws.amazon.com

**Books:**
- *The Kubernetes Book* (Nigel Poulton)
- *Terraform Up and Running* (Yevgeniy Brikman)
- *The Phoenix Project* (Gene Kim)
- *Site Reliability Engineering* (Google)

**Courses:**
- Linux Academy (A Cloud Guru)
- Kubernetes the Hard Way
- Certified Kubernetes Administrator (CKA)
- AWS Solutions Architect Associate

---

**Status:** Comprehensive infrastructure skill covering 5 roles and 100+ tools
