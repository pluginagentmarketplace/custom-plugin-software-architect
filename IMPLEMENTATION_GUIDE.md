# Infrastructure & DevOps Implementation Guide

## Quick Reference Structure

### 1. Docker Implementation

#### Dockerfile Best Practices
```dockerfile
# Multi-stage build example
FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:16-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
USER node
EXPOSE 3000
CMD ["node", "index.js"]
```

**Key Practices:**
- Use minimal base images (Alpine, Distroless)
- Leverage multi-stage builds to reduce final image size
- Use specific version tags (never `latest`)
- Run as non-root user
- Minimize layers by combining RUN commands
- Order Dockerfile commands for optimal caching

#### Docker Image Scanning
```bash
# Trivy scanning
trivy image --severity HIGH,CRITICAL myapp:v1.0

# Clair scanning
clair-scanner myapp:v1.0

# Snyk scanning
snyk container test myapp:v1.0
```

**Security Scanning Focus:**
- Check for known vulnerabilities (CVEs)
- Verify base image security
- Scan before pushing to registry
- Integrate into CI/CD pipeline
- Enforce compliance policies

---

### 2. Kubernetes Implementation

#### Deployment Best Practices
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: app
  namespace: production
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
        version: v1
    spec:
      securityContext:
        runAsNonRoot: true
        runAsUser: 1000
      affinity:
        podAntiAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
            - weight: 100
              podAffinityTerm:
                labelSelector:
                  matchExpressions:
                    - key: app
                      operator: In
                      values:
                        - myapp
                topologyKey: kubernetes.io/hostname
      containers:
        - name: app
          image: myregistry.azurecr.io/myapp:v1.0
          imagePullPolicy: IfNotPresent
          ports:
            - name: http
              containerPort: 3000
              protocol: TCP
          env:
            - name: LOG_LEVEL
              value: "info"
            - name: DB_HOST
              valueFrom:
                configMapKeyRef:
                  name: app-config
                  key: db.host
            - name: DB_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: app-secrets
                  key: db.password
          resources:
            requests:
              cpu: 100m
              memory: 128Mi
            limits:
              cpu: 500m
              memory: 512Mi
          livenessProbe:
            httpGet:
              path: /health
              port: 3000
            initialDelaySeconds: 30
            periodSeconds: 10
            failureThreshold: 3
          readinessProbe:
            httpGet:
              path: /ready
              port: 3000
            initialDelaySeconds: 5
            periodSeconds: 5
          securityContext:
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
            capabilities:
              drop:
                - ALL
          volumeMounts:
            - name: tmp
              mountPath: /tmp
            - name: config
              mountPath: /etc/config
              readOnly: true
      volumes:
        - name: tmp
          emptyDir: {}
        - name: config
          configMap:
            name: app-config
      imagePullSecrets:
        - name: registry-credentials
```

**Critical Points:**
- Resource requests and limits
- Liveness and readiness probes
- Pod disruption budgets for reliability
- Network policies for security
- RBAC for access control

#### Network Policies
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: app-network-policy
  namespace: production
spec:
  podSelector:
    matchLabels:
      app: myapp
  policyTypes:
    - Ingress
    - Egress
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              name: ingress-nginx
        - podSelector:
            matchLabels:
              app: api-gateway
      ports:
        - protocol: TCP
          port: 3000
  egress:
    - to:
        - namespaceSelector: {}
      ports:
        - protocol: TCP
          port: 5432  # Database
        - protocol: TCP
          port: 443   # HTTPS
    - to:
        - podSelector:
            matchLabels:
              k8s-app: kube-dns
      ports:
        - protocol: UDP
          port: 53    # DNS
```

#### RBAC Configuration
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  name: app-sa
  namespace: production

---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: app-role
  namespace: production
rules:
  - apiGroups: [""]
    resources: ["configmaps"]
    verbs: ["get", "list", "watch"]
  - apiGroups: [""]
    resources: ["secrets"]
    verbs: ["get"]
    resourceNames: ["app-secrets"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: app-rolebinding
  namespace: production
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: app-role
subjects:
  - kind: ServiceAccount
    name: app-sa
    namespace: production
```

---

### 3. Terraform Implementation

#### Module Structure
```
terraform/
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── terraform.tfvars
│   │   └── outputs.tf
│   └── prod/
│       ├── main.tf
│       ├── terraform.tfvars
│       └── outputs.tf
├── modules/
│   ├── networking/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   ├── outputs.tf
│   │   └── security_groups.tf
│   ├── compute/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── database/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
└── global/
    ├── main.tf
    ├── variables.tf
    └── outputs.tf
```

#### Example: Kubernetes Cluster Module
```hcl
# modules/kubernetes/main.tf

terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
    kubernetes = {
      source  = "hashicorp/kubernetes"
      version = "~> 2.20"
    }
  }
}

locals {
  cluster_name = "${var.environment}-${var.cluster_name}"
}

# EKS Cluster
resource "aws_eks_cluster" "main" {
  name     = local.cluster_name
  role_arn = aws_iam_role.cluster.arn
  version  = var.kubernetes_version

  vpc_config {
    subnet_ids              = var.subnet_ids
    endpoint_private_access = true
    endpoint_public_access  = var.endpoint_public_access
    public_access_cidrs     = var.public_access_cidrs
  }

  enabled_cluster_log_types = ["api", "audit", "authenticator", "controllerManager", "scheduler"]

  tags = merge(var.tags, {
    Name = local.cluster_name
  })

  depends_on = [aws_iam_role_policy_attachment.cluster_policy]
}

# Node Group
resource "aws_eks_node_group" "main" {
  cluster_name    = aws_eks_cluster.main.name
  node_group_name = "${local.cluster_name}-nodes"
  node_role_arn   = aws_iam_role.node.arn
  subnet_ids      = var.subnet_ids

  scaling_config {
    desired_size = var.desired_size
    max_size     = var.max_size
    min_size     = var.min_size
  }

  instance_types = var.instance_types

  tags = merge(var.tags, {
    Name = "${local.cluster_name}-nodes"
  })

  depends_on = [
    aws_iam_role_policy_attachment.node_policy,
    aws_iam_role_policy_attachment.cni_policy
  ]
}

# State management
terraform {
  backend "s3" {
    bucket         = "terraform-state-bucket"
    key            = "kubernetes/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}
```

#### Variables and Outputs
```hcl
# modules/kubernetes/variables.tf

variable "environment" {
  description = "Environment name"
  type        = string
}

variable "cluster_name" {
  description = "EKS cluster name"
  type        = string
}

variable "kubernetes_version" {
  description = "Kubernetes version"
  type        = string
  default     = "1.27"
}

variable "instance_types" {
  description = "EC2 instance types for nodes"
  type        = list(string)
  default     = ["t3.medium"]
}

variable "desired_size" {
  description = "Desired number of nodes"
  type        = number
}

variable "min_size" {
  description = "Minimum number of nodes"
  type        = number
}

variable "max_size" {
  description = "Maximum number of nodes"
  type        = number
}

variable "subnet_ids" {
  description = "Subnet IDs for the cluster"
  type        = list(string)
}

variable "tags" {
  description = "Tags to apply to resources"
  type        = map(string)
  default     = {}
}

# modules/kubernetes/outputs.tf

output "cluster_id" {
  value = aws_eks_cluster.main.id
}

output "cluster_arn" {
  value = aws_eks_cluster.main.arn
}

output "cluster_endpoint" {
  value = aws_eks_cluster.main.endpoint
}

output "cluster_security_group_id" {
  value = aws_eks_cluster.main.vpc_config[0].cluster_security_group_id
}

output "node_group_id" {
  value = aws_eks_node_group.main.id
}
```

---

### 4. Ansible Implementation

#### Playbook Structure
```yaml
# roles/web_server/tasks/main.yml
---
- name: Update system packages
  yum:
    name: "*"
    state: latest
  when: ansible_os_family == "RedHat"

- name: Install required packages
  package:
    name:
      - nginx
      - curl
      - git
    state: present

- name: Start and enable Nginx
  systemd:
    name: nginx
    state: started
    enabled: yes

- name: Deploy application
  git:
    repo: "{{ git_repo_url }}"
    dest: "/var/www/app"
    version: "{{ app_version }}"
    update: yes

- name: Copy Nginx configuration
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/sites-available/app
    owner: root
    group: root
    mode: '0644'
  notify: Reload Nginx

- name: Enable Nginx site
  file:
    src: /etc/nginx/sites-available/app
    dest: /etc/nginx/sites-enabled/app
    state: link

- name: Create application user
  user:
    name: appuser
    shell: /bin/bash
    home: /var/www/app
    createhome: yes

- name: Set permissions
  file:
    path: /var/www/app
    owner: appuser
    group: appuser
    recurse: yes
```

#### Handler Definition
```yaml
# roles/web_server/handlers/main.yml
---
- name: Reload Nginx
  systemd:
    name: nginx
    state: reloaded

- name: Restart application
  systemd:
    name: app
    state: restarted
```

#### Playbook Execution
```yaml
# site.yml
---
- name: Configure web servers
  hosts: webservers
  become: yes
  vars:
    git_repo_url: "https://github.com/myorg/app.git"
    app_version: "v1.0.0"
  roles:
    - common
    - web_server
    - monitoring

- name: Configure databases
  hosts: databases
  become: yes
  roles:
    - database
    - backup
```

---

### 5. Linux System Administration

#### User and Group Management
```bash
# Create user with home directory
useradd -m -s /bin/bash -d /home/newuser newuser

# Set password
passwd newuser

# Add user to sudoers
usermod -aG sudo newuser

# Create group
groupadd developers

# Add user to group
usermod -aG developers newuser

# Configure sudoers for specific commands
visudo
# Add: newuser ALL=(ALL) NOPASSWD: /usr/bin/systemctl restart nginx
```

#### Service Management
```bash
# Check service status
systemctl status nginx

# Start/stop/restart services
systemctl start nginx
systemctl stop nginx
systemctl restart nginx

# Enable service on boot
systemctl enable nginx

# View service logs
journalctl -u nginx -f

# Check failed services
systemctl list-units --failed
```

#### Firewall Configuration
```bash
# Enable UFW
ufw enable

# Allow SSH
ufw allow 22/tcp

# Allow HTTP/HTTPS
ufw allow 80/tcp
ufw allow 443/tcp

# Block specific IP
ufw deny from 192.168.1.100

# View rules
ufw status numbered

# Delete rule
ufw delete allow 80/tcp
```

#### Storage Management
```bash
# List disks
lsblk
fdisk -l

# Create partition
fdisk /dev/sdb
# n = new partition
# p = primary
# w = write

# Format filesystem
mkfs.ext4 /dev/sdb1

# Mount filesystem
mount /dev/sdb1 /mnt/storage

# Persistent mount (fstab)
echo "/dev/sdb1 /mnt/storage ext4 defaults 0 2" >> /etc/fstab

# Check disk usage
df -h
du -sh /var/*
```

---

### 6. Cloud Security Implementation

#### AWS IAM Policy Example
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowEC2ReadOnly",
      "Effect": "Allow",
      "Action": [
        "ec2:Describe*",
        "ec2:Get*",
        "ec2:List*"
      ],
      "Resource": "*"
    },
    {
      "Sid": "AllowS3Access",
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::my-bucket/*",
      "Condition": {
        "StringEquals": {
          "aws:PrincipalOrgID": "o-xxxxxxxxxx"
        }
      }
    },
    {
      "Sid": "DenyUnencryptedObjectUploads",
      "Effect": "Deny",
      "Action": "s3:PutObject",
      "Resource": "arn:aws:s3:::my-bucket/*",
      "Condition": {
        "StringNotEquals": {
          "s3:x-amz-server-side-encryption": "AES256"
        }
      }
    }
  ]
}
```

#### Kubernetes RBAC Example
```yaml
# Role for application developers
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: development
  name: app-developer
rules:
  - apiGroups: ["apps"]
    resources: ["deployments", "statefulsets"]
    verbs: ["get", "list", "watch", "patch", "update"]
  - apiGroups: [""]
    resources: ["pods", "pods/logs"]
    verbs: ["get", "list", "watch"]
  - apiGroups: [""]
    resources: ["configmaps"]
    verbs: ["get", "list", "create", "patch"]
  - apiGroups: [""]
    resources: ["secrets"]
    verbs: ["get"]
    resourceNames: ["app-secrets"]

---
# Bind role to user
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  namespace: development
  name: app-developer-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: Role
  name: app-developer
subjects:
  - kind: User
    name: "dev@company.com"
    apiGroup: rbac.authorization.k8s.io
```

---

### 7. Monitoring and Logging Implementation

#### Prometheus Configuration
```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s
  external_labels:
    cluster: production
    environment: prod

alerting:
  alertmanagers:
    - static_configs:
        - targets:
            - alertmanager:9093

rule_files:
  - "/etc/prometheus/rules/*.yml"

scrape_configs:
  - job_name: "prometheus"
    static_configs:
      - targets: ["localhost:9090"]

  - job_name: "kubernetes"
    kubernetes_sd_configs:
      - role: pod
    relabel_configs:
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
        action: keep
        regex: true
      - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
        action: replace
        target_label: __metrics_path__
        regex: (.+)
      - source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
        action: replace
        regex: ([^:]+)(?::\d+)?;(\d+)
        replacement: $1:$2
        target_label: __address__

  - job_name: "application"
    metrics_path: "/metrics"
    static_configs:
      - targets: ["localhost:8080"]
```

#### Prometheus Alert Rules
```yaml
groups:
  - name: application
    interval: 30s
    rules:
      - alert: HighErrorRate
        expr: |
          (
            sum(rate(http_requests_total{status=~"5.."}[5m]))
            /
            sum(rate(http_requests_total[5m]))
          ) > 0.05
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value | humanizePercentage }}"

      - alert: PodCrashLooping
        expr: rate(kube_pod_container_status_restarts_total[15m]) > 0.1
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Pod is crash looping"
          description: "Pod {{ $labels.pod }} in {{ $labels.namespace }} is crash looping"

      - alert: HighMemoryUsage
        expr: |
          (
            container_memory_usage_bytes
            /
            container_spec_memory_limit_bytes
          ) > 0.9
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High memory usage"
          description: "Memory usage is {{ $value | humanizePercentage }}"
```

#### ELK Stack Setup
```yaml
# docker-compose.yml for ELK
version: '3.8'
services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.0.0
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
    volumes:
      - es_data:/usr/share/elasticsearch/data
    ports:
      - "9200:9200"

  kibana:
    image: docker.elastic.co/kibana/kibana:8.0.0
    ports:
      - "5601:5601"
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200

  logstash:
    image: docker.elastic.co/logstash/logstash:8.0.0
    volumes:
      - ./logstash.conf:/usr/share/logstash/pipeline/logstash.conf
    ports:
      - "5000:5000"
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200

volumes:
  es_data:
```

---

### 8. CI/CD Pipeline Implementation

#### GitHub Actions Example
```yaml
# .github/workflows/deploy.yml
name: Deploy Application

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

env:
  REGISTRY: ghcr.io
  IMAGE_NAME: ${{ github.repository }}

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.9'
      
      - name: Install dependencies
        run: |
          pip install -r requirements.txt
          pip install pytest pytest-cov
      
      - name: Run tests
        run: pytest --cov=app tests/

  security:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Run Trivy scan
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          scan-ref: '.'
          format: 'sarif'
          output: 'trivy-results.sarif'
      
      - name: Upload Trivy results
        uses: github/codeql-action/upload-sarif@v2
        with:
          sarif_file: 'trivy-results.sarif'

  build:
    needs: [test, security]
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v2
      
      - name: Log in to Container Registry
        uses: docker/login-action@v2
        with:
          registry: ${{ env.REGISTRY }}
          username: ${{ github.actor }}
          password: ${{ secrets.GITHUB_TOKEN }}
      
      - name: Build and push Docker image
        uses: docker/build-push-action@v4
        with:
          context: .
          push: true
          tags: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }}
          cache-from: type=gha
          cache-to: type=gha,mode=max

  deploy:
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v3
      
      - name: Deploy to production
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
          DEPLOY_HOST: ${{ secrets.DEPLOY_HOST }}
        run: |
          mkdir -p ~/.ssh
          echo "$DEPLOY_KEY" > ~/.ssh/deploy_key
          chmod 600 ~/.ssh/deploy_key
          ssh-keyscan -H $DEPLOY_HOST >> ~/.ssh/known_hosts
          ssh -i ~/.ssh/deploy_key deployer@$DEPLOY_HOST "cd /app && docker pull ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}:${{ github.sha }} && docker-compose up -d"
```

#### GitLab CI Example
```yaml
# .gitlab-ci.yml
stages:
  - test
  - build
  - deploy

variables:
  DOCKER_DRIVER: overlay2
  DOCKER_TLS_CERTDIR: "/certs"

test:
  stage: test
  image: python:3.9
  script:
    - pip install -r requirements.txt
    - pytest --cov=app tests/
  coverage: '/TOTAL.+ ([0-9]+%)$/'

security:
  stage: test
  image: aquasec/trivy:latest
  script:
    - trivy fs --exit-code 0 --severity HIGH,CRITICAL .

build:
  stage: build
  image: docker:latest
  services:
    - docker:dind
  script:
    - docker build -t $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA .
    - docker login -u $CI_REGISTRY_USER -p $CI_REGISTRY_PASSWORD $CI_REGISTRY
    - docker push $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA
    - docker tag $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA $CI_REGISTRY_IMAGE:latest
    - docker push $CI_REGISTRY_IMAGE:latest

deploy_staging:
  stage: deploy
  image: alpine:latest
  script:
    - apk add --no-cache openssh-client
    - mkdir -p ~/.ssh
    - echo "$DEPLOY_KEY" > ~/.ssh/deploy_key
    - chmod 600 ~/.ssh/deploy_key
    - ssh-keyscan -H $STAGING_HOST >> ~/.ssh/known_hosts
    - ssh -i ~/.ssh/deploy_key deployer@$STAGING_HOST "docker pull $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA && docker-compose up -d"
  environment:
    name: staging
    url: https://staging.example.com
  only:
    - main

deploy_production:
  stage: deploy
  image: alpine:latest
  script:
    - apk add --no-cache openssh-client
    - mkdir -p ~/.ssh
    - echo "$DEPLOY_KEY" > ~/.ssh/deploy_key
    - chmod 600 ~/.ssh/deploy_key
    - ssh-keyscan -H $PROD_HOST >> ~/.ssh/known_hosts
    - ssh -i ~/.ssh/deploy_key deployer@$PROD_HOST "docker pull $CI_REGISTRY_IMAGE:$CI_COMMIT_SHA && docker-compose up -d"
  environment:
    name: production
    url: https://example.com
  only:
    - tags
  when: manual
```

---

## Technology-Specific Security Practices

### Docker Security
1. Scan images before deployment
2. Use specific base image versions
3. Run containers as non-root
4. Implement resource limits
5. Use read-only root filesystems where possible
6. Sign images for integrity verification
7. Minimize attack surface with minimal images

### Kubernetes Security
1. Enable RBAC for access control
2. Use network policies for traffic control
3. Implement pod security policies
4. Use secrets for sensitive data
5. Enable audit logging
6. Implement admission controllers
7. Use security contexts for pod isolation

### Terraform Security
1. Use remote state with encryption and locking
2. Avoid hardcoding secrets (use Vault, SSM, Secrets Manager)
3. Implement policy-as-code (Sentinel, OPA)
4. Use module versioning
5. Review all infrastructure changes
6. Rotate service account keys regularly
7. Use separate states for environments

### Linux Security
1. Harden base systems (disable unnecessary services)
2. Implement firewall rules
3. Use SELinux or AppArmor
4. Regular patching and updates
5. Implement AIDE for file integrity monitoring
6. Use strong authentication (SSH keys, MFA)
7. Monitor and audit system activities

### AWS Security
1. Enable MFA for root account
2. Use least privilege IAM policies
3. Enable VPC Flow Logs
4. Use KMS for encryption
5. Enable CloudTrail for audit logging
6. Use Security Groups and NACLs
7. Enable GuardDuty for threat detection

### GCP Security
1. Use Cloud IAM for access control
2. Enable Cloud Audit Logs
3. Use Cloud KMS for encryption
4. Implement VPC Service Controls
5. Enable Cloud Armor for DDoS protection
6. Use Workload Identity for service authentication
7. Enable Security Command Center

### Azure Security
1. Use Role-Based Access Control (RBAC)
2. Enable Azure Policy for governance
3. Use Key Vault for secrets
4. Enable Azure Defender
5. Use Network Security Groups
6. Enable diagnostic logging
7. Implement Azure Firewall

---

## Common Implementation Patterns

### Blue-Green Deployment
```yaml
# Create green environment
kubectl create deployment myapp-green --image=myapp:v2 -n production

# Wait for green to be ready
kubectl wait --for=condition=available --timeout=300s deployment/myapp-green -n production

# Switch traffic to green
kubectl patch service myapp -p '{"spec":{"selector":{"version":"green"}}}'

# Verify green is working
# If failed, switch back
kubectl patch service myapp -p '{"spec":{"selector":{"version":"blue"}}}'

# Clean up old blue deployment
kubectl delete deployment myapp-blue -n production
```

### Canary Deployment
```yaml
# Initial deployment with Istio
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: myapp
spec:
  hosts:
    - myapp
  http:
    - match:
        - uri:
            prefix: "/"
      route:
        - destination:
            host: myapp
            subset: v1
          weight: 90
        - destination:
            host: myapp
            subset: v2
          weight: 10

---
# Gradually increase traffic to v2
# Increase weights: 80-20, 70-30, 50-50, 0-100
# Complete cutover when stable
```

### Infrastructure Drift Detection
```bash
#!/bin/bash
# Check Terraform drift
terraform plan -out=tfplan

# Parse and report changes
terraform show -json tfplan | jq '.resource_changes[] | select(.change.actions[0] != "no-op")'

# Detect manual changes
aws ec2 describe-instances --query 'Reservations[*].Instances[*].[InstanceId,State.Name,Tags[?Key==`Name`].Value[0]]' -o table
```

---

## Disaster Recovery Patterns

### RTO/RPO Planning
- **RTO (Recovery Time Objective)**: Maximum acceptable downtime
- **RPO (Recovery Point Objective)**: Maximum acceptable data loss

**Example for Critical Service:**
- RTO: 1 hour
- RPO: 15 minutes
- Requires: Multi-region replication, automated failover

### Backup Strategy
```bash
#!/bin/bash
# Daily incremental backups
0 2 * * * /usr/local/bin/backup-database.sh > /var/log/backup.log

# Weekly full backups
0 3 * * 0 /usr/local/bin/backup-full.sh > /var/log/backup-full.log

# Monthly offsite backups
0 4 1 * * /usr/local/bin/backup-offsite.sh > /var/log/backup-offsite.log

# Verify backups
0 5 * * * /usr/local/bin/verify-backup.sh > /var/log/verify.log
```

---

## Cost Optimization Techniques

1. **Right-sizing**: Match instance types to actual needs
2. **Spot Instances**: Use for non-critical, fault-tolerant workloads (up to 70% savings)
3. **Reserved Instances**: Commit to 1-3 year terms (up to 60% savings)
4. **Savings Plans**: Flexible commitment across services
5. **Auto-scaling**: Scale based on demand
6. **Storage Optimization**: Archive old data, use tiered storage
7. **Data Transfer**: Minimize cross-region transfer

---

## Performance Optimization

1. **Caching**: Implement multi-level caching
2. **CDN**: Distribute content globally
3. **Database**: Index optimization, connection pooling
4. **Application**: Code profiling, async operations
5. **Infrastructure**: Right-sizing, load balancing
6. **Network**: Protocol selection (HTTP/2, gRPC), compression

