# Gitleaks Production-Level Hands-On Practice Project (MLOps)

## Overview

A production-ready **DevSecOps** project demonstrating how to use **Gitleaks** to detect hardcoded secrets in Machine Learning and MLOps projects.

This project covers scanning Git repositories, commit history, environment files, source code, Dockerfiles, Kubernetes manifests, and configuration files to prevent sensitive information from being committed to source control.

## Features

* Git Repository Secret Scanning
* Git History Scanning
* Environment File Scanning
* Python Source Code Scanning
* Dockerfile Scanning
* Kubernetes Manifest Scanning
* Custom Detection Rules
* JSON & SARIF Report Generation
* Git Hooks Integration
* CI/CD Ready Secret Detection

## Tech Stack

* Gitleaks
* Git
* GitHub
* Python
* FastAPI
* Docker
* Kubernetes
* Ubuntu Linux

## Architecture

```text
Developer
    │
    ▼
Git Repository
    │
    ▼
Gitleaks
    │
    ├── Source Code
    ├── Git History
    ├── Environment Files
    ├── Dockerfile
    ├── Kubernetes
    └── Configuration Files
    │
    ▼
Security Report
    │
    ▼
CI/CD Pipeline
```

## Project Structure

```text
enterprise-gitleaks-devsecops/
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
├── .gitignore
└── README.md
```

## Quick Start

### Clone Repository

```bash
git clone https://github.com/<your-username>/enterprise-gitleaks-devsecops.git

cd enterprise-gitleaks-devsecops
```

### Install Gitleaks

```bash
wget https://github.com/gitleaks/gitleaks/releases/latest/download/gitleaks_linux_x64.tar.gz

tar -xzf gitleaks_linux_x64.tar.gz

sudo mv gitleaks /usr/local/bin/
```

### Verify Installation

```bash
gitleaks version
```

## Scan Repository

```bash
gitleaks detect
```

## Scan Git History

```bash
gitleaks detect --log-opts="--all"
```

## Scan Specific Directory

```bash
gitleaks detect --source app/
```

## Generate JSON Report

```bash
gitleaks detect \
--report-format json \
--report-path report.json
```

## Generate SARIF Report

```bash
gitleaks detect \
--report-format sarif \
--report-path report.sarif
```

## Fail Build on Secret Detection

```bash
gitleaks detect --exit-code 1
```

## Test Application

```bash
curl http://localhost:8000
```

Response

```json
{
  "status": "healthy"
}
```

## Skills Demonstrated

* Secret Detection
* Git Repository Security
* Git History Analysis
* Environment File Protection
* Dockerfile Security
* Kubernetes Security
* Custom Gitleaks Rules
* JSON & SARIF Reporting
* Git Hooks
* DevSecOps Best Practices
* MLOps Security

## Enterprise DevSecOps Workflow

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
Container Registry
      │
      ▼
Kubernetes
```

## Future Enhancements

* GitHub Actions Integration
* Trivy Integration
* SonarQube Integration
* AWS ECR Image Scanning
* Terraform Security Scanning
* Helm Chart Security
* Prometheus Monitoring
* Grafana Dashboards

## License

This project is intended for educational purposes and demonstrates production-ready secret scanning and DevSecOps practices for MLOps environments.
