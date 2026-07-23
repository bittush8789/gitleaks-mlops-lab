# Gitleaks Production-Level Hands-On Practice Project (MLOps)

## Objective

Learn how to secure an MLOps project by detecting hardcoded secrets using **Gitleaks**.

In this hands-on project, you'll build a production-ready DevSecOps workflow to scan:

- Git Repository
- Git Commit History
- Source Code
- Environment Files
- Python Files
- Dockerfiles
- Kubernetes Manifests
- YAML Files
- Configuration Files

This project demonstrates how Gitleaks is integrated into enterprise MLOps and CI/CD pipelines to prevent secrets from being committed to Git repositories.

---

# Tech Stack

- Ubuntu
- Git
- GitHub
- Python
- FastAPI
- Docker
- Kubernetes
- Gitleaks
- YAML
- Bash

---

# Production Architecture

```text
Developer
     │
     ▼
Git Repository
     │
     ▼
Gitleaks Scan
     │
     ├── Source Code
     ├── Git History
     ├── Environment Files
     ├── YAML Files
     ├── Dockerfile
     ├── Kubernetes Manifests
     └── Configuration Files
     │
     ▼
Secret Detection Report
     │
     ▼
GitHub Actions
     │
     ▼
Docker Build
     │
     ▼
Container Registry
     │
     ▼
Kubernetes
```

---

# Project Structure

```text
gitleaks-mlops-lab/
│
├── app/
│   ├── app.py
│   ├── config.py
│   ├── requirements.txt
│   └── .env
│
├── kubernetes/
│   ├── deployment.yaml
│   └── service.yaml
│
├── Dockerfile
├── docker-compose.yml
├── .gitleaks.toml
├── README.md
└── .gitignore
```

---

# Step 1: Install Git

```bash
sudo apt update

sudo apt install git -y

git --version
```

---

# Step 2: Install Gitleaks

```bash
wget https://github.com/gitleaks/gitleaks/releases/latest/download/gitleaks_linux_x64.tar.gz

tar -xzf gitleaks_linux_x64.tar.gz

sudo mv gitleaks /usr/local/bin/
```

Verify

```bash
gitleaks version
```

---

# Step 3: Create Project

```bash
mkdir gitleaks-mlops-lab

cd gitleaks-mlops-lab

git init
```

---

# Step 4: Create Python Application

## app/app.py

```python
from fastapi import FastAPI

app = FastAPI()

@app.get("/")
def home():

    return {
        "status":"healthy"
    }
```

---

## app/.env

```text
AWS_ACCESS_KEY_ID=AKIA123456789

AWS_SECRET_ACCESS_KEY=my-super-secret-key

OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxxxxxxxxxx

DATABASE_PASSWORD=admin123
```

---

# Step 5: Commit Code

```bash
git add .

git commit -m "Initial Commit"
```

---

# Step 6: Scan Repository

```bash
gitleaks detect
```

Expected

```text
4 Leaks Found

AWS Secret

OpenAI Key

Password

Environment Variable
```

---

# Step 7: Scan Specific Directory

```bash
gitleaks detect \
--source app/
```

---

# Step 8: Scan Git History

```bash
gitleaks detect \
--log-opts="--all"
```

Detects secrets committed in previous commits.

---

# Step 9: Generate JSON Report

```bash
gitleaks detect \
--report-format json \
--report-path report.json
```

---

# Step 10: Generate SARIF Report

```bash
gitleaks detect \
--report-format sarif \
--report-path report.sarif
```

Useful for GitHub Code Scanning.

---

# Step 11: Ignore False Positives

Create

```text
.gitleaksignore
```

Example

```text
app/test.py
```

Run

```bash
gitleaks detect
```

---

# Step 12: Create Custom Rules

## .gitleaks.toml

```toml
title = "Enterprise Gitleaks Rules"

[[rules]]

id = "custom-api-key"

description = "Detect API Keys"

regex = '''(?i)api[_-]?key\s*=\s*['"][A-Za-z0-9_-]+['"]'''
```

Scan

```bash
gitleaks detect
```

---

# Step 13: Fail Build if Secrets Exist

```bash
gitleaks detect \
--exit-code 1
```

Used in CI/CD pipelines.

---

# Step 14: Dockerize Application

Build

```bash
docker build -t gitleaks-demo .
```

Run

```bash
docker run -d \
-p 8000:8000 \
--name gitleaks-app \
gitleaks-demo
```

---

# Step 15: Test Application

Health Check

```bash
curl http://localhost:8000
```

Expected

```json
{
  "status":"healthy"
}
```

---

# Step 16: Scan Dockerfile

```bash
gitleaks detect \
--source Dockerfile
```

---

# Step 17: Scan Kubernetes Manifests

```bash
gitleaks detect \
--source kubernetes/
```

---

# Step 18: Scan Entire Repository

```bash
gitleaks detect \
--source .
```

---

# Step 19: Scan Before Every Commit

Install Git Hook

```bash
cp .git/hooks/pre-commit.sample .git/hooks/pre-commit

chmod +x .git/hooks/pre-commit
```

Example Hook

```bash
#!/bin/bash

gitleaks detect

if [ $? -ne 0 ]
then
    echo "Secrets Found"

    exit 1
fi
```

Now every commit is scanned automatically.

---

# Step 20: Continuous Integration Workflow

```bash
gitleaks detect \
--exit-code 1 \
--report-format json \
--report-path report.json
```

---

# Production Best Practices

## Scan

```text
Git Repository

Git History

Environment Files

Python Files

YAML Files

Dockerfile

Terraform

Kubernetes

Secrets

Configuration Files
```

---

## Reports

```text
JSON

SARIF

CSV

Console Output
```

---

## CI/CD Pipeline

```text
Developer
      │
      ▼
GitHub
      │
      ▼
GitHub Actions
      │
      ▼
Gitleaks Scan
      │
      ├── Repository
      ├── Commit History
      ├── Dockerfile
      ├── YAML
      ├── Secrets
      └── Config Files
      │
      ▼
Trivy Scan
      │
      ▼
SonarQube
      │
      ▼
Docker Build
      │
      ▼
Container Registry
      │
      ▼
Kubernetes
```

---

# Skills Covered

- Gitleaks Installation
- Secret Detection
- Git Repository Scanning
- Git History Scanning
- Dockerfile Scanning
- Kubernetes Manifest Scanning
- Environment File Scanning
- Custom Rules
- JSON & SARIF Reports
- Git Hooks
- DevSecOps
- Production Security

---

# Enterprise Security Workflow

```text
Developer
     │
     ▼
GitHub
     │
     ▼
Gitleaks
     │
     ▼
Trivy
     │
     ▼
SonarQube
     │
     ▼
Docker Build
     │
     ▼
AWS ECR
     │
     ▼
Kubernetes
     │
     ▼
Prometheus
     │
     ▼
Grafana
```

---

# Real-World Use Cases

- Prevent AWS credential leaks
- Detect OpenAI API keys
- Prevent database password exposure
- Scan Terraform and Kubernetes repositories
- Enforce secret scanning in CI/CD
- Secure MLOps pipelines before deployment

---

# Suggested Repository Names

```text
gitleaks-mlops-lab

enterprise-gitleaks-devsecops

enterprise-secret-scanning

secure-mlops-pipeline

devsecops-secret-scanning

gitleaks-security-platform
```

## Recommended Repository

```text
enterprise-gitleaks-devsecops
```
