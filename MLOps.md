

## MLOps Operations Guide

### 📘 What is MLOps?

**MLOps (Machine Learning Operations)** is a set of practices that aims to deploy and maintain machine learning models in production reliably and efficiently. 
MLOps =  machine learning + DevOps + data engineering

### 🔄 MLOps Operations Lifecycle

```
Development → CI/CD → Containerization → Orchestration → Deployment → Monitoring → Optimization
```

| Phase | Definition & Purpose | Key Components (in flow order) |
|-------|----------------------|-------------------------------|
| 1: Development Environment | Standardize infra & tools so every dev has a reproducible environment matching production | Git (clone/version), Poetry (install dependencies), VS Code (load workspace config), pytest (run local tests) |
| 2: CI/CD Pipeline | Automate integration, testing, and deployment to reduce manual errors and speed up releases | GitHub Actions (build), MLflow (deploy to registry), GitHub Actions (rebuild on model update) |
| 3: Containerization | Package code + dependencies into portable containers for consistent runtime across environments | Dockerfile (build image), Docker Hub (push registry), Docker Compose (local orchestration) |
| 4: Orchestration & Scaling | Automate container scheduling across clusters for load balancing and high availability | kubectl (apply to cluster), Istio (enable service mesh), HPA (set auto-scaling policy) |
| 5: Production Deployment | Release model to live users via APIs or UIs, making it accessible and reliable | TensorFlow Serving (serve model), Kong (API gateway), Argo Rollouts (blue‑green deployment) |
| 6: Monitoring & Observability | Collect metrics/logs/traces to understand system state, detect anomalies, and ensure reliability | Prometheus (scrape metrics), Loki (aggregate logs), Jaeger (trace requests), Grafana (visualise), Alertmanager (send alerts) |
| 7: Security & Compliance | Protect data and adhere to regulations while maintaining system integrity | Vault (access control + encryption), Fluentd (audit logging), Chef InSpec (compliance automation) |
| 8: Optimization & Maintenance | Improve performance, reduce cost, and keep systems reliable through updates and backups | Prometheus (performance tuning), AWS Cost Explorer (cost optimisation), Velero (backup), Gremlin (chaos testing for DR) |
### 🛠️ Key Operational Components

#### CI/CD Pipelines
**Definition**: A CI/CD pipeline is an automated sequence of steps that code changes go through from commit to production deployment. It includes stages for building, testing, and deploying applications.

**Core Principles** (according to AWS DevOps documentation):
- **Continuous Integration**: Automatically build and test code changes
- **Continuous Delivery**: Automatically deploy changes to staging environments
- **Continuous Deployment**: Automatically deploy changes to production

#### Container Orchestration
**Definition**: Container orchestration automates the deployment, scaling, and management of containerized applications across clusters of machines.

**Key Features**:
- **Service Discovery**: Automatically detect and connect services
- **Load Balancing**: Distribute traffic across multiple instances
- **Self-Healing**: Automatically restart failed containers
- **Rolling Updates**: Update applications without downtime

#### Model Serving Infrastructure
**Definition**: Model serving infrastructure provides the runtime environment and APIs needed to deploy machine learning models for inference in production.

**Types of Serving**:
- **Real-time Serving**: Low-latency predictions for individual requests
- **Batch Serving**: High-throughput processing of multiple predictions
- **Streaming Serving**: Continuous prediction on data streams

#### Monitoring Stack
**Definition**: A monitoring stack is a collection of tools and processes used to observe, analyze, and alert on the health and performance of systems and applications.

**Components**:
- **Metrics**: Quantitative measurements of system performance
- **Logs**: Detailed records of system events and activities
- **Traces**: Request paths through distributed systems
- **Alerts**: Automated notifications of issues or anomalies

#### Infrastructure as Code (IaC)
**Definition**: Infrastructure as Code is the practice of managing and provisioning computing infrastructure through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.

**Benefits**:
- **Version Control**: Track infrastructure changes like code
- **Reproducibility**: Recreate environments consistently
- **Automation**: Deploy infrastructure programmatically
- **Scalability**: Manage complex infrastructures efficiently

### 📊 Essential Ops Skills

#### Containerization Technologies
- **Docker**: Platform for developing, shipping, and running applications in containers
- **Container Registries**: Storage and distribution systems for container images
- **Container Runtimes**: Software that runs containers (Docker Engine, containerd)

#### Orchestration Platforms
- **Kubernetes**: Open-source container orchestration platform
- **Docker Swarm**: Native clustering and orchestration for Docker
- **Amazon ECS/EKS**: AWS container orchestration services

#### CI/CD Tools
- **GitHub Actions**: CI/CD platform integrated with GitHub
- **GitLab CI/CD**: Comprehensive DevOps platform
- **Jenkins**: Open-source automation server
- **CircleCI**: Cloud-based CI/CD platform

#### Monitoring and Observability
- **Prometheus**: Open-source monitoring and alerting toolkit
- **Grafana**: Open-source analytics and monitoring platform
- **ELK Stack**: Elasticsearch, Logstash, and Kibana for log management
- **Jaeger**: Distributed tracing system

#### Cloud Platforms
- **Amazon Web Services (AWS)**: Comprehensive cloud computing platform
- **Google Cloud Platform (GCP)**: Cloud computing services by Google
- **Microsoft Azure**: Cloud computing platform by Microsoft

#### Infrastructure as Code
- **Terraform**: Open-source infrastructure as code software tool
- **AWS CloudFormation**: Infrastructure as code service for AWS
- **Helm**: Package manager for Kubernetes applications

### 🚀 Getting Started with MLOps Ops

#### Learning Path
1. **Foundations**: Learn Linux, networking, and basic system administration
2. **Containerization**: Master Docker and container concepts
3. **Orchestration**: Learn Kubernetes fundamentals and operations
4. **CI/CD**: Implement automated pipelines with GitHub Actions
5. **Monitoring**: Set up comprehensive monitoring stacks
6. **Cloud Platforms**: Gain expertise in at least one major cloud provider
7. **Security**: Understand container and infrastructure security
8. **Optimization**: Learn performance tuning and cost optimization

#### Prerequisites
- **Programming**: Python, Bash scripting
- **Systems**: Linux administration, networking fundamentals
- **Version Control**: Git and Git workflows
- **Databases**: SQL and NoSQL database concepts
- **APIs**: REST API design and implementation

### 📈 Career Path in MLOps Operations

#### Entry-Level (0-2 years)
- **DevOps Engineer**: Focus on infrastructure automation and deployment
- **Site Reliability Engineer (SRE)**: Emphasis on system reliability and monitoring
- **Platform Engineer**: Build and maintain development platforms

#### Mid-Level (2-5 years)
- **Senior DevOps Engineer**: Lead infrastructure initiatives and team mentoring
- **MLOps Engineer**: Specialize in ML infrastructure and operations
- **Cloud Engineer**: Deep expertise in cloud platforms and services

#### Senior-Level (5+ years)
- **Principal Engineer**: Technical leadership and architecture design
- **Engineering Manager**: Lead teams and manage MLOps operations
- **Platform Architect**: Design scalable ML platforms and systems

#### Key Skills Progression
- **Technical Skills**: Container orchestration, IaC, monitoring, security
- **Soft Skills**: Communication, collaboration, problem-solving
- **Leadership Skills**: Team management, strategic planning, mentoring

<a id="top"></a>
<style>
.back-to-top-button {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background: #1f77b4;
  color: #ffffff;
  padding: 10px 14px;
  border-radius: 999px;
  text-decoration: none;
  font-weight: bold;
  box-shadow: 0 6px 18px rgba(0,0,0,0.18);
  z-index: 9999;
}
.back-to-top-button:hover {
  background: #155a8a;
}
</style>

<a href="#top" class="back-to-top-button">Back to Top</a>

## Table of Contents

- [1. Development Environment Setup](#1-development-environment-setup)
  - [1.1 Local Development Environment](#11-local-development-environment)
  - [1.2 Version Control with Git](#12-version-control-with-git)
  - [1.3 Development Tools and IDEs](#13-development-tools-and-ides)
- [2. CI/CD Pipeline Automation](#2-cicd-pipeline-automation)
  - [2.1 GitHub Actions Fundamentals](#21-github-actions-fundamentals)
  - [2.2 Automated Testing](#22-automated-testing)
  - [2.3 Continuous Deployment](#23-continuous-deployment)
- [3. Containerization](#3-containerization)
  - [3.1 Docker Fundamentals](#31-docker-fundamentals)
  - [3.2 Multi-stage Builds for ML](#32-multi-stage-builds-for-ml)
  - [3.3 Docker Compose for ML Stacks](#33-docker-compose-for-ml-stacks)
- [4. Orchestration and Scaling](#4-orchestration-and-scaling)
  - [4.1 Kubernetes Basics](#41-kubernetes-basics)
  - [4.2 Helm Charts for ML Applications](#42-helm-charts-for-ml-applications)
  - [4.3 Auto-scaling and Load Balancing](#43-auto-scaling-and-load-balancing)
- [5. Model Management and Serving](#5-model-management-and-serving)
  - [5.1 MLflow for Experiment Tracking](#51-mlflow-for-experiment-tracking)
  - [5.2 Model Registry and Versioning](#52-model-registry-and-versioning)
  - [5.3 Model Serving Infrastructure](#53-model-serving-infrastructure)
- [6. Monitoring and Observability](#6-monitoring-and-observability)
  - [6.1 Prometheus Metrics Collection](#61-prometheus-metrics-collection)
  - [6.2 Grafana Dashboards](#62-grafana-dashboards)
  - [6.3 Logging with ELK Stack](#63-logging-with-elk-stack)
- [7. Security and Compliance](#7-security-and-compliance)
  - [7.1 Container Security](#71-container-security)
  - [7.2 Infrastructure Security](#72-infrastructure-security)
  - [7.3 Compliance Automation](#73-compliance-automation)
- [8. Optimization and Maintenance](#8-optimization-and-maintenance)
  - [8.1 Performance Optimization](#81-performance-optimization)
  - [8.2 Cost Optimization](#82-cost-optimization)
  - [8.3 Backup and Disaster Recovery](#83-backup-and-disaster-recovery)
- [9. Troubleshooting Guide](#9-troubleshooting-guide)
  - [9.1 Common Operational Issues](#91-common-operational-issues)
  - [9.2 Debugging Strategies](#92-debugging-strategies)
  - [9.3 Incident Response](#93-incident-response)
- [10. Resources and Best Practices](#10-resources-and-best-practices)
  - [10.1 Official Documentation](#101-official-documentation)
  - [10.2 Learning Resources](#102-learning-resources)
  - [10.3 Community and Tools](#103-community-and-tools)
  - [10.1 Container Security](#101-container-security)
  - [10.2 Model Security](#102-model-security)
  - [10.3 Compliance Automation](#103-compliance-automation)
- [11. Troubleshooting and Best Practices](#11-troubleshooting-and-best-practices)
  - [11.1 Common Operational Issues](#111-common-operational-issues)
  - [11.2 Performance Optimization](#112-performance-optimization)
  - [11.3 Cost Optimization](#113-cost-optimization)
- [12. Resources and Tools](#12-resources-and-tools)
  - [12.1 Official Documentation](#121-official-documentation)
  - [12.2 Learning Resources](#122-learning-resources)
  - [12.3 Community and Events](#123-community-and-events)

## 1. Development Environment Setup

### 1.1 Local Development Environment

#### What is a Development Environment?

A development environment is a workspace configured with all the necessary tools, libraries, and dependencies required for software development. In MLOps, it must support both machine learning development and operational tooling.

**Key Characteristics**:
- **Isolation**: Separate environments for different projects to avoid dependency conflicts
- **Reproducibility**: Ability to recreate the exact same environment across different machines
- **Consistency**: Same tools and configurations across development, staging, and production

#### Python Environment Management

**Conda Environments:**
Conda is an open-source package management system and environment management system that runs on Windows, macOS, and Linux. It allows you to create isolated environments with specific versions of packages.

```bash
# Create a new conda environment for ML development
conda create -n mlops-env python=3.9

# Activate the environment
conda activate mlops-env

# Install essential ML packages
conda install -c conda-forge scikit-learn pandas numpy matplotlib jupyter

# Export environment for reproducibility
conda env export > environment.yml
```

**Benefits of Conda**:
- **Cross-platform compatibility**: Works on Windows, macOS, Linux
- **Package management**: Handles both Python and non-Python dependencies
- **Environment isolation**: Prevents conflicts between different projects
- **Reproducible environments**: Environment files can be shared and recreated

**Virtualenv with pip:**
Virtualenv is a tool to create isolated Python environments. It creates a folder containing all the necessary executables to use the packages that a Python project would need.

```bash
# Create virtual environment
python -m venv mlops-env

# Activate environment
source mlops-env/bin/activate  # Linux/Mac
# or
mlops-env\Scripts\activate     # Windows

# Install requirements
pip install -r requirements.txt

# Deactivate when done
deactivate
```

**When to use Virtualenv vs Conda**:
- **Use Conda**: When you need non-Python dependencies or want cross-platform compatibility
- **Use Virtualenv**: When you only need Python packages and want a lightweight solution

#### Essential Development Tools

**Jupyter Lab:**
JupyterLab is the next-generation user interface for Project Jupyter. It offers all the familiar building blocks of the classic Jupyter Notebook (notebook, terminal, text editor, file browser, rich outputs, etc.) in a flexible and powerful user interface.

```bash
# Install Jupyter Lab
pip install jupyterlab

# Launch Jupyter Lab
jupyter lab
```

**Key Features**:
- **Modular interface**: Drag-and-drop interface for arranging panels
- **File browser**: Navigate and manage files and directories
- **Terminal integration**: Run shell commands directly in the browser
- **Text editor**: Edit files with syntax highlighting and code completion
- **Notebook support**: Enhanced notebook experience with better performance

**Visual Studio Code:**
Visual Studio Code (VS Code) is a free, open-source code editor developed by Microsoft. It's highly extensible and supports many programming languages through extensions.

**Essential Extensions for MLOps**:
- **Python**: Official Python extension with IntelliSense, debugging, and more
- **Docker**: Build, manage, and deploy containerized applications
- **Kubernetes**: Develop, deploy, and debug Kubernetes applications
- **GitLens**: Enhance Git capabilities in VS Code
- **YAML**: YAML Language Support for Kubernetes manifests

#### Development Workflow Tools

**Git for Version Control:**
Git is a distributed version control system that tracks changes in source code during software development. It allows multiple developers to work on the same codebase simultaneously.

**Basic Git Workflow**:
```bash
# Initialize repository
git init

# Add files to staging
git add .

# Commit changes
git commit -m "Initial commit"

# Create and switch to branch
git checkout -b feature/ml-pipeline

# Push to remote repository
git push origin feature/ml-pipeline
```

**Pre-commit Hooks:**
Pre-commit hooks are scripts that run before a commit is created. They can check code quality, run tests, and enforce standards.

```bash
# Install pre-commit
pip install pre-commit

# Create .pre-commit-config.yaml
# Configure hooks for black, flake8, mypy, etc.
```

**Makefile for Automation:**
A Makefile is a file containing a set of directives used by the make build automation tool. In MLOps, it's commonly used to automate development tasks.

```makefile
.PHONY: install test lint format clean

install:
	pip install -r requirements.txt

test:
	pytest tests/ -v

lint:
	flake8 src/ tests/

format:
	black src/ tests/

clean:
	find . -type f -name "*.pyc" -delete
	find . -type d -name "__pycache__" -delete
```

### 1.2 Version Control with Git

#### Git Fundamentals

**What is Version Control?**
Version control is a system that records changes to files over time so that you can recall specific versions later. Git is a distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

**Core Git Concepts**:
- **Repository**: A directory containing your project files and the entire history of changes
- **Commit**: A snapshot of your repository at a specific point in time
- **Branch**: A parallel version of the repository allowing independent development
- **Merge**: Combining changes from different branches
- **Pull Request**: A request to merge changes from one branch to another

#### Git Workflow for MLOps

**GitFlow Workflow:**
GitFlow is a branching model for Git that defines a strict branching model designed around the project release.

```bash
# Create develop branch
git checkout -b develop

# Create feature branch
git checkout -b feature/model-training-pipeline

# Merge feature to develop
git checkout develop
git merge feature/model-training-pipeline

# Create release branch
git checkout -b release/v1.0.0

# Merge release to main and develop
git checkout main
git merge release/v1.0.0
git checkout develop
git merge release/v1.0.0
```

**Branch Naming Conventions**:
- `main` or `master`: Production-ready code
- `develop`: Integration branch for features
- `feature/*`: New features or experiments
- `bugfix/*`: Bug fixes
- `hotfix/*`: Critical fixes for production
- `release/*`: Release preparation

#### Git Best Practices for MLOps

**Commit Messages:**
Follow conventional commit format for consistency and automation:

```
type(scope): description

[optional body]

[optional footer]
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Example**:
```
feat(model): add support for XGBoost classifier

- Implement XGBoost training pipeline
- Add hyperparameter tuning
- Update model validation metrics

Closes #123
```

**Git LFS for Large Files:**
Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git.

```bash
# Install Git LFS
git lfs install

# Track large files
git lfs track "*.pkl"
git lfs track "*.h5"
git lfs track "data/*.csv"

# Add .gitattributes
git add .gitattributes
```

### 1.3 Development Tools and IDEs

#### Integrated Development Environments (IDEs)

**PyCharm Professional:**
PyCharm is an IDE specifically designed for Python development with advanced features for web development, data science, and machine learning.

**Key Features for MLOps**:
- **Scientific Mode**: Enhanced support for Jupyter notebooks
- **Database Tools**: Built-in database browser and SQL editor
- **Docker Integration**: Run and debug applications in Docker containers
- **Remote Development**: Connect to remote machines for development
- **Profiling Tools**: Performance analysis and memory debugging

**VS Code Configuration for MLOps:**

**settings.json**:
```json
{
    "python.defaultInterpreterPath": "./venv/bin/python",
    "python.linting.enabled": true,
    "python.linting.flake8Enabled": true,
    "python.formatting.blackPath": "black",
    "python.formatting.provider": "black",
    "editor.formatOnSave": true,
    "docker.languageserver.diagnostics.deprecatedMaintainer": "ignore"
}
```

**Recommended Extensions**:
- **Python** (ms-python.python): Core Python support
- **Pylance** (ms-python.vscode-pylance): Fast, feature-rich language support
- **Jupyter** (ms-toolsai.jupyter): Jupyter notebook support
- **Docker** (ms-azuretools.vscode-docker): Docker integration
- **Kubernetes** (ms-kubernetes-tools.vscode-kubernetes-tools): K8s support
- **GitLens** (eamodio.gitlens): Enhanced Git capabilities
- **Remote SSH** (ms-vscode-remote.remote-ssh): Remote development

#### Code Quality Tools

**Linting:**
Linting analyzes code for potential errors, bugs, stylistic errors, and suspicious constructs.

**Flake8:**
Flake8 is a wrapper around PyFlakes, pycodestyle, and Ned Batchelder's McCabe script.

```bash
# Install flake8
pip install flake8

# Run linting
flake8 src/ tests/

# Configuration in setup.cfg
[flake8]
max-line-length = 88
extend-ignore = E203, W503
exclude = .git,__pycache__,build,dist
```

**Black Code Formatter:**
Black is the uncompromising Python code formatter. It enforces a consistent code style.

```bash
# Install black
pip install black

# Format code
black src/ tests/

# Check formatting without changes
black --check src/ tests/
```

**MyPy for Type Checking:**
MyPy is an optional static type checker for Python that aims to combine the benefits of dynamic typing and static typing.

```python
# example.py
from typing import List, Optional

def train_model(X: List[List[float]], y: List[int]) -> Optional[str]:
    """Train a machine learning model."""
    if not X or not y:
        return None
    # Training logic here
    return "model_trained"
```

**Testing Frameworks:**

**pytest:**
pytest is a mature, full-featured Python testing framework that helps you write better programs.

```python
# test_model.py
import pytest
from src.model import train_model, predict

class TestModel:
    def test_train_model_success(self):
        X = [[1, 2], [3, 4], [5, 6]]
        y = [0, 1, 0]

        result = train_model(X, y)
        assert result == "model_trained"

    def test_predict_shape(self):
        # Mock trained model
        predictions = predict([[1, 2], [3, 4]])
        assert len(predictions) == 2
        assert all(isinstance(p, (int, float)) for p in predictions)
```

**Coverage Testing:**
Coverage.py measures code coverage, typically during test execution.

```bash
# Install coverage
pip install coverage

# Run tests with coverage
coverage run -m pytest

# Generate report
coverage report

# Generate HTML report
coverage html
```

#### Development Environment Automation

**Environment Setup Scripts:**

**setup.sh** for Linux/Mac:
```bash
#!/bin/bash

# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install -r requirements-dev.txt

# Setup pre-commit hooks
pre-commit install

echo "Development environment setup complete!"
```

**setup.ps1** for Windows:
```powershell
# Create virtual environment
python -m venv venv
venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Install development dependencies
pip install -r requirements-dev.txt

# Setup pre-commit hooks
pre-commit install

Write-Host "Development environment setup complete!"
```

**Docker for Development:**

**Dockerfile.dev**:
```dockerfile
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    git \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt requirements-dev.txt ./
RUN pip install --no-cache-dir -r requirements.txt -r requirements-dev.txt

# Copy source code
COPY . .

# Expose port for Jupyter
EXPOSE 8888

# Default command
CMD ["jupyter", "lab", "--ip=0.0.0.0", "--allow-root", "--no-browser"]
```

**docker-compose.dev.yml**:
```yaml
version: '3.8'
services:
  mlops-dev:
    build:
      context: .
      dockerfile: Dockerfile.dev
    volumes:
      - .:/app
      - /app/venv
    ports:
      - "8888:8888"
    environment:
      - JUPYTER_TOKEN=dev-token
    command: jupyter lab --ip=0.0.0.0 --allow-root --no-browser --NotebookApp.token='dev-token'
```

This comprehensive development environment setup ensures consistency, reproducibility, and efficiency in MLOps development workflows.

# Configure Jupyter for ML development
jupyter lab --notebook-dir=/path/to/ml-projects
```

**VS Code Configuration:**
- Install Python extension
- Install Docker extension
- Install Kubernetes extension
- Configure Python interpreter for virtual environment
- Set up debugging configurations

#### Local Infrastructure Setup

**Docker Desktop:**
```bash
# Verify Docker installation
docker --version
docker-compose --version

# Test Docker with hello-world
docker run hello-world
```

**Minikube for Local Kubernetes:**
```bash
# Install Minikube
# macOS
brew install minikube

# Linux
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start Minikube
minikube start

# Verify cluster
kubectl get nodes
```

### 1.2 Version Control with Git

Effective version control is essential for MLOps, especially when dealing with code, configurations, and model artifacts.

#### Git Workflow Best Practices

**Repository Structure:**
```
mlops-project/
├── .github/
│   └── workflows/          # GitHub Actions
├── docker/
│   ├── Dockerfile
│   └── docker-compose.yml
├── k8s/                    # Kubernetes manifests
├── src/
│   ├── models/
│   ├── pipelines/
│   └── utils/
├── tests/
├── requirements.txt
├── environment.yml
└── README.md
```

**Branching Strategy:**
```bash
# Create feature branch
git checkout -b feature/model-serving

# Make changes and commit
git add .
git commit -m "Add model serving endpoint"

# Push to remote
git push origin feature/model-serving

# Create pull request
# Merge after review
```

#### Handling Large Files and Datasets

**Git LFS for Large Files:**
```bash
# Install Git LFS
git lfs install

# Track large files
git lfs track "*.pkl"
git lfs track "*.h5"
git lfs track "models/**"

# Add .gitattributes
git add .gitattributes
git commit -m "Add Git LFS tracking"
```

**DVC for Data Versioning:**
```bash
# Initialize DVC
dvc init

# Add data files
dvc add data/train.csv
dvc add data/models/model.pkl

# Commit DVC files
git add data/train.csv.dvc data/models/model.pkl.dvc
git commit -m "Add data and model versioning"
```

### 1.3 Development Tools and IDEs

#### VS Code for MLOps Development

**Essential Extensions:**
- Python
- Docker
- Kubernetes
- GitLens
- Remote Development
- Jupyter
- YAML

**VS Code Settings for ML:**
```json
{
    "python.defaultInterpreterPath": "./venv/bin/python",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "python.formatting.provider": "black",
    "editor.formatOnSave": true,
    "python.testing.pytestEnabled": true
}
```

#### Jupyter Environment Setup

**Jupyter Extensions:**
```bash
# Install extensions
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user

# Enable useful extensions
jupyter nbextension enable codefolding/main
jupyter nbextension enable collapsible_headings/main
```

**Remote Jupyter Setup:**
```bash
# Install jupyter-server-proxy
pip install jupyter-server-proxy

# Configure remote access
jupyter lab --ip=0.0.0.0 --port=8888 --no-browser --allow-root
```

#### Development Best Practices

**Code Quality Tools:**
```bash
# Install development dependencies
pip install black flake8 mypy pre-commit

# Configure pre-commit hooks
# .pre-commit-config.yaml
repos:
- repo: https://github.com/pre-commit/pre-commit-hooks
  rev: v4.4.0
  hooks:
  - id: trailing-whitespace
  - id: end-of-file-fixer
  - id: check-yaml
  - id: check-added-large-files

- repo: https://github.com/psf/black
  rev: 22.3.0
  hooks:
  - id: black
```

**Environment Consistency:**
- Use `requirements.txt` or `environment.yml`
- Document setup instructions in README
- Use Docker for consistent environments
- Implement automated environment checks

## 2. CI/CD Pipeline Automation

### 2.1 GitHub Actions Fundamentals

#### What is CI/CD?

**Continuous Integration (CI)** is a development practice where developers regularly merge their code changes into a central repository, after which automated builds and tests are run.

**Continuous Delivery (CD)** extends CI by automatically deploying all code changes to a testing and/or production environment after the build stage.

**Continuous Deployment** goes one step further by automatically deploying changes to production without human intervention.

**Benefits in MLOps**:
- **Automated Testing**: Ensure code quality and prevent regressions
- **Faster Feedback**: Catch issues early in the development cycle
- **Consistent Deployments**: Reduce manual errors and ensure reproducibility
- **Version Control Integration**: Tie deployments directly to code changes

#### GitHub Actions Architecture

GitHub Actions is a CI/CD platform that allows you to automate your build, test, and deployment pipeline. It uses workflows defined in YAML files stored in your repository.

**Core Components**:

**Workflows**: Automated processes defined in `.github/workflows/` directory
**Events**: Triggers that start workflows (push, pull request, schedule, etc.)
**Jobs**: Set of steps that execute on the same runner
**Steps**: Individual tasks within a job
**Actions**: Reusable units of code that perform specific tasks
**Runners**: Machines that execute the jobs (GitHub-hosted or self-hosted)

#### Basic Workflow Structure

**Simple CI Pipeline:**
```yaml
# .github/workflows/ci.yml
name: CI Pipeline

# Triggers for the workflow
on:
  push:
    branches: [ main, develop ]
  pull_request:
    branches: [ main ]

# Jobs to run
jobs:
  test:
    # Runner environment
    runs-on: ubuntu-latest

    steps:
    # Checkout repository code
    - uses: actions/checkout@v3

    # Setup Python environment
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.9'

    # Install project dependencies
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    # Execute test suite
    - name: Run tests
      run: |
        python -m pytest tests/ -v --cov=src/

    # Upload coverage reports
    - name: Upload coverage
      uses: codecov/codecov-action@v3
```

**Workflow Triggers Explained**:
- `push`: Triggers on code pushes to specified branches
- `pull_request`: Triggers on pull request creation/update to specified branches
- `schedule`: Cron-based scheduling for regular tasks
- `workflow_dispatch`: Manual workflow triggering
- `release`: Triggers on GitHub release creation

#### Advanced Workflow Features

**Matrix Builds:**
Matrix builds allow you to run the same job multiple times with different configurations, enabling testing across multiple environments simultaneously.

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    # Define matrix of test configurations
    strategy:
      matrix:
        python-version: [3.8, 3.9, '3.10']
        include:
          - python-version: 3.9
            experimental: true

    steps:
    - uses: actions/checkout@v3

    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v4
      with:
        python-version: ${{ matrix.python-version }}

    - name: Install dependencies
      run: pip install -r requirements.txt

    - name: Run tests
      run: python -m pytest tests/
```

**Benefits of Matrix Builds**:
- **Multi-version Testing**: Test against multiple Python versions
- **Cross-platform Compatibility**: Test on different operating systems
- **Parallel Execution**: Run tests simultaneously for faster feedback
- **Fail-fast Strategy**: Stop on first failure or continue for comprehensive results

**Dependency Caching:**
Caching dependencies reduces build times by storing and reusing previously downloaded packages.

```yaml
steps:
- uses: actions/checkout@v3

- name: Cache pip dependencies
  uses: actions/cache@v3
  with:
    # Path to cache
    path: ~/.cache/pip
    # Cache key based on requirements file hash
    key: ${{ runner.os }}-pip-${{ hashFiles('**/requirements.txt') }}
    # Fallback keys for partial cache hits
    restore-keys: |
      ${{ runner.os }}-pip-

- name: Set up Python
  uses: actions/setup-python@v4
  with:
    python-version: '3.9'

- name: Install dependencies
  run: |
    pip install -r requirements.txt
```

**Caching Strategies**:
- **Hash-based Keys**: Use file hashes to invalidate cache when dependencies change
- **Multi-level Restore Keys**: Provide fallback caches for partial hits
- **Platform-specific Caches**: Separate caches for different operating systems
- **Dependency-specific Caches**: Cache different types of dependencies separately

#### Environment Variables and Secrets

**Environment Variables:**
```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment: production
    env:
      NODE_ENV: production
      API_URL: ${{ vars.API_URL }}
    steps:
    - name: Deploy to production
      run: echo "Deploying to $NODE_ENV with API_URL=$API_URL"
```

**Secrets Management:**
```yaml
steps:
- name: Configure AWS credentials
  uses: aws-actions/configure-aws-credentials@v2
  with:
    aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
    aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
    aws-region: us-east-1
```

**Security Best Practices**:
- **Never log secrets**: Use masking to prevent accidental exposure
- **Environment-specific secrets**: Use different secrets for different environments
- **Minimal permissions**: Grant only necessary permissions to workflows
- **Regular rotation**: Rotate secrets regularly and on compromise

### 2.2 Automated Testing

#### Testing Pyramid in MLOps

The testing pyramid is a concept that groups software tests into three layers based on their scope and speed.

**Unit Tests (Bottom Layer)**:
- Test individual functions, methods, or classes in isolation
- Fast execution, high coverage, immediate feedback
- Should represent ~70% of total tests

**Integration Tests (Middle Layer)**:
- Test interactions between different components
- Slower than unit tests but catch more complex issues
- Should represent ~20% of total tests

**End-to-End Tests (Top Layer)**:
- Test complete user workflows from start to finish
- Slowest execution but highest confidence
- Should represent ~10% of total tests

#### Unit Testing for ML Code

**Testing ML Model Components:**
```python
# tests/test_model.py
import pytest
import numpy as np
from sklearn.ensemble import RandomForestClassifier
from src.model import train_model, predict, evaluate_model

class TestModelTraining:
    """Test cases for model training functionality."""

    @pytest.fixture
    def sample_data(self):
        """Provide sample training data."""
        np.random.seed(42)
        X = np.random.randn(100, 4)
        y = np.random.randint(0, 2, 100)
        return X, y

    def test_train_model_success(self, sample_data):
        """Test successful model training."""
        X, y = sample_data

        model = train_model(X, y)

        assert model is not None
        assert isinstance(model, RandomForestClassifier)
        assert hasattr(model, 'predict')

    def test_train_model_empty_data(self):
        """Test model training with empty data."""
        X, y = np.array([]), np.array([])

        with pytest.raises(ValueError):
            train_model(X, y)

    def test_predict_shape(self, sample_data):
        """Test prediction output shape."""
        X, y = sample_data
        model = train_model(X, y)

        X_test = np.random.randn(10, 4)
        predictions = predict(model, X_test)

        assert predictions.shape == (10,)
        assert predictions.dtype in [np.int32, np.int64]

    def test_evaluate_model_metrics(self, sample_data):
        """Test model evaluation returns expected metrics."""
        X, y = sample_data
        model = train_model(X, y)

        metrics = evaluate_model(model, X, y)

        required_metrics = ['accuracy', 'precision', 'recall', 'f1_score']
        for metric in required_metrics:
            assert metric in metrics
            assert isinstance(metrics[metric], (int, float))
            assert 0 <= metrics[metric] <= 1
```

**Mocking External Dependencies:**
```python
# tests/test_api.py
from unittest.mock import Mock, patch
import pytest
from src.api import ModelAPI

class TestModelAPI:
    """Test cases for model API endpoints."""

    @pytest.fixture
    def api_client(self):
        """Create API client with mocked model."""
        api = ModelAPI()
        api.model = Mock()
        api.model.predict.return_value = [0.8, 0.3]
        return api

    @patch('src.api.load_model_from_registry')
    def test_predict_endpoint_success(self, mock_load_model, api_client):
        """Test successful prediction endpoint."""
        mock_load_model.return_value = api_client.model

        # Simulate API request
        features = [[1.0, 2.0, 3.0, 4.0], [5.0, 6.0, 7.0, 8.0]]
        result = api_client.predict(features)

        assert result == [0.8, 0.3]
        api_client.model.predict.assert_called_once_with(features)

    @patch('src.api.validate_input')
    def test_predict_endpoint_validation_error(self, mock_validate, api_client):
        """Test prediction endpoint with invalid input."""
        mock_validate.side_effect = ValueError("Invalid input format")

        with pytest.raises(ValueError, match="Invalid input format"):
            api_client.predict("invalid_input")
```

#### Integration Testing

**Testing Data Pipeline Integration:**
```python
# tests/test_pipeline.py
import pytest
import pandas as pd
from src.pipeline import DataPipeline, ModelPipeline

class TestDataPipeline:
    """Test data processing pipeline integration."""

    @pytest.fixture
    def sample_raw_data(self):
        """Create sample raw data for testing."""
        return pd.DataFrame({
            'feature1': [1, 2, 3, None, 5],
            'feature2': ['A', 'B', 'A', 'C', 'B'],
            'target': [0, 1, 0, 1, 0]
        })

    def test_data_pipeline_end_to_end(self, sample_raw_data):
        """Test complete data processing pipeline."""
        pipeline = DataPipeline()

        # Process raw data
        processed_data = pipeline.process(sample_raw_data)

        # Assertions
        assert processed_data is not None
        assert 'feature1' in processed_data.columns
        assert 'feature2_encoded' in processed_data.columns
        assert processed_data['feature1'].isnull().sum() == 0  # No nulls after processing
        assert len(processed_data) == len(sample_raw_data)

    def test_model_pipeline_integration(self, sample_raw_data):
        """Test integration between data and model pipelines."""
        data_pipeline = DataPipeline()
        model_pipeline = ModelPipeline()

        # Process data
        processed_data = data_pipeline.process(sample_raw_data)

        # Train model
        model = model_pipeline.train(processed_data.drop('target', axis=1),
                                   processed_data['target'])

        # Make predictions
        predictions = model_pipeline.predict(model, processed_data.drop('target', axis=1))

        assert len(predictions) == len(processed_data)
        assert all(pred in [0, 1] for pred in predictions)
```

#### Test Coverage and Quality Metrics

**Coverage Configuration:**
```ini
# .coveragerc
[run]
source = src
omit =
    */tests/*
    */venv/*
    setup.py

[report]
exclude_lines =
    pragma: no cover
    def __repr__
    raise AssertionError
    raise NotImplementedError
    if __name__ == .__main__.:
    class .*\bProtocol\):
    @(abc\.)?abstractmethod

[html]
directory = htmlcov
```

**Quality Gates in CI/CD:**
```yaml
# .github/workflows/ci.yml
- name: Run tests with coverage
  run: |
    pytest --cov=src --cov-report=xml --cov-report=term-missing

- name: Upload coverage to Codecov
  uses: codecov/codecov-action@v3
  with:
    file: ./coverage.xml
    fail_ci_if_error: true

- name: Check coverage threshold
  run: |
    coverage report --fail-under=80
```

### 2.3 Continuous Deployment

#### Deployment Strategies

**Blue-Green Deployment:**
Blue-green deployment is a technique that reduces downtime and risk by running two identical production environments called Blue and Green.

**Benefits**:
- **Zero downtime**: Switch between environments instantly
- **Instant rollback**: Switch back to previous version immediately
- **Testing in production**: Test new version before full rollout

**Implementation in GitHub Actions:**
```yaml
# .github/workflows/deploy.yml
name: Blue-Green Deployment

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v2
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

    - name: Deploy to Blue environment
      run: |
        # Deploy to blue environment
        aws ecs update-service --cluster ml-cluster --service blue-service --force-new-deployment

    - name: Run smoke tests on Blue
      run: |
        # Wait for deployment
        aws ecs wait services-stable --cluster ml-cluster --services blue-service
        # Run smoke tests
        python scripts/smoke_test.py --environment blue

    - name: Switch traffic to Blue
      run: |
        # Update load balancer to route to blue
        aws elbv2 modify-listener --listener-arn ${{ secrets.LISTENER_ARN }} \
          --default-actions Type=forward,TargetGroupArn=${{ secrets.BLUE_TARGET_GROUP }}

    - name: Monitor and rollback if needed
      run: |
        # Monitor for 5 minutes
        sleep 300
        # Check error rates, latency, etc.
        if python scripts/health_check.py --environment blue; then
          echo "Deployment successful"
        else
          echo "Rolling back..."
          # Switch back to green
          aws elbv2 modify-listener --listener-arn ${{ secrets.LISTENER_ARN }} \
            --default-actions Type=forward,TargetGroupArn=${{ secrets.GREEN_TARGET_GROUP }}
          exit 1
        fi
```

**Canary Deployment:**
Canary deployment gradually rolls out changes to a small subset of users before rolling out to the entire infrastructure.

```yaml
# .github/workflows/canary-deploy.yml
name: Canary Deployment

jobs:
  canary-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Deploy to 10% of traffic
      run: |
        # Update canary deployment
        kubectl set image deployment/ml-api-canary ml-api=${{ github.sha }}
        kubectl scale deployment ml-api-canary --replicas=1

    - name: Monitor canary
      run: |
        # Wait and monitor metrics
        sleep 600  # 10 minutes

        # Check if canary is healthy
        if kubectl get pods -l app=ml-api-canary | grep -q Running; then
          echo "Canary healthy, proceeding with full deployment"
        else
          echo "Canary failed, rolling back"
          kubectl scale deployment ml-api-canary --replicas=0
          exit 1
        fi

    - name: Full deployment
      run: |
        # Scale canary to full deployment
        kubectl set image deployment/ml-api ml-api=${{ github.sha }}
        kubectl scale deployment ml-api --replicas=10
        kubectl scale deployment ml-api-canary --replicas=0
```

#### Infrastructure as Code Integration

**Terraform with GitHub Actions:**
```yaml
# .github/workflows/infrastructure.yml
name: Infrastructure Deployment

on:
  push:
    branches: [ main ]
    paths:
      - 'infrastructure/**'

jobs:
  terraform:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Setup Terraform
      uses: hashicorp/setup-terraform@v2

    - name: Terraform Format
      run: terraform fmt -check

    - name: Terraform Init
      run: terraform init

    - name: Terraform Validate
      run: terraform validate

    - name: Terraform Plan
      run: terraform plan -out=tfplan

    - name: Terraform Apply
      run: terraform apply tfplan
```

#### Deployment Safety Measures

**Automated Rollbacks:**
```yaml
# .github/workflows/rollback.yml
name: Rollback Deployment

on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Environment to rollback'
        required: true
        default: 'production'

jobs:
  rollback:
    runs-on: ubuntu-latest

    steps:
    - name: Rollback ${{ github.event.inputs.environment }}
      run: |
        # Get previous deployment
        PREVIOUS_SHA=$(git rev-parse HEAD~1)

        # Deploy previous version
        kubectl set image deployment/ml-api ml-api=${PREVIOUS_SHA}

        # Wait for rollout
        kubectl rollout status deployment/ml-api

        # Run smoke tests
        python scripts/smoke_test.py
```

**Health Checks and Monitoring:**
```python
# scripts/health_check.py
import requests
import time
import sys

def check_health(endpoint: str, timeout: int = 30) -> bool:
    """Check service health with timeout."""
    start_time = time.time()

    while time.time() - start_time < timeout:
        try:
            response = requests.get(f"{endpoint}/health")
            if response.status_code == 200:
                print("Health check passed")
                return True
        except requests.RequestException:
            pass

        time.sleep(5)

    print("Health check failed")
    return False

def check_model_performance(endpoint: str) -> bool:
    """Check model performance metrics."""
    try:
        # Test prediction endpoint
        test_data = {"features": [[1.0, 2.0, 3.0, 4.0]]}
        response = requests.post(f"{endpoint}/predict", json=test_data)

        if response.status_code != 200:
            return False

        result = response.json()
        if "predictions" not in result:
            return False

        # Check latency (should be < 100ms for real-time)
        latency = response.elapsed.total_seconds() * 1000
        if latency > 100:
            print(f"High latency: {latency}ms")
            return False

        return True

    except Exception as e:
        print(f"Performance check failed: {e}")
        return False

if __name__ == "__main__":
    endpoint = sys.argv[1] if len(sys.argv) > 1 else "http://localhost:8000"

    if not check_health(endpoint):
        sys.exit(1)

    if not check_model_performance(endpoint):
        sys.exit(1)

    print("All checks passed")
```

This comprehensive CI/CD section provides the foundation for automated, reliable, and safe deployment of ML systems in production environments.

- name: Install dependencies
  run: |
    python -m pip install --upgrade pip
    pip install -r requirements.txt
```

### 2.2 Automated Testing

Comprehensive testing is crucial for maintaining reliable ML systems in production.

#### Unit Testing for ML Code

**Testing ML Models:**
```python
# tests/test_model.py
import pytest
import numpy as np
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score
from src.model import train_model, predict

class TestModel:
    def setup_method(self):
        self.X_train = np.random.rand(100, 4)
        self.y_train = np.random.randint(0, 2, 100)
        self.X_test = np.random.rand(20, 4)
        self.y_test = np.random.randint(0, 2, 20)
    
    def test_model_training(self):
        model = train_model(self.X_train, self.y_train)
        assert model is not None
        assert isinstance(model, RandomForestClassifier)
    
    def test_model_prediction(self):
        model = train_model(self.X_train, self.y_train)
        predictions = predict(model, self.X_test)
        assert len(predictions) == len(self.X_test)
        assert all(pred in [0, 1] for pred in predictions)
    
    def test_model_accuracy(self):
        model = train_model(self.X_train, self.y_train)
        predictions = predict(model, self.X_test)
        accuracy = accuracy_score(self.y_test, predictions)
        assert accuracy > 0.5  # Basic sanity check
```

**Testing Data Pipelines:**
```python
# tests/test_pipeline.py
import pytest
import pandas as pd
from src.data_pipeline import load_data, preprocess_data, validate_data

class TestDataPipeline:
    def test_load_data(self):
        df = load_data('tests/test_data.csv')
        assert isinstance(df, pd.DataFrame)
        assert not df.empty
    
    def test_preprocess_data(self):
        raw_data = pd.DataFrame({
            'feature1': [1, 2, None, 4],
            'feature2': ['A', 'B', 'A', 'C']
        })
        processed = preprocess_data(raw_data)
        assert processed.isnull().sum().sum() == 0  # No nulls after preprocessing
    
    def test_validate_data(self):
        valid_data = pd.DataFrame({
            'feature1': [1.0, 2.0, 3.0],
            'feature2': ['A', 'B', 'C']
        })
        assert validate_data(valid_data) == True
        
        invalid_data = pd.DataFrame({
            'feature1': ['invalid', 2.0, 3.0]
        })
        assert validate_data(invalid_data) == False
```

#### Integration Testing

**API Integration Tests:**
```python
# tests/test_api.py
import pytest
import requests
from fastapi.testclient import TestClient
from src.api import app

client = TestClient(app)

class TestAPI:
    def test_health_endpoint(self):
        response = client.get("/health")
        assert response.status_code == 200
        assert response.json() == {"status": "healthy"}
    
    def test_prediction_endpoint(self):
        test_data = {
            "features": [1.0, 2.0, 3.0, 4.0]
        }
        response = client.post("/predict", json=test_data)
        assert response.status_code == 200
        assert "prediction" in response.json()
    
    def test_prediction_validation(self):
        # Test with invalid data
        invalid_data = {"features": "not_a_list"}
        response = client.post("/predict", json=invalid_data)
        assert response.status_code == 422  # Validation error
```

### 2.3 Continuous Deployment

Automating the deployment process ensures reliable and consistent releases.

#### Staging Deployment Workflow

```yaml
# .github/workflows/deploy-staging.yml
name: Deploy to Staging

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v2
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1
    
    - name: Login to Amazon ECR
      id: login-ecr
      uses: aws-actions/amazon-ecr-login@v1
    
    - name: Build and push Docker image
      env:
        ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
        ECR_REPOSITORY: mlops-app
        IMAGE_TAG: ${{ github.sha }}
      run: |
        docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
        docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
        
    - name: Deploy to ECS
      run: |
        aws ecs update-service --cluster mlops-staging --service mlops-service --force-new-deployment
```

#### Blue-Green Deployment Strategy

**Kubernetes Blue-Green Deployment:**
```yaml
# k8s/blue-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-app-blue
  labels:
    app: ml-app
    version: blue
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ml-app
      version: blue
  template:
    metadata:
      labels:
        app: ml-app
        version: blue
    spec:
      containers:
      - name: ml-app
        image: ml-app:v2.0.0
        ports:
        - containerPort: 8000
---
# k8s/green-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-app-green
  labels:
    app: ml-app
    version: green
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ml-app
      version: green
  template:
    metadata:
      labels:
        app: ml-app
        version: green
    spec:
      containers:
      - name: ml-app
        image: ml-app:v2.1.0
        ports:
        - containerPort: 8000
```

**Service Switching Script:**
```bash
#!/bin/bash
# switch-to-green.sh

# Update service to point to green deployment
kubectl patch service ml-app-service -p '{"spec":{"selector":{"version":"green"}}}'

# Wait for rollout
kubectl rollout status deployment/ml-app-green

# Test the green deployment
curl http://ml-app-service/health

# If successful, scale down blue deployment
kubectl scale deployment ml-app-blue --replicas=0
```

#### Rollback Procedures

**Automated Rollback Workflow:**
```yaml
# .github/workflows/rollback.yml
name: Rollback Deployment

on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Environment to rollback'
        required: true
        default: 'staging'

jobs:
  rollback:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Rollback to previous version
      run: |
        # Get previous successful deployment
        PREVIOUS_TAG=$(git rev-list --tags --skip=1 --max-count=1)
        
        # Deploy previous version
        echo "Rolling back to tag: $PREVIOUS_TAG"
        
        # Add rollback logic here
        # kubectl set image deployment/ml-app ml-app=ml-app:$PREVIOUS_TAG
```

#### Deployment Best Practices

**Health Checks:**
```python
# health_check.py
from fastapi import FastAPI, HTTPException
import time

app = FastAPI()

@app.get("/health")
async def health_check():
    """Comprehensive health check endpoint"""
    health_status = {
        "status": "healthy",
        "timestamp": time.time(),
        "checks": {}
    }
    
    # Database connectivity check
    try:
        # db.check_connection()
        health_status["checks"]["database"] = "healthy"
    except Exception as e:
        health_status["checks"]["database"] = f"unhealthy: {str(e)}"
        health_status["status"] = "unhealthy"
    
    # Model loading check
    try:
        # model.check_loaded()
        health_status["checks"]["model"] = "healthy"
    except Exception as e:
        health_status["checks"]["model"] = f"unhealthy: {str(e)}"
        health_status["status"] = "unhealthy"
    
    # Memory usage check
    import psutil
    memory_percent = psutil.virtual_memory().percent
    if memory_percent > 90:
        health_status["checks"]["memory"] = f"critical: {memory_percent}%"
        health_status["status"] = "unhealthy"
    else:
        health_status["checks"]["memory"] = f"healthy: {memory_percent}%"
    
    if health_status["status"] != "healthy":
        raise HTTPException(status_code=503, detail=health_status)
    
    return health_status
```

**Monitoring Deployment Success:**
```yaml
# .github/workflows/monitor-deployment.yml
name: Monitor Deployment

on:
  workflow_run:
    workflows: ["Deploy to Staging"]
    types:
      - completed

jobs:
  monitor:
    runs-on: ubuntu-latest
    
    steps:
    - name: Check deployment status
      run: |
        # Wait for deployment to be ready
        timeout 300 bash -c 'while [[ "$(curl -s -o /dev/null -w ''%{http_code}'' http://staging-api/health)" != "200" ]]; do sleep 10; done' || exit 1
        
        echo "Deployment successful!"
        
    - name: Run smoke tests
      run: |
        # Run basic functionality tests
        curl -X POST http://staging-api/predict -H "Content-Type: application/json" -d '{"features": [1,2,3,4]}'
        
    - name: Notify on success
      if: success()
      uses: 8398a7/action-slack-notification@v3
      with:
        status: success
        text: "Staging deployment completed successfully"
      
    - name: Notify on failure
      if: failure()
      uses: 8398a7/action-slack-notification@v3
      with:
        status: failure
        text: "Staging deployment failed - manual intervention required"
```

## 3. Containerization

### 3.1 Docker Fundamentals

#### What is Containerization?

**Containerization** is a lightweight form of virtualization that allows applications to run in isolated environments called containers. Containers package an application and its dependencies into a standardized unit that can run consistently across different computing environments.

**Key Characteristics**:
- **Isolation**: Each container runs in its own isolated environment
- **Portability**: Containers can run on any system that supports the container runtime
- **Lightweight**: Containers share the host OS kernel, making them more efficient than virtual machines
- **Immutable**: Container images are read-only and produce consistent results

**Why Containerization Matters in MLOps**:
- **Environment Consistency**: Eliminates "works on my machine" problems
- **Dependency Management**: Packages all dependencies with the application
- **Scalability**: Easy to scale containerized applications horizontally
- **Version Control**: Container images can be versioned and stored in registries
- **Security**: Containers provide process isolation and resource limits

#### Docker Architecture

**Docker Engine Components**:
- **Docker Daemon**: Background service that manages containers, images, networks, and volumes
- **Docker CLI**: Command-line interface for interacting with Docker
- **Docker Registry**: Storage and distribution system for Docker images
- **Container Runtime**: Low-level component that runs containers (runC, containerd)

**Docker Objects**:
- **Images**: Read-only templates containing application code and dependencies
- **Containers**: Runnable instances of images
- **Networks**: Communication channels between containers
- **Volumes**: Persistent data storage for containers
- **Services**: Define how containers should run in production (Docker Swarm)

#### Basic Dockerfile for ML Applications

**Simple ML Application Dockerfile:**
```dockerfile
# Use Python 3.9 slim image as base
FROM python:3.9-slim

# Set working directory inside container
WORKDIR /app

# Install system dependencies required for ML libraries
RUN apt-get update && apt-get install -y \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements first for better Docker layer caching
COPY requirements.txt .

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy application source code
COPY . .

# Create non-root user for security
RUN useradd --create-home --shell /bin/bash app \
    && chown -R app:app /app
USER app

# Expose port for web service
EXPOSE 8000

# Health check to verify container is running properly
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

# Command to run the application
CMD ["python", "app.py"]
```

**Requirements.txt:**
```
fastapi==0.104.1
uvicorn[standard]==0.24.0
scikit-learn==1.3.2
pandas==2.1.3
numpy==1.26.2
joblib==1.3.2
pydantic==2.5.0
```

**Dockerfile Best Practices**:
- **Use specific base images**: Pin versions (e.g., `python:3.9-slim` not `python:latest`)
- **Minimize image size**: Use multi-stage builds and remove unnecessary files
- **Layer optimization**: Order commands to maximize Docker layer caching
- **Security**: Run as non-root user and include health checks
- **Documentation**: Add comments explaining complex operations

#### Advanced Dockerfile Techniques

**Multi-stage Builds for ML Models:**
Multi-stage builds allow you to use different base images for building and running your application, resulting in smaller final images.

```dockerfile
# Build stage - larger image with build tools
FROM python:3.9-slim as builder

WORKDIR /build

# Install build dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    git \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements for caching
COPY requirements.txt .

# Install all dependencies (including dev dependencies)
RUN pip install --user -r requirements.txt

# Copy source code
COPY . .

# Production stage - smaller runtime image
FROM python:3.9-slim as production

# Install only runtime dependencies
RUN apt-get update && apt-get install -y \
    libgomp1 \
    && rm -rf /var/lib/apt/lists/*

# Create app user
RUN useradd --create-home --shell /bin/bash app

# Copy installed packages from builder stage
COPY --from=builder /root/.local /home/app/.local

# Copy application code
COPY --from=builder /build/src /app/src
COPY --from=builder /build/models /app/models

# Set proper permissions
RUN chown -R app:app /app /home/app/.local

# Set environment
ENV PATH=/home/app/.local/bin:$PATH
USER app
WORKDIR /app

# Expose port
EXPOSE 8000

# Health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
    CMD python -c "import requests; requests.get('http://localhost:8000/health')"

# Run application
CMD ["uvicorn", "src.app:app", "--host", "0.0.0.0", "--port", "8000"]
```

**Benefits of Multi-stage Builds**:
- **Smaller Images**: Final image contains only runtime dependencies
- **Security**: Build tools and source code not present in final image
- **Build Optimization**: Separate build and runtime environments
- **Caching**: Better layer caching for faster rebuilds

#### Docker Image Optimization

**Layer Caching Strategies:**
```dockerfile
# Bad - requirements installed after copying all code
FROM python:3.9-slim
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt  # Changes to any file invalidate cache

# Good - requirements installed before copying code
FROM python:3.9-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt  # Only invalidated when requirements change
COPY . .
```

**Image Size Optimization:**
```dockerfile
# Use smaller base images
FROM python:3.9-slim instead of python:3.9

# Combine RUN commands to reduce layers
RUN apt-get update && apt-get install -y \
    package1 \
    package2 \
    && rm -rf /var/lib/apt/lists/*  # Clean up in same layer

# Use .dockerignore to exclude unnecessary files
# .dockerignore
.git
__pycache__
*.pyc
.pytest_cache
tests/
docs/
```

### 3.2 Multi-stage Builds for ML

#### ML-Specific Containerization Challenges

**Large Model Files**: ML models can be hundreds of MB to GB in size
**GPU Dependencies**: GPU-enabled containers require specific base images
**Data Dependencies**: Training data and model artifacts need efficient handling
**Library Conflicts**: Different ML frameworks may have conflicting dependencies

#### GPU-Enabled Containers

**NVIDIA Docker for GPU Support:**
```dockerfile
# Use NVIDIA CUDA base image
FROM nvidia/cuda:11.8-runtime-ubuntu20.04

# Install Python and pip
RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    && rm -rf /var/lib/apt/lists/*

# Install ML libraries with GPU support
RUN pip install --no-cache-dir \
    torch==2.0.1+cu118 \
    torchvision==0.15.2+cu118 \
    torchaudio==2.0.1 \
    --index-url https://download.pytorch.org/whl/cu118

# Copy application
COPY . /app
WORKDIR /app

# Run with GPU access
CMD ["python", "train_gpu.py"]
```

**Running GPU Containers:**
```bash
# Run with GPU access
docker run --gpus all nvidia-ml-app

# Run with specific GPU
docker run --gpus device=0 nvidia-ml-app

# Run with GPU capabilities check
docker run --rm --gpus all nvidia/cuda:11.8-base nvidia-smi
```

#### Model Packaging Strategies

**Model-in-Image Approach:**
```dockerfile
# Multi-stage build with model training and packaging
FROM python:3.9-slim as trainer

WORKDIR /train

# Install training dependencies
COPY requirements-train.txt .
RUN pip install -r requirements-train.txt

# Copy training code and data
COPY src/train.py .
COPY data/ ./data/

# Train model
RUN python train.py

# Save model artifacts
RUN mkdir /models && cp *.pkl /models/

# Production stage
FROM python:3.9-slim as production

COPY --from=trainer /models /app/models
COPY requirements-serve.txt .
RUN pip install -r requirements-serve.txt

COPY src/serve.py .

CMD ["python", "serve.py"]
```

**Model-Volume Approach:**
```dockerfile
# Container expects model to be mounted as volume
FROM python:3.9-slim

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY src/app.py .

# Model will be mounted at runtime
VOLUME ["/models"]

CMD ["python", "app.py"]
```

**Running with Model Volume:**
```bash
# Mount model directory
docker run -v /host/models:/models ml-app

# Use named volume
docker run -v model_data:/models ml-app
```

### 3.3 Docker Compose for ML Stacks

#### What is Docker Compose?

**Docker Compose** is a tool for defining and running multi-container Docker applications. It uses YAML files to configure application services and performs the creation and start of all the services from the configuration.

**Key Benefits**:
- **Service Definition**: Define complex applications as services
- **Dependency Management**: Specify service dependencies and startup order
- **Environment Management**: Different configurations for development and production
- **Networking**: Automatic service discovery and networking
- **Volume Management**: Persistent data management across containers

#### ML Stack with Docker Compose

**Complete ML Development Stack:**
```yaml
# docker-compose.yml
version: '3.8'

services:
  # ML API Service
  ml-api:
    build:
      context: .
      dockerfile: Dockerfile.api
    ports:
      - "8000:8000"
    volumes:
      - ./models:/app/models:ro
      - ./src:/app/src:ro
    environment:
      - MODEL_PATH=/app/models/model.pkl
      - LOG_LEVEL=INFO
    depends_on:
      - redis
      - postgres
    networks:
      - ml-network
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:8000/health"]
      interval: 30s
      timeout: 10s
      retries: 3

  # Training Service
  ml-trainer:
    build:
      context: .
      dockerfile: Dockerfile.train
    volumes:
      - ./data:/app/data:ro
      - ./models:/app/models
      - ./src:/app/src:ro
    environment:
      - DATA_PATH=/app/data
      - MODEL_OUTPUT_PATH=/app/models
    depends_on:
      postgres:
        condition: service_healthy
    networks:
      - ml-network
    profiles:
      - train  # Only start when training

  # Database
  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: mlops
      POSTGRES_USER: mlops
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    ports:
      - "5432:5432"
    networks:
      - ml-network
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U mlops"]
      interval: 10s
      timeout: 5s
      retries: 5

  # Cache
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    networks:
      - ml-network
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 3s
      retries: 3

  # Monitoring
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - prometheus_data:/prometheus
    networks:
      - ml-network
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'

  # Grafana
  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    volumes:
      - grafana_data:/var/lib/grafana
      - ./monitoring/grafana/provisioning:/etc/grafana/provisioning:ro
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    networks:
      - ml-network
    depends_on:
      - prometheus

volumes:
  postgres_data:
  redis_data:
  prometheus_data:
  grafana_data:

networks:
  ml-network:
    driver: bridge
```

#### Environment-Specific Configurations

**Development Override:**
```yaml
# docker-compose.override.yml (automatically merged with docker-compose.yml)
version: '3.8'

services:
  ml-api:
    environment:
      - LOG_LEVEL=DEBUG
      - DEBUG=true
    volumes:
      - ./src:/app/src  # Mount source for live reload

  postgres:
    ports:
      - "5432:5432"  # Expose for local development
```

**Production Override:**
```yaml
# docker-compose.prod.yml
version: '3.8'

services:
  ml-api:
    deploy:
      replicas: 3
      resources:
        limits:
          cpus: '1.0'
          memory: 1G
        reservations:
          cpus: '0.5'
          memory: 512M
      restart_policy:
        condition: on-failure

  postgres:
    deploy:
      placement:
        constraints:
          - node.role == manager
```

#### Docker Compose Commands

**Common Commands:**
```bash
# Start all services
docker-compose up -d

# Start specific services
docker-compose up ml-api postgres -d

# Start with training profile
docker-compose --profile train up ml-trainer

# View logs
docker-compose logs -f ml-api

# Execute commands in running containers
docker-compose exec ml-api bash

# Stop and remove containers
docker-compose down

# Remove volumes as well
docker-compose down -v

# Rebuild and restart
docker-compose up --build --force-recreate
```

#### Networking in Docker Compose

**Service Discovery:**
Services can communicate using service names as hostnames:
```python
# In ml-api container, connect to postgres
import psycopg2

conn = psycopg2.connect(
    host="postgres",  # Service name becomes hostname
    database="mlops",
    user="mlops",
    password="password"
)
```

**Network Isolation:**
```yaml
# Separate networks for different concerns
networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge
    internal: true  # No external access

services:
  web:
    networks:
      - frontend
  api:
    networks:
      - frontend
      - backend
  db:
    networks:
      - backend
```

This comprehensive containerization section provides the foundation for packaging, distributing, and running ML applications consistently across different environments.

# Copy and install Python dependencies
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt

# Copy source code
COPY src/ ./src/

# Train model (if needed during build)
RUN python -c "from src.train import train_model; train_model()"

# Production stage
FROM python:3.9-slim

# Install only runtime dependencies
RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Copy installed packages from builder
COPY --from=builder /root/.local /root/.local

# Copy trained models and source code
COPY --from=builder /build/models ./models
COPY src/ ./src/

# Add local bin to PATH
ENV PATH=/root/.local/bin:$PATH

# Create non-root user
RUN useradd --create-home --shell /bin/bash app \
    && chown -R app:app /app
USER app

EXPOSE 8000

HEALTHCHECK --interval=30s --timeout=10s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

CMD ["uvicorn", "src.api:app", "--host", "0.0.0.0", "--port", "8000"]
```

#### Docker Image Optimization

**Minimize Image Size:**
```dockerfile
# Use Alpine Linux for smaller images
FROM python:3.9-alpine

# Install only necessary packages
RUN apk add --no-cache \
    build-base \
    linux-headers \
    && pip install --no-cache-dir -r requirements.txt \
    && apk del build-base linux-headers

# Use .dockerignore
# .dockerignore
**/__pycache__
**/*.pyc
**/*.pyo
**/*.pyd
**/.Python
**/env
**/venv
**/.env
.git
.gitignore
README.md
docs/
tests/
```

### 3.2 Multi-stage Builds for ML

Multi-stage builds are essential for optimizing ML container images, separating build-time dependencies from runtime.

#### ML Training and Serving Separation

**Training Image:**
```dockerfile
FROM python:3.9-slim as trainer

WORKDIR /train

# Install ML training dependencies
COPY requirements-train.txt .
RUN pip install --no-cache-dir -r requirements-train.txt

# Copy training code and data
COPY src/train.py .
COPY data/ ./data/

# Run training
RUN python train.py

# Save model artifacts
RUN mkdir -p /models && cp *.pkl /models/

# Serving image (much smaller)
FROM python:3.9-slim

WORKDIR /app

# Install only serving dependencies
COPY requirements-serve.txt .
RUN pip install --no-cache-dir -r requirements-serve.txt

# Copy trained model from trainer stage
COPY --from=trainer /models ./models

# Copy serving code
COPY src/serve.py .

EXPOSE 8000

CMD ["python", "serve.py"]
```

#### GPU-Enabled ML Containers

**NVIDIA GPU Dockerfile:**
```dockerfile
FROM nvidia/cuda:11.8-runtime-ubuntu20.04

# Install Python and pip
RUN apt-get update && apt-get install -y \
    python3.9 \
    python3.9-pip \
    && rm -rf /var/lib/apt/lists/*

# Set Python path
ENV PYTHONPATH=/usr/bin/python3.9

# Install ML libraries with GPU support
RUN pip install --no-cache-dir \
    torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118 \
    tensorflow[and-cuda]==2.13.0 \
    scikit-learn \
    pandas \
    numpy

WORKDIR /app

COPY src/ ./src/
COPY models/ ./models/

EXPOSE 8000

CMD ["python", "src/gpu_inference.py"]
```

### 3.3 Docker Compose for ML Stacks

Docker Compose orchestrates multi-container ML applications locally and in development environments.

#### Complete ML Stack with Compose

**docker-compose.yml:**
```yaml
version: '3.8'

services:
  ml-api:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "8000:8000"
    environment:
      - MODEL_PATH=/models/model.pkl
      - REDIS_URL=redis://redis:6379
    depends_on:
      - redis
      - postgres
    volumes:
      - ./models:/models:ro
    networks:
      - ml-network
    restart: unless-stopped

  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    networks:
      - ml-network
    restart: unless-stopped

  postgres:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: mlops
      POSTGRES_USER: mlops
      POSTGRES_PASSWORD: password
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data
    networks:
      - ml-network
    restart: unless-stopped

  mlflow:
    image: ghcr.io/mlflow/mlflow:v2.8.1
    ports:
      - "5000:5000"
    environment:
      - MLFLOW_BACKEND_STORE_URI=postgresql://mlops:password@postgres/mlops
      - MLFLOW_ARTIFACT_STORE_URI=file:/mlruns
    depends_on:
      - postgres
    volumes:
      - mlflow_data:/mlruns
    networks:
      - ml-network
    command: mlflow server --host 0.0.0.0 --port 5000

  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - prometheus_data:/prometheus
    networks:
      - ml-network
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
    volumes:
      - grafana_data:/var/lib/grafana
    networks:
      - ml-network
    restart: unless-stopped

volumes:
  redis_data:
  postgres_data:
  mlflow_data:
  prometheus_data:
  grafana_data:

networks:
  ml-network:
    driver: bridge
```

#### Environment-Specific Configurations

**Development Override:**
```yaml
# docker-compose.dev.yml
version: '3.8'

services:
  ml-api:
    build:
      context: .
      dockerfile: Dockerfile.dev
    environment:
      - DEBUG=true
      - LOG_LEVEL=DEBUG
    volumes:
      - .:/app
      - /app/__pycache__
```

**Production Override:**
```yaml
# docker-compose.prod.yml
version: '3.8'

services:
  ml-api:
    image: myregistry.com/ml-api:latest
    environment:
      - DEBUG=false
      - LOG_LEVEL=INFO
    deploy:
      replicas: 3
      resources:
        limits:
          cpus: '1.0'
          memory: 1G
        reservations:
          cpus: '0.5'
          memory: 512M
```

#### Docker Compose Commands

**Development Workflow:**
```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f ml-api

# Run tests in container
docker-compose exec ml-api python -m pytest tests/

# Scale services
docker-compose up -d --scale ml-api=3

# Stop and remove everything
docker-compose down -v
```

#### Networking and Service Discovery

**Service Communication:**
```python
# src/api.py
import os
import redis
import psycopg2
from fastapi import FastAPI

app = FastAPI()

# Connect to Redis (service name from compose)
redis_client = redis.Redis(host='redis', port=6379, decode_responses=True)

# Connect to PostgreSQL
db_conn = psycopg2.connect(
    host="postgres",
    database="mlops",
    user="mlops",
    password="password"
)

@app.get("/cache/{key}")
async def get_cache(key: str):
    value = redis_client.get(key)
    return {"key": key, "value": value}

@app.get("/experiments")
async def get_experiments():
    cursor = db_conn.cursor()
    cursor.execute("SELECT * FROM experiments LIMIT 10")
    results = cursor.fetchall()
    cursor.close()
    return {"experiments": results}
```

#### Volume Management for ML Data

**Data Persistence:**
```yaml
# docker-compose.yml (data volumes)
services:
  ml-training:
    build: .
    volumes:
      - ./data:/app/data:ro          # Read-only data
      - ./models:/app/models         # Read-write models
      - ./artifacts:/app/artifacts   # Training artifacts
    environment:
      - DATA_PATH=/app/data
      - MODEL_OUTPUT_PATH=/app/models

volumes:
  training_data:
    driver: local
    driver_opts:
      o: bind
      type: none
      device: /host/path/to/data
```

**Model Artifact Management:**
```python
# src/train.py
import os
import joblib
from datetime import datetime

MODEL_DIR = os.getenv('MODEL_OUTPUT_PATH', './models')
ARTIFACTS_DIR = os.getenv('ARTIFACTS_DIR', './artifacts')

def save_model(model, model_name):
    """Save model with timestamp"""
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    model_path = f"{MODEL_DIR}/{model_name}_{timestamp}.pkl"
    
    os.makedirs(MODEL_DIR, exist_ok=True)
    joblib.dump(model, model_path)
    
    # Create symlink to latest model
    latest_path = f"{MODEL_DIR}/{model_name}_latest.pkl"
    if os.path.exists(latest_path):
        os.remove(latest_path)
    os.symlink(os.path.basename(model_path), latest_path)
    
    return model_path
```

#### Security Best Practices

**Non-root Containers:**
```dockerfile
FROM python:3.9-slim

# Create non-root user
RUN groupadd -r mluser && useradd -r -g mluser mluser

# Set working directory with correct permissions
WORKDIR /app
RUN chown mluser:mluser /app

# Switch to non-root user
USER mluser

# Your application code here
```

**Secrets Management:**
```yaml
# docker-compose.yml
services:
  ml-api:
    environment:
      - DB_PASSWORD_FILE=/run/secrets/db_password
    secrets:
      - db_password

secrets:
  db_password:
    file: ./secrets/db_password.txt
```

**Image Security Scanning:**
```yaml
# .github/workflows/security-scan.yml
name: Security Scan

on:
  push:
    branches: [ main ]

jobs:
  scan:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Build Docker image
      run: docker build -t ml-app .
    
    - name: Scan image for vulnerabilities
      uses: aquasecurity/trivy-action@master
      with:
        scan-type: 'image'
        scan-ref: 'ml-app'
        format: 'sarif'
        output: 'trivy-results.sarif'
    
    - name: Upload Trivy scan results
      uses: github/codeql-action/upload-sarif@v2
      if: always()
      with:
        sarif_file: 'trivy-results.sarif'
```

## 4. Orchestration and Scaling

### 4.1 Kubernetes Basics

#### What is Container Orchestration?

**Container Orchestration** is the automated management, coordination, and scheduling of containers across a cluster of machines. It handles container deployment, scaling, networking, and lifecycle management.

**Key Problems Orchestration Solves**:
- **Service Discovery**: How do containers find and communicate with each other?
- **Load Balancing**: How to distribute traffic across multiple container instances?
- **Scaling**: How to automatically adjust the number of running containers?
- **Fault Tolerance**: How to handle container failures and ensure high availability?
- **Resource Management**: How to allocate CPU, memory, and storage efficiently?

#### Kubernetes Architecture

**Kubernetes (K8s)** is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

**Core Components**:

**Control Plane**:
- **API Server**: Frontend for the Kubernetes control plane
- **etcd**: Distributed key-value store for cluster state
- **Scheduler**: Assigns pods to nodes based on resource requirements
- **Controller Manager**: Runs controller processes (replication, endpoints, etc.)

**Worker Nodes**:
- **Kubelet**: Agent that runs on each node, ensures containers are running
- **Container Runtime**: Software for running containers (Docker, containerd)
- **Kube Proxy**: Network proxy that maintains network rules on nodes

**Key Concepts**:

**Pods**: Smallest deployable unit in Kubernetes, containing one or more containers
**Deployments**: Declarative way to manage pod replicas and updates
**Services**: Abstraction that defines a logical set of pods and policy for accessing them
**Namespaces**: Virtual clusters within a physical cluster for resource isolation

#### Core Kubernetes Objects for ML

**Pods:**
A Pod is the basic execution unit in Kubernetes. It represents a single instance of a running process in the cluster.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: ml-training-pod
  labels:
    app: ml-trainer
    version: v1.0
spec:
  containers:
  - name: ml-trainer
    image: ml-trainer:latest
    command: ["python", "train.py"]
    resources:
      requests:
        memory: "2Gi"
        cpu: "1000m"
        nvidia.com/gpu: 1  # GPU request
      limits:
        memory: "4Gi"
        cpu: "2000m"
        nvidia.com/gpu: 1
    volumeMounts:
    - name: model-storage
      mountPath: /models
    - name: data-storage
      mountPath: /data
  volumes:
  - name: model-storage
    persistentVolumeClaim:
      claimName: model-pvc
  - name: data-storage
    persistentVolumeClaim:
      claimName: data-pvc
  restartPolicy: Never
```

**Deployments:**
A Deployment provides declarative updates for Pods and ReplicaSets. It manages the desired state of your application.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api-deployment
  labels:
    app: ml-api
spec:
  replicas: 3  # Number of pod replicas
  selector:
    matchLabels:
      app: ml-api
  template:
    metadata:
      labels:
        app: ml-api
    spec:
      containers:
      - name: ml-api
        image: ml-api:v1.0.0
        ports:
        - containerPort: 8000
        resources:
          requests:
            memory: "256Mi"
            cpu: "250m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        # Liveness probe for container health
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        # Readiness probe for traffic routing
        readinessProbe:
          httpGet:
            path: /ready
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
          timeoutSeconds: 3
        env:
        - name: MODEL_PATH
          value: "/models/model.pkl"
        volumeMounts:
        - name: model-storage
          mountPath: /models
      volumes:
      - name: model-storage
        persistentVolumeClaim:
          claimName: model-pvc
```

**Services:**
A Service is an abstraction that defines a logical set of Pods and a policy for accessing them.

```yaml
# ClusterIP Service (internal access)
apiVersion: v1
kind: Service
metadata:
  name: ml-api-service
spec:
  selector:
    app: ml-api
  ports:
  - port: 80
    targetPort: 8000
    protocol: TCP
  type: ClusterIP

---
# LoadBalancer Service (external access)
apiVersion: v1
kind: Service
metadata:
  name: ml-api-external
spec:
  selector:
    app: ml-api
  ports:
  - port: 80
    targetPort: 8000
    protocol: TCP
  type: LoadBalancer
  loadBalancerIP: "10.0.0.100"  # Optional static IP
```

#### Configuration Management

**ConfigMaps:**
ConfigMaps allow you to decouple configuration artifacts from image content to keep containerized applications portable.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: ml-api-config
  namespace: ml-production
data:
  # Configuration values
  LOG_LEVEL: "INFO"
  MODEL_PATH: "/models/model.pkl"
  MAX_WORKERS: "4"
  BATCH_SIZE: "32"
  # Configuration files
  app-config.yaml: |
    database:
      host: postgres-service
      port: 5432
      name: mlops
    redis:
      host: redis-service
      port: 6379
    monitoring:
      prometheus_url: http://prometheus:9090
```

**Using ConfigMaps in Pods:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api-deployment
spec:
  template:
    spec:
      containers:
      - name: ml-api
        image: ml-api:latest
        env:
        - name: LOG_LEVEL
          valueFrom:
            configMapKeyRef:
              name: ml-api-config
              key: LOG_LEVEL
        - name: CONFIG_FILE
          value: /config/app-config.yaml
        volumeMounts:
        - name: config-volume
          mountPath: /config
      volumes:
      - name: config-volume
        configMap:
          name: ml-api-config
```

**Secrets:**
Secrets are similar to ConfigMaps but specifically for sensitive data like passwords, tokens, and keys.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: ml-api-secrets
  namespace: ml-production
type: Opaque
data:
  # Base64 encoded values
  database-password: cGFzc3dvcmQ=  # "password" base64 encoded
  api-key: YXBpX2tleQ==           # "api_key" base64 encoded
  tls.crt: LS0tLS1CRUdJTi...     # Certificate data
  tls.key: LS0tLS1CRUdJTi...     # Private key data

---
# Using secrets in pods
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api-deployment
spec:
  template:
    spec:
      containers:
      - name: ml-api
        env:
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: ml-api-secrets
              key: database-password
        volumeMounts:
        - name: tls-certs
          mountPath: /etc/ssl/certs
          readOnly: true
      volumes:
      - name: tls-certs
        secret:
          secretName: ml-api-secrets
          items:
          - key: tls.crt
            path: tls.crt
          - key: tls.key
            path: tls.key
```

### 4.2 Helm Charts for ML Applications

#### What is Helm?

**Helm** is the package manager for Kubernetes. It helps you define, install, and upgrade complex Kubernetes applications.

**Key Concepts**:
- **Charts**: Packages of pre-configured Kubernetes resources
- **Repositories**: Collections of charts that can be searched and downloaded
- **Releases**: Instances of charts running in a Kubernetes cluster

**Why Helm for ML Applications**:
- **Templating**: Parameterize Kubernetes manifests
- **Versioning**: Manage chart versions and rollbacks
- **Dependencies**: Manage complex application dependencies
- **Sharing**: Distribute and reuse ML application configurations

#### Creating ML Application Charts

**Chart Structure:**
```
ml-api-chart/
├── Chart.yaml          # Chart metadata
├── values.yaml         # Default configuration values
├── templates/          # Kubernetes manifest templates
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── configmap.yaml
│   ├── _helpers.tpl    # Template helpers
├── charts/             # Dependencies
└── .helmignore         # Files to ignore
```

**Chart.yaml:**
```yaml
apiVersion: v2
name: ml-api
description: A Helm chart for ML API deployment
type: application
version: 1.0.0
appVersion: "1.0.0"
keywords:
  - ml
  - api
  - machine-learning
home: https://github.com/your-org/ml-api
sources:
  - https://github.com/your-org/ml-api
maintainers:
  - name: ML Team
    email: ml-team@company.com
dependencies:
  - name: postgresql
    version: "12.x.x"
    repository: "https://charts.bitnami.com/bitnami"
    condition: postgresql.enabled
  - name: redis
    version: "17.x.x"
    repository: "https://charts.bitnami.com/bitnami"
    condition: redis.enabled
```

**values.yaml:**
```yaml
# Default values for ml-api
replicaCount: 3

image:
  repository: your-registry/ml-api
  tag: "latest"
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80
  targetPort: 8000

resources:
  requests:
    memory: "256Mi"
    cpu: "250m"
  limits:
    memory: "512Mi"
    cpu: "500m"

config:
  logLevel: INFO
  modelPath: /models/model.pkl
  maxWorkers: 4

postgresql:
  enabled: true
  auth:
    database: mlops
    username: mlops
    password: "changeMe123"

redis:
  enabled: true
  auth:
    password: "changeMe123"

ingress:
  enabled: false
  className: ""
  annotations: {}
  hosts:
    - host: ml-api.local
      paths:
        - path: /
          pathType: Prefix
  tls: []
```

**Deployment Template:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "ml-api.fullname" . }}
  labels:
    {{- include "ml-api.labels" . | nindent 4 }}
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      {{- include "ml-api.selectorLabels" . | nindent 6 }}
  template:
    metadata:
      labels:
        {{- include "ml-api.selectorLabels" . | nindent 8 }}
    spec:
      containers:
      - name: ml-api
        image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
        imagePullPolicy: {{ .Values.image.pullPolicy }}
        ports:
        - containerPort: 8000
          name: http
        env:
        - name: LOG_LEVEL
          value: {{ .Values.config.logLevel | quote }}
        - name: MODEL_PATH
          value: {{ .Values.config.modelPath | quote }}
        - name: MAX_WORKERS
          value: {{ .Values.config.maxWorkers | quote }}
        {{- if .Values.postgresql.enabled }}
        - name: DATABASE_URL
          value: postgresql://{{ .Values.postgresql.auth.username }}:{{ .Values.postgresql.auth.password }}@{{ include "ml-api.fullname" . }}-postgresql:5432/{{ .Values.postgresql.auth.database }}
        {{- end }}
        {{- if .Values.redis.enabled }}
        - name: REDIS_URL
          value: redis://{{ include "ml-api.fullname" . }}-redis:6379
        {{- end }}
        resources:
          {{- toYaml .Values.resources | nindent 12 }}
        livenessProbe:
          httpGet:
            path: /health
            port: http
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: http
          initialDelaySeconds: 5
          periodSeconds: 5
        volumeMounts:
        - name: model-storage
          mountPath: /models
      volumes:
      - name: model-storage
        persistentVolumeClaim:
          claimName: {{ include "ml-api.fullname" . }}-model-pvc
```

**Helper Templates (_helpers.tpl):**
```yaml
{{/*
Expand the name of the chart.
*/}}
{{- define "ml-api.name" -}}
{{- default .Chart.Name .Values.nameOverride | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/*
Create a default fully qualified app name.
*/}}
{{- define "ml-api.fullname" -}}
{{- if .Values.fullnameOverride }}
{{- .Values.fullnameOverride | trunc 63 | trimSuffix "-" }}
{{- else }}
{{- $name := default .Chart.Name .Values.nameOverride }}
{{- if contains $name .Release.Name }}
{{- .Release.Name | trunc 63 | trimSuffix "-" }}
{{- else }}
{{- printf "%s-%s" .Release.Name $name | trunc 63 | trimSuffix "-" }}
{{- end }}
{{- end }}
{{- end }}

{{/*
Create chart name and version as used by the chart label.
*/}}
{{- define "ml-api.chart" -}}
{{- printf "%s-%s" .Chart.Name .Chart.Version | replace "+" "_" | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/*
Common labels
*/}}
{{- define "ml-api.labels" -}}
helm.sh/chart: {{ include "ml-api.chart" . }}
{{ include "ml-api.selectorLabels" . }}
{{- if .Chart.AppVersion }}
app.kubernetes.io/version: {{ .Chart.AppVersion | quote }}
{{- end }}
app.kubernetes.io/managed-by: {{ .Release.Service }}
{{- end }}

{{/*
Selector labels
*/}}
{{- define "ml-api.selectorLabels" -}}
app.kubernetes.io/name: {{ include "ml-api.name" . }}
app.kubernetes.io/instance: {{ .Release.Name }}
{{- end }}
```

#### Using Helm Charts

**Installing Charts:**
```bash
# Install chart with default values
helm install ml-api ./ml-api-chart

# Install with custom values
helm install ml-api ./ml-api-chart -f custom-values.yaml

# Install from repository
helm repo add my-repo https://charts.mycompany.com
helm install ml-api my-repo/ml-api

# List installed releases
helm list

# Upgrade release
helm upgrade ml-api ./ml-api-chart

# Rollback release
helm rollback ml-api 1

# Uninstall release
helm uninstall ml-api
```

### 4.3 Auto-scaling and Load Balancing

#### Horizontal Pod Autoscaling (HPA)

**What is HPA?**
Horizontal Pod Autoscaling automatically scales the number of pods in a deployment based on observed CPU utilization or custom metrics.

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: ml-api-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: ml-api-deployment
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
        target:
          type: Utilization
          averageUtilization: 80
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
    scaleUp:
      stabilizationWindowSeconds: 60
      policies:
      - type: Percent
        value: 100
        periodSeconds: 60
```

**Custom Metrics Autoscaling:**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: ml-api-custom-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: ml-api-deployment
  minReplicas: 1
  maxReplicas: 20
  metrics:
  - type: Pods
    pods:
      metric:
        name: requests_per_second
      target:
        type: AverageValue
        averageValue: 1000m  # 1000 requests per second per pod
  - type: Object
    object:
      metric:
        name: requests_queue_length
      describedObject:
        apiVersion: v1
        kind: ConfigMap
        name: ml-api-config
      target:
        type: Value
        value: 100
```

#### Load Balancing in Kubernetes

**Service Load Balancing:**
```yaml
# LoadBalancer Service
apiVersion: v1
kind: Service
metadata:
  name: ml-api-loadbalancer
spec:
  selector:
    app: ml-api
  ports:
  - port: 80
    targetPort: 8000
  type: LoadBalancer
  loadBalancerIP: "10.0.0.100"
```

**Ingress for Advanced Routing:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ml-api-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
spec:
  ingressClassName: nginx
  tls:
  - hosts:
    - ml-api.yourcompany.com
    secretName: ml-api-tls
  rules:
  - host: ml-api.yourcompany.com
    http:
      paths:
      - path: /api/v1
        pathType: Prefix
        backend:
          service:
            name: ml-api-service
            port:
              number: 80
      - path: /metrics
        pathType: Exact
        backend:
          service:
            name: prometheus-service
            port:
              number: 9090
```

#### Cluster Autoscaling

**Cluster Autoscaler:**
Automatically adjusts the size of the Kubernetes cluster based on the resource requests of unscheduled pods.

```yaml
# Cluster Autoscaler Deployment (example for AWS)
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cluster-autoscaler
  namespace: kube-system
spec:
  template:
    spec:
      containers:
      - name: cluster-autoscaler
        image: k8s.gcr.io/autoscaling/cluster-autoscaler:v1.26.0
        command:
        - ./cluster-autoscaler
        - --v=4
        - --stderrthreshold=info
        - --cloud-provider=aws
        - --skip-nodes-with-local-storage=false
        - --expander=least-waste
        - --node-group-auto-discovery=asg:tag=k8s.io/cluster-autoscaler/enabled,k8s.io/cluster-autoscaler/your-cluster-name
```

**Node Groups Configuration (AWS):**
```yaml
# Auto Scaling Group Tags
Tags:
  - Key: k8s.io/cluster-autoscaler/enabled
    Value: "true"
  - Key: k8s.io/cluster-autoscaler/your-cluster-name
    Value: ""
  - Key: k8s.io/cluster-autoscaler/node-template/label/k8s.io/cluster-autoscaler/enabled
    Value: "true"
```

This comprehensive orchestration section provides the foundation for deploying and managing ML applications at scale in production environments.
  REDIS_URL: "redis://redis-service:6379"
---
# Secret for sensitive data
apiVersion: v1
kind: Secret
metadata:
  name: ml-api-secrets
type: Opaque
data:
  # Base64 encoded values
  DB_PASSWORD: cGFzc3dvcmQ=  # 'password' base64 encoded
  API_KEY: YXBpX2tleQ==     # 'api_key' base64 encoded
```

**Using ConfigMaps and Secrets in Pods:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api-deployment
spec:
  template:
    spec:
      containers:
      - name: ml-api
        image: ml-api:v1.0.0
        env:
        - name: LOG_LEVEL
          valueFrom:
            configMapKeyRef:
              name: ml-api-config
              key: LOG_LEVEL
        - name: DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: ml-api-secrets
              key: DB_PASSWORD
        envFrom:
        - configMapRef:
            name: ml-api-config
        volumeMounts:
        - name: model-storage
          mountPath: /models
      volumes:
      - name: model-storage
        persistentVolumeClaim:
          claimName: model-pvc
```

### 4.2 Helm Charts for ML Applications

Helm is the package manager for Kubernetes, essential for managing complex ML deployments.

#### Basic Helm Chart Structure

**Chart Directory Structure:**
```
ml-api-chart/
├── Chart.yaml
├── values.yaml
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   ├── _helpers.tpl
│   └── tests/
│       └── test-connection.yaml
└── charts/  # Dependencies
```

**Chart.yaml:**
```yaml
apiVersion: v2
name: ml-api
description: A Helm chart for ML API deployment
type: application
version: 1.0.0
appVersion: "1.0.0"
dependencies:
  - name: postgresql
    version: "12.1.6"
    repository: "https://charts.bitnami.com/bitnami"
  - name: redis
    version: "17.3.3"
    repository: "https://charts.bitnami.com/bitnami"
```

**values.yaml:**
```yaml
# Default values for ml-api
replicaCount: 3

image:
  repository: myregistry.com/ml-api
  tag: "v1.0.0"
  pullPolicy: IfNotPresent

service:
  type: ClusterIP
  port: 80
  targetPort: 8000

resources:
  requests:
    memory: "256Mi"
    cpu: "250m"
  limits:
    memory: "512Mi"
    cpu: "500m"

config:
  logLevel: INFO
  modelPath: /models/model.pkl

secrets:
  dbPassword: ""
  apiKey: ""

postgresql:
  enabled: true
  auth:
    database: mlops
    username: mlops

redis:
  enabled: true
```

**templates/deployment.yaml:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ include "ml-api.fullname" . }}
  labels:
    {{- include "ml-api.labels" . | nindent 4 }}
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      {{- include "ml-api.selectorLabels" . | nindent 6 }}
  template:
    metadata:
      labels:
        {{- include "ml-api.selectorLabels" . | nindent 8 }}
    spec:
      containers:
      - name: ml-api
        image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
        ports:
        - containerPort: 8000
        env:
        - name: LOG_LEVEL
          value: {{ .Values.config.logLevel | quote }}
        - name: MODEL_PATH
          value: {{ .Values.config.modelPath | quote }}
        - name: DB_PASSWORD
          valueFrom:
            secretKey:
              name: {{ include "ml-api.fullname" . }}
              key: db-password
        resources:
          {{- toYaml .Values.resources | nindent 10 }}
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
```

**_helpers.tpl:**
```yaml
{{/*
Expand the name of the chart.
*/}}
{{- define "ml-api.name" -}}
{{- default .Chart.Name .Values.nameOverride | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/*
Create a default fully qualified app name.
*/}}
{{- define "ml-api.fullname" -}}
{{- if .Values.fullnameOverride }}
{{- .Values.fullnameOverride | trunc 63 | trimSuffix "-" }}
{{- else }}
{{- $name := default .Chart.Name .Values.nameOverride }}
{{- if contains $name .Release.Name }}
{{- .Release.Name | trunc 63 | trimSuffix "-" }}
{{- else }}
{{- printf "%s-%s" .Release.Name $name | trunc 63 | trimSuffix "-" }}
{{- end }}
{{- end }}
{{- end }}

{{/*
Create chart name and version as used by the chart label.
*/}}
{{- define "ml-api.chart" -}}
{{- printf "%s-%s" .Chart.Name .Chart.Version | replace "+" "_" | trunc 63 | trimSuffix "-" }}
{{- end }}

{{/*
Common labels
*/}}
{{- define "ml-api.labels" -}}
helm.sh/chart: {{ include "ml-api.chart" . }}
{{ include "ml-api.selectorLabels" . }}
{{- if .Chart.AppVersion }}
app.kubernetes.io/version: {{ .Chart.AppVersion | quote }}
{{- end }}
app.kubernetes.io/managed-by: {{ .Release.Service }}
{{- end }}

{{/*
Selector labels
*/}}
{{- define "ml-api.selectorLabels" -}}
app.kubernetes.io/name: {{ include "ml-api.name" . }}
app.kubernetes.io/instance: {{ .Release.Name }}
{{- end }}
```

#### Installing and Managing Helm Charts

**Installing a Chart:**
```bash
# Add repositories
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

# Install ML API chart
helm install ml-api ./ml-api-chart \
  --set image.tag=v1.1.0 \
  --set replicaCount=5

# Install with custom values
helm install ml-api ./ml-api-chart -f custom-values.yaml

# Install in specific namespace
helm install ml-api ./ml-api-chart -n ml-production
```

**Upgrading and Rolling Back:**
```bash
# Upgrade release
helm upgrade ml-api ./ml-api-chart --set image.tag=v1.2.0

# Check release status
helm status ml-api

# List release history
helm history ml-api

# Rollback to previous version
helm rollback ml-api 1

# Rollback to specific version
helm rollback ml-api 2
```

### 4.3 Auto-scaling and Load Balancing

Auto-scaling ensures your ML applications can handle varying loads efficiently.

#### Horizontal Pod Autoscaling (HPA)

**CPU-based Auto-scaling:**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: ml-api-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: ml-api-deployment
  minReplicas: 3
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
```

**Custom Metrics Auto-scaling:**
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: ml-api-custom-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: ml-api-deployment
  minReplicas: 2
  maxReplicas: 20
  metrics:
  - type: Pods
    pods:
      metric:
        name: requests_per_second
      target:
        type: AverageValue
        averageValue: 100
  - type: Object
    object:
      metric:
        name: requests_queue_length
      describedObject:
        apiVersion: v1
        kind: ConfigMap
        name: ml-api-config
      target:
        type: Value
        value: 10
```

#### Cluster Autoscaling

**AWS EKS Cluster Autoscaler:**
```yaml
# IAM policy for cluster autoscaler
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "autoscaling:DescribeAutoScalingGroups",
                "autoscaling:DescribeAutoScalingInstances",
                "autoscaling:DescribeLaunchConfigurations",
                "autoscaling:DescribeTags",
                "autoscaling:SetDesiredCapacity",
                "autoscaling:TerminateInstanceInAutoScalingGroup",
                "ec2:DescribeLaunchTemplateVersions"
            ],
            "Resource": "*"
        }
    ]
}
```

**Cluster Autoscaler Deployment:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: cluster-autoscaler
  namespace: kube-system
  labels:
    app: cluster-autoscaler
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cluster-autoscaler
  template:
    metadata:
      labels:
        app: cluster-autoscaler
    spec:
      serviceAccountName: cluster-autoscaler
      containers:
      - image: k8s.gcr.io/autoscaling/cluster-autoscaler:v1.26.2
        name: cluster-autoscaler
        command:
        - ./cluster-autoscaler
        - --v=4
        - --stderrthreshold=info
        - --cloud-provider=aws
        - --skip-nodes-with-local-storage=false
        - --expander=least-waste
        - --node-group-auto-discovery=asg:tag=k8s.io/cluster-autoscaler/enabled,k8s.io/cluster-autoscaler/my-cluster
```

#### Load Balancing Strategies

**Kubernetes Service Load Balancing:**
```yaml
# LoadBalancer service
apiVersion: v1
kind: Service
metadata:
  name: ml-api-loadbalancer
  annotations:
    service.beta.kubernetes.io/aws-load-balancer-type: nlb
    service.beta.kubernetes.io/aws-load-balancer-cross-zone-load-balancing-enabled: 'true'
spec:
  type: LoadBalancer
  selector:
    app: ml-api
  ports:
  - port: 80
    targetPort: 8000
    protocol: TCP
```

**Ingress for Advanced Routing:**
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ml-api-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
    nginx.ingress.kubernetes.io/ssl-redirect: "true"
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
spec:
  ingressClassName: nginx
  tls:
  - hosts:
    - api.mlops.example.com
    secretName: ml-api-tls
  rules:
  - host: api.mlops.example.com
    http:
      paths:
      - path: /v1/predict
        pathType: Prefix
        backend:
          service:
            name: ml-api-service
            port:
              number: 80
      - path: /v1/health
        pathType: Prefix
        backend:
          service:
            name: ml-api-service
            port:
              number: 80
```

#### Advanced Scaling Patterns

**Predictive Auto-scaling:**
```python
# predictive_scaler.py
import numpy as np
from datetime import datetime, timedelta
from kubernetes import client, config

class PredictiveScaler:
    def __init__(self, deployment_name, namespace='default'):
        config.load_incluster_config()
        self.apps_v1 = client.AppsV1Api()
        self.deployment_name = deployment_name
        self.namespace = namespace
        
        # Historical data for prediction
        self.request_history = []
        
    def collect_metrics(self):
        """Collect current request metrics"""
        # Implementation to collect metrics from Prometheus
        pass
        
    def predict_load(self, hours_ahead=1):
        """Predict future load using time series analysis"""
        if len(self.request_history) < 24:  # Need at least 24 hours of data
            return None
            
        # Simple moving average prediction
        recent_avg = np.mean(self.request_history[-24:])  # Last 24 hours
        predicted_load = recent_avg * 1.2  # 20% safety margin
        
        return predicted_load
        
    def scale_deployment(self, replicas):
        """Scale deployment to specified number of replicas"""
        # Get current deployment
        deployment = self.apps_v1.read_namespaced_deployment(
            name=self.deployment_name,
            namespace=self.namespace
        )
        
        # Update replicas
        deployment.spec.replicas = replicas
        
        # Apply changes
        self.apps_v1.patch_namespaced_deployment(
            name=self.deployment_name,
            namespace=self.namespace,
            body=deployment
        )
        
        print(f"Scaled {self.deployment_name} to {replicas} replicas")
```

**Multi-region Load Balancing:**
```yaml
# Global load balancer configuration
apiVersion: v1
kind: ConfigMap
metadata:
  name: global-lb-config
data:
  config.yaml: |
    services:
      - name: ml-api
        regions:
          - name: us-east-1
            weight: 60
            health-check: /health
          - name: eu-west-1
            weight: 40
            health-check: /health
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: global-load-balancer
spec:
  replicas: 2
  template:
    spec:
      containers:
      - name: envoy
        image: envoyproxy/envoy:v1.25.0
        ports:
        - containerPort: 80
        - containerPort: 443
        volumeMounts:
        - name: config
          mountPath: /etc/envoy
      volumes:
      - name: config
        configMap:
          name: global-lb-config
```

#### Monitoring Scaling Events

**Scaling Metrics Collection:**
```yaml
# prometheus-rules.yaml
apiVersion: monitoring.coreos.com/v1
kind: PrometheusRule
metadata:
  name: scaling-rules
  namespace: monitoring
spec:
  groups:
  - name: scaling
    rules:
    - alert: HighScalingFrequency
      expr: rate(kube_deployment_spec_replicas[5m]) > 0.1
      for: 10m
      labels:
        severity: warning
      annotations:
        summary: "High scaling frequency detected"
        description: "Deployment {{ $labels.deployment }} is scaling frequently"
        
    - alert: ScalingLimitReached
      expr: kube_deployment_spec_replicas >= kube_deployment_status_replicas_available * 2
      for: 5m
      labels:
        severity: critical
      annotations:
        summary: "Scaling limit reached"
        description: "Deployment {{ $labels.deployment }} has reached scaling limits"
```

**Scaling Dashboard in Grafana:**
```json
{
  "dashboard": {
    "title": "ML Application Scaling Dashboard",
    "panels": [
      {
        "title": "Pod Count Over Time",
        "type": "graph",
        "targets": [
          {
            "expr": "count(kube_pod_info{pod=~\"ml-api-.*\"})",
            "legendFormat": "Total Pods"
          }
        ]
      },
      {
        "title": "CPU Utilization",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(container_cpu_usage_seconds_total{pod=~\"ml-api-.*\"}[5m])",
            "legendFormat": "{{ pod }}"
          }
        ]
      }
    ]
  }
}
```

#### Resource Optimization

**Resource Quotas and Limits:**
```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: ml-namespace-quota
  namespace: ml-production
spec:
  hard:
    requests.cpu: "20"
    requests.memory: 40Gi
    limits.cpu: "40"
    limits.memory: 80Gi
    persistentvolumeclaims: "10"
    pods: "50"
    services: "20"
---
apiVersion: v1
kind: LimitRange
metadata:
  name: ml-container-limits
  namespace: ml-production
spec:
  limits:
  - default:
      cpu: 500m
      memory: 512Mi
    defaultRequest:
      cpu: 100m
      memory: 128Mi
    type: Container
```

**Cost-aware Scaling:**
```python
# cost_aware_scaler.py
class CostAwareScaler:
    def __init__(self, max_daily_cost=100.0):
        self.max_daily_cost = max_daily_cost
        self.instance_pricing = {
            't3.medium': 0.0416,    # per hour
            't3.large': 0.0832,
            'c5.large': 0.096,     # compute optimized
            'm5.large': 0.1152,    # general purpose
        }
        
    def calculate_optimal_scaling(self, current_load, current_instances):
        """Calculate optimal number of instances based on load and cost"""
        # Implementation for cost-aware scaling logic
        pass
        
    def get_spot_instance_recommendation(self):
        """Recommend spot instances for cost savings"""
        # Implementation for spot instance recommendations
        pass
```

This comprehensive approach to orchestration and scaling ensures your ML applications can handle production workloads efficiently while maintaining cost-effectiveness and reliability. The combination of Kubernetes, Helm, and intelligent auto-scaling provides a robust foundation for MLOps at scale.

## 5. Model Management and Serving

### 5.1 MLflow for Experiment Tracking

#### What is MLflow?

**MLflow** is an open-source platform for managing the machine learning lifecycle. It provides tools for tracking experiments, packaging code into reproducible runs, and sharing and deploying models.

**Core Components**:
- **MLflow Tracking**: Record and query experiments (code, data, config, results)
- **MLflow Projects**: Package data science code in a reusable, reproducible format
- **MLflow Models**: Deploy machine learning models in diverse serving environments
- **MLflow Registry**: Store, annotate, discover, and manage models in a central repository

**Why MLflow for MLOps**:
- **Experiment Reproducibility**: Track all aspects of ML experiments
- **Model Versioning**: Manage different versions of trained models
- **Deployment Ready**: Package models for easy deployment
- **Collaboration**: Share experiments and models across teams
- **Integration**: Works with popular ML frameworks (scikit-learn, TensorFlow, PyTorch)

#### Setting Up MLflow

**Local MLflow Server:**
```bash
# Install MLflow
pip install mlflow

# Start MLflow server with local backend
mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root ./artifacts --host 0.0.0.0 --port 5000

# Or use Docker
docker run -p 5000:5000 -v $(pwd)/mlruns:/mlruns ghcr.io/mlflow/mlflow server --backend-store-uri sqlite:///mlflow.db --default-artifact-root /mlruns
```

**MLflow with Database Backend:**
```python
# mlflow_config.py
import mlflow
import os

# Configure MLflow tracking URI
MLFLOW_TRACKING_URI = os.getenv("MLFLOW_TRACKING_URI", "http://localhost:5000")
mlflow.set_tracking_uri(MLFLOW_TRACKING_URI)

# Set experiment
mlflow.set_experiment("customer_churn_prediction")
```

**Production MLflow Setup:**
```yaml
# docker-compose.mlflow.yml
version: '3.8'
services:
  mlflow-server:
    image: ghcr.io/mlflow/mlflow:latest
    ports:
      - "5000:5000"
    environment:
      - MLFLOW_BACKEND_STORE_URI=postgresql://mlflow:password@postgres:5432/mlflow
      - MLFLOW_ARTIFACT_STORE_URI=s3://mlflow-artifacts/
      - AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}
      - AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}
    depends_on:
      - postgres

  postgres:
    image: postgres:15-alpine
    environment:
      - POSTGRES_DB=mlflow
      - POSTGRES_USER=mlflow
      - POSTGRES_PASSWORD=password
    volumes:
      - mlflow_postgres_data:/var/lib/postgresql/data

volumes:
  mlflow_postgres_data:
```

#### Experiment Tracking Implementation

**Basic Experiment Logging:**
```python
# train_with_tracking.py
import mlflow
import mlflow.sklearn
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score, precision_score, recall_score, f1_score
from sklearn.model_selection import train_test_split
import pandas as pd
import numpy as np
import json
from datetime import datetime

def train_model_with_tracking(X, y, params):
    """Train model with comprehensive MLflow tracking"""

    with mlflow.start_run():
        # Log parameters
        mlflow.log_params(params)

        # Log input data info
        mlflow.log_param("data_shape", str(X.shape))
        mlflow.log_param("feature_count", X.shape[1])
        mlflow.log_param("target_distribution", json.dumps(dict(pd.Series(y).value_counts())))

        # Log training metadata
        mlflow.log_param("training_start_time", datetime.now().isoformat())
        mlflow.log_param("model_type", "RandomForestClassifier")
        mlflow.log_param("random_state", 42)

        # Split data
        X_train, X_test, y_train, y_test = train_test_split(
            X, y, test_size=0.2, random_state=42, stratify=y
        )

        # Train model
        model = RandomForestClassifier(**params, random_state=42)
        model.fit(X_train, y_train)

        # Make predictions
        y_pred = model.predict(X_test)
        y_pred_proba = model.predict_proba(X_test)

        # Calculate comprehensive metrics
        accuracy = accuracy_score(y_test, y_pred)
        precision = precision_score(y_test, y_pred, average='weighted')
        recall = recall_score(y_test, y_pred, average='weighted')
        f1 = f1_score(y_test, y_pred, average='weighted')

        # Log metrics
        mlflow.log_metric("accuracy", accuracy)
        mlflow.log_metric("precision", precision)
        mlflow.log_metric("recall", recall)
        mlflow.log_metric("f1_score", f1)

        # Log feature importance
        feature_importance = pd.DataFrame({
            'feature': [f'feature_{i}' for i in range(X.shape[1])],
            'importance': model.feature_importances_
        }).sort_values('importance', ascending=False)

        feature_importance.to_csv("feature_importance.csv", index=False)
        mlflow.log_artifact("feature_importance.csv")

        # Log model
        mlflow.sklearn.log_model(model, "model")

        # Log additional artifacts
        mlflow.log_artifact("requirements.txt")

        # Create and log plots
        import matplotlib.pyplot as plt
        from sklearn.metrics import confusion_matrix, roc_curve, auc

        # Confusion Matrix
        cm = confusion_matrix(y_test, y_pred)
        plt.figure(figsize=(8, 6))
        plt.imshow(cm, interpolation='nearest', cmap=plt.cm.Blues)
        plt.title('Confusion Matrix')
        plt.colorbar()
        plt.savefig("confusion_matrix.png")
        mlflow.log_artifact("confusion_matrix.png")
        plt.close()

        # ROC Curve (for binary classification)
        if len(np.unique(y)) == 2:
            fpr, tpr, _ = roc_curve(y_test, y_pred_proba[:, 1])
            roc_auc = auc(fpr, tpr)

            plt.figure(figsize=(8, 6))
            plt.plot(fpr, tpr, color='darkorange', lw=2, label=f'ROC curve (area = {roc_auc:.2f})')
            plt.plot([0, 1], [0, 1], color='navy', lw=2, linestyle='--')
            plt.xlim([0.0, 1.0])
            plt.ylim([0.0, 1.05])
            plt.xlabel('False Positive Rate')
            plt.ylabel('True Positive Rate')
            plt.title('Receiver Operating Characteristic')
            plt.legend(loc="lower right")
            plt.savefig("roc_curve.png")
            mlflow.log_artifact("roc_curve.png")
            plt.close()

            mlflow.log_metric("roc_auc", roc_auc)

        # Log model signature and input example
        from mlflow.models.signature import infer_signature
        signature = infer_signature(X_test, y_pred)
        mlflow.sklearn.log_model(model, "model", signature=signature, input_example=X_test[:5])

        return model, {
            'accuracy': accuracy,
            'precision': precision,
            'recall': recall,
            'f1_score': f1
        }
```

**Advanced Experiment Tracking:**
```python
# advanced_tracking.py
import mlflow
from mlflow.tracking import MlflowClient
import tempfile
import os

def log_model_artifacts(model, X_test, y_test, model_name):
    """Log comprehensive model artifacts"""

    with mlflow.start_run() as run:
        # Log model with metadata
        mlflow.sklearn.log_model(
            model,
            model_name,
            registered_model_name=model_name
        )

        # Log dataset information
        dataset_info = {
            "test_size": len(X_test),
            "feature_count": X_test.shape[1],
            "test_labels_distribution": dict(pd.Series(y_test).value_counts())
        }
        mlflow.log_dict(dataset_info, "dataset_info.json")

        # Log model hyperparameters as tags
        for param, value in model.get_params().items():
            mlflow.set_tag(f"model_param.{param}", str(value))

        # Log environment information
        import sys
        env_info = {
            "python_version": sys.version,
            "platform": sys.platform,
            "mlflow_version": mlflow.__version__
        }
        mlflow.log_dict(env_info, "environment.json")

        # Log custom metrics
        mlflow.log_metric("model_size_mb", calculate_model_size(model))

        return run.info.run_id

def calculate_model_size(model):
    """Calculate model size in MB"""
    import pickle
    with tempfile.NamedTemporaryFile() as f:
        pickle.dump(model, f)
        size_bytes = os.path.getsize(f.name)
    return size_bytes / (1024 * 1024)

def compare_experiments(experiment_ids):
    """Compare multiple experiments"""
    client = MlflowClient()

    comparison_data = []
    for exp_id in experiment_ids:
        runs = client.search_runs(exp_id, order_by=["metrics.accuracy DESC"])

        for run in runs[:5]:  # Top 5 runs per experiment
            run_data = {
                'experiment_id': exp_id,
                'run_id': run.info.run_id,
                'accuracy': run.data.metrics.get('accuracy'),
                'precision': run.data.metrics.get('precision'),
                'model_params': run.data.params
            }
            comparison_data.append(run_data)

    return pd.DataFrame(comparison_data)
```

### 5.2 Model Registry and Versioning

#### What is a Model Registry?

**Model Registry** is a centralized repository for storing, versioning, and managing machine learning models. It provides model lineage, stage transitions, and access control.

**Key Features**:
- **Version Control**: Track different versions of models
- **Stage Management**: Development → Staging → Production
- **Metadata Storage**: Store model descriptions, metrics, and artifacts
- **Access Control**: Manage permissions for model access
- **Model Comparison**: Compare different model versions

#### MLflow Model Registry

**Registering Models:**
```python
# register_model.py
import mlflow
import mlflow.sklearn
from mlflow.tracking import MlflowClient

def register_model(run_id, model_name, model_description=""):
    """Register a model from a run"""

    client = MlflowClient()

    # Create model version
    result = mlflow.register_model(
        model_uri=f"runs:/{run_id}/model",
        name=model_name
    )

    # Add description
    if model_description:
        client.update_model_version(
            name=model_name,
            version=result.version,
            description=model_description
        )

    # Add tags
    client.set_model_version_tag(
        name=model_name,
        version=result.version,
        key="validation_status",
        value="pending"
    )

    return result

def promote_model_to_staging(model_name, version):
    """Promote model to staging stage"""

    client = MlflowClient()

    # Transition to staging
    client.transition_model_version_stage(
        name=model_name,
        version=version,
        stage="Staging"
    )

    # Update description
    client.update_model_version(
        name=model_name,
        version=version,
        description="Promoted to staging after validation"
    )

def promote_model_to_production(model_name, version, metrics):
    """Promote model to production with metrics"""

    client = MlflowClient()

    # Transition to production
    client.transition_model_version_stage(
        name=model_name,
        version=version,
        stage="Production"
    )

    # Log production metrics
    for metric_name, value in metrics.items():
        client.set_model_version_tag(
            name=model_name,
            version=version,
            key=f"prod_{metric_name}",
            value=str(value)
        )

def archive_old_models(model_name, keep_versions=5):
    """Archive old model versions"""

    client = MlflowClient()

    # Get all versions
    versions = client.get_latest_versions(model_name, stages=["Production", "Staging", "Archived"])

    # Archive old versions
    for version_info in versions[keep_versions:]:
        if version_info.current_stage != "Archived":
            client.transition_model_version_stage(
                name=model_name,
                version=version_info.version,
                stage="Archived"
            )
```

**Model Registry API:**
```python
# model_registry_api.py
from mlflow.tracking import MlflowClient
from typing import List, Dict, Optional
import pandas as pd

class ModelRegistry:
    """MLflow Model Registry wrapper"""

    def __init__(self):
        self.client = MlflowClient()

    def list_models(self) -> List[str]:
        """List all registered models"""
        return [model.name for model in self.client.list_registered_models()]

    def get_model_versions(self, model_name: str) -> pd.DataFrame:
        """Get all versions of a model"""
        versions = self.client.get_latest_versions(model_name, stages=["None", "Staging", "Production", "Archived"])
        return pd.DataFrame([{
            'version': v.version,
            'stage': v.current_stage,
            'creation_time': v.creation_timestamp,
            'run_id': v.run_id,
            'description': v.description
        } for v in versions])

    def get_model_info(self, model_name: str, version: str) -> Dict:
        """Get detailed information about a model version"""
        version_info = self.client.get_model_version(model_name, version)
        run = self.client.get_run(version_info.run_id)

        return {
            'model_name': model_name,
            'version': version,
            'stage': version_info.current_stage,
            'run_id': version_info.run_id,
            'metrics': run.data.metrics,
            'params': run.data.params,
            'tags': version_info.tags,
            'description': version_info.description
        }

    def compare_models(self, model_name: str, versions: List[str]) -> pd.DataFrame:
        """Compare multiple model versions"""
        comparison_data = []

        for version in versions:
            info = self.get_model_info(model_name, version)
            comparison_data.append({
                'version': version,
                'stage': info['stage'],
                'accuracy': info['metrics'].get('accuracy', 0),
                'precision': info['metrics'].get('precision', 0),
                'recall': info['metrics'].get('recall', 0),
                'f1_score': info['metrics'].get('f1_score', 0)
            })

        return pd.DataFrame(comparison_data)

    def load_model(self, model_name: str, version: str = "Production"):
        """Load a model for inference"""
        if version == "Production":
            model_version = self.client.get_latest_versions(model_name, stages=["Production"])[0]
            version = model_version.version

        model_uri = f"models:/{model_name}/{version}"
        return mlflow.sklearn.load_model(model_uri)
```

### 5.3 Model Serving Infrastructure

#### What is Model Serving?

**Model Serving** is the process of deploying trained machine learning models into production environments where they can receive input data and return predictions.

**Serving Patterns**:
- **Real-time Serving**: Low-latency predictions for individual requests
- **Batch Serving**: High-throughput processing of multiple predictions
- **Streaming Serving**: Continuous prediction on data streams
- **Edge Serving**: Running models on edge devices

#### FastAPI Model Serving

**Basic ML API:**
```python
# app.py
from fastapi import FastAPI, HTTPException
from pydantic import BaseModel
import mlflow.sklearn
import numpy as np
import logging
from typing import List, Optional
import time

# Configure logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

app = FastAPI(title="ML Prediction API", version="1.0.0")

# Global model variable
model = None

class PredictionRequest(BaseModel):
    features: List[List[float]]
    model_version: Optional[str] = "Production"

class PredictionResponse(BaseModel):
    predictions: List[float]
    model_version: str
    processing_time: float
    status: str

class HealthResponse(BaseModel):
    status: str
    model_loaded: bool
    model_version: Optional[str]

@app.on_event("startup")
async def startup_event():
    """Load model on startup"""
    global model
    try:
        # Load model from MLflow registry
        model = mlflow.sklearn.load_model("models:/churn-prediction-model/Production")
        logger.info("Model loaded successfully")
    except Exception as e:
        logger.error(f"Failed to load model: {e}")
        raise

@app.get("/health", response_model=HealthResponse)
async def health_check():
    """Health check endpoint"""
    return HealthResponse(
        status="healthy" if model is not None else "unhealthy",
        model_loaded=model is not None,
        model_version="Production" if model else None
    )

@app.post("/predict", response_model=PredictionResponse)
async def predict(request: PredictionRequest):
    """Prediction endpoint"""
    if model is None:
        raise HTTPException(status_code=503, detail="Model not loaded")

    start_time = time.time()

    try:
        # Convert input to numpy array
        features = np.array(request.features)

        # Make predictions
        predictions = model.predict_proba(features)[:, 1].tolist()

        processing_time = time.time() - start_time

        return PredictionResponse(
            predictions=predictions,
            model_version=request.model_version,
            processing_time=processing_time,
            status="success"
        )

    except Exception as e:
        logger.error(f"Prediction error: {e}")
        raise HTTPException(status_code=500, detail="Prediction failed")

@app.get("/model/info")
async def model_info():
    """Get model information"""
    if model is None:
        raise HTTPException(status_code=503, detail="Model not loaded")

    # Get model metadata from MLflow
    try:
        run_id = model.metadata.run_id
        client = mlflow.tracking.MlflowClient()
        run = client.get_run(run_id)

        return {
            "model_type": type(model).__name__,
            "run_id": run_id,
            "parameters": run.data.params,
            "metrics": run.data.metrics,
            "creation_time": run.info.start_time
        }
    except Exception as e:
        logger.error(f"Failed to get model info: {e}")
        return {"error": "Could not retrieve model information"}
```

**Advanced Serving Features:**
```python
# advanced_serving.py
from fastapi import FastAPI, BackgroundTasks, Request
from fastapi.middleware.cors import CORSMiddleware
from slowapi import Limiter, _rate_limit_exceeded_handler
from slowapi.util import get_remote_address
from slowapi.errors import RateLimitExceeded
import asyncio
from typing import Dict, List
import time
import logging

logger = logging.getLogger(__name__)

# Rate limiting
limiter = Limiter(key_func=get_remote_address)
app = FastAPI(title="Advanced ML API")

# Add CORS middleware
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# Rate limiting middleware
app.state.limiter = limiter
app.add_exception_handler(RateLimitExceeded, _rate_limit_exceeded_handler)

# Metrics storage
metrics_store = {
    "requests_total": 0,
    "predictions_total": 0,
    "errors_total": 0,
    "avg_response_time": 0.0
}

class MetricsManager:
    """Manage API metrics"""

    def __init__(self):
        self._metrics = metrics_store
        self._lock = asyncio.Lock()

    async def increment_counter(self, metric: str):
        async with self._lock:
            self._metrics[metric] += 1

    async def record_response_time(self, response_time: float):
        async with self._lock:
            # Simple moving average
            self._metrics["avg_response_time"] = (
                self._metrics["avg_response_time"] + response_time
            ) / 2

    def get_metrics(self) -> Dict:
        return self._metrics.copy()

metrics_manager = MetricsManager()

@app.middleware("http")
async def metrics_middleware(request: Request, call_next):
    """Middleware to collect metrics"""
    start_time = time.time()

    response = await call_next(request)

    response_time = time.time() - start_time
    await metrics_manager.record_response_time(response_time)
    await metrics_manager.increment_counter("requests_total")

    # Add custom headers
    response.headers["X-Response-Time"] = str(response_time)
    response.headers["X-API-Version"] = "1.0.0"

    return response

@app.get("/metrics")
async def get_metrics():
    """Expose metrics endpoint"""
    return metrics_manager.get_metrics()

@app.post("/predict")
@limiter.limit("100/minute")  # Rate limit: 100 requests per minute
async def predict(request: PredictionRequest, background_tasks: BackgroundTasks):
    """Enhanced prediction endpoint"""
    await metrics_manager.increment_counter("predictions_total")

    try:
        # Prediction logic here
        predictions = [0.8, 0.3]  # Mock predictions

        # Add background task for logging
        background_tasks.add_task(log_prediction, request, predictions)

        return PredictionResponse(
            predictions=predictions,
            model_version=request.model_version,
            processing_time=0.1,
            status="success"
        )

    except Exception as e:
        await metrics_manager.increment_counter("errors_total")
        logger.error(f"Prediction error: {e}")
        raise HTTPException(status_code=500, detail="Prediction failed")

async def log_prediction(request: PredictionRequest, predictions: List[float]):
    """Background task to log predictions"""
    # Log to database, monitoring system, etc.
    logger.info(f"Prediction made: {len(predictions)} predictions for model {request.model_version}")

@app.get("/model/versions")
async def list_model_versions():
    """List available model versions"""
    # In a real implementation, this would query MLflow registry
    return {
        "available_versions": ["v1.0.0", "v1.1.0", "v2.0.0"],
        "production_version": "v2.0.0",
        "staging_version": "v1.1.0"
    }

@app.post("/model/switch")
async def switch_model_version(version: str):
    """Switch active model version"""
    # In a real implementation, this would load a different model version
    logger.info(f"Switching to model version: {version}")
    return {"status": "success", "new_version": version}
```

#### Docker Deployment for Model Serving

**Dockerfile for ML API:**
```dockerfile
FROM python:3.9-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    && rm -rf /var/lib/apt/lists/*

# Copy requirements and install
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Create non-root user
RUN useradd --create-home --shell /bin/bash app \
    && chown -R app:app /app
USER app

# Health check
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
    CMD curl -f http://localhost:8000/health || exit 1

EXPOSE 8000

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

**Kubernetes Deployment:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ml-api
  template:
    metadata:
      labels:
        app: ml-api
    spec:
      containers:
      - name: ml-api
        image: your-registry/ml-api:latest
        ports:
        - containerPort: 8000
        env:
        - name: MLFLOW_TRACKING_URI
          value: "http://mlflow-server:5000"
        resources:
          requests:
            memory: "512Mi"
            cpu: "250m"
          limits:
            memory: "1Gi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
---
apiVersion: v1
kind: Service
metadata:
  name: ml-api-service
spec:
  selector:
    app: ml-api
  ports:
  - port: 80
    targetPort: 8000
  type: LoadBalancer
```

This comprehensive model management and serving section provides the foundation for tracking, versioning, and deploying ML models in production environments.
            'feature': X.columns,
            'importance': model.feature_importances_
        }).sort_values('importance', ascending=False)
        
        # Save feature importance plot
        import matplotlib.pyplot as plt
        plt.figure(figsize=(10, 6))
        plt.bar(feature_importance['feature'][:10], feature_importance['importance'][:10])
        plt.xticks(rotation=45)
        plt.title("Top 10 Feature Importance")
        plt.tight_layout()
        plt.savefig("feature_importance.png")
        mlflow.log_artifact("feature_importance.png")
        
        # Log model
        mlflow.sklearn.log_model(model, "model")
        
        # Log additional artifacts
        mlflow.log_artifact("requirements.txt")
        
        # Set tags
        mlflow.set_tags({
            "model_type": "random_forest",
            "data_version": "v1.0",
            "experiment_type": "hyperparameter_tuning"
        })
        
        return model, accuracy

# Example usage
if __name__ == "__main__":
    # Load data
    data = pd.read_csv("data/customer_churn.csv")
    X = data.drop('Churn', axis=1)
    y = data['Churn']
    
    # Define parameters
    params = {
        'n_estimators': 100,
        'max_depth': 10,
        'min_samples_split': 2,
        'random_state': 42
    }
    
    # Train with tracking
    model, accuracy = train_model_with_tracking(X, y, params)
    print(f"Model trained with accuracy: {accuracy:.4f}")
```

#### Hyperparameter Tuning with MLflow

**Grid Search with Tracking:**
```python
# hyperparameter_tuning.py
import mlflow
from sklearn.model_selection import GridSearchCV
from sklearn.ensemble import RandomForestClassifier
import pandas as pd

def hyperparameter_tuning_with_mlflow(X, y):
    """Perform hyperparameter tuning with MLflow tracking"""
    
    # Define parameter grid
    param_grid = {
        'n_estimators': [50, 100, 200],
        'max_depth': [None, 10, 20, 30],
        'min_samples_split': [2, 5, 10],
        'min_samples_leaf': [1, 2, 4]
    }
    
    # Create base model
    rf = RandomForestClassifier(random_state=42)
    
    # Create GridSearchCV
    grid_search = GridSearchCV(
        rf, param_grid, cv=5, scoring='accuracy', 
        n_jobs=-1, verbose=1
    )
    
    # Parent run for hyperparameter tuning
    with mlflow.start_run(run_name="hyperparameter_tuning"):
        
        # Fit grid search
        grid_search.fit(X, y)
        
        # Log best parameters
        mlflow.log_params(grid_search.best_params_)
        mlflow.log_metric("best_cv_score", grid_search.best_score_)
        
        # Log all results
        cv_results = pd.DataFrame(grid_search.cv_results_)
        cv_results.to_csv("cv_results.csv")
        mlflow.log_artifact("cv_results.csv")
        
        # Train final model with best parameters
        best_model = grid_search.best_estimator_
        
        # Child run for best model
        with mlflow.start_run(run_name="best_model", nested=True):
            mlflow.log_params(grid_search.best_params_)
            mlflow.log_metric("best_accuracy", grid_search.best_score_)
            mlflow.sklearn.log_model(best_model, "best_model")
            
            # Log model info
            mlflow.set_tags({
                "model_type": "random_forest_tuned",
                "tuning_method": "grid_search",
                "cv_folds": 5
            })
        
        return best_model, grid_search.best_params_

# Parallel hyperparameter tuning
def parallel_hyperparameter_tuning(X, y, n_trials=50):
    """Use Optuna with MLflow for parallel hyperparameter tuning"""
    import optuna
    
    def objective(trial):
        with mlflow.start_run(nested=True):
            # Define hyperparameters to optimize
            n_estimators = trial.suggest_int('n_estimators', 50, 300)
            max_depth = trial.suggest_int('max_depth', 3, 30)
            min_samples_split = trial.suggest_int('min_samples_split', 2, 20)
            min_samples_leaf = trial.suggest_int('min_samples_leaf', 1, 10)
            
            # Create and train model
            model = RandomForestClassifier(
                n_estimators=n_estimators,
                max_depth=max_depth,
                min_samples_split=min_samples_split,
                min_samples_leaf=min_samples_leaf,
                random_state=42
            )
            
            # Cross-validation
            from sklearn.model_selection import cross_val_score
            scores = cross_val_score(model, X, y, cv=5, scoring='accuracy')
            accuracy = scores.mean()
            
            # Log to MLflow
            mlflow.log_params({
                'n_estimators': n_estimators,
                'max_depth': max_depth,
                'min_samples_split': min_samples_split,
                'min_samples_leaf': min_samples_leaf
            })
            mlflow.log_metric("cv_accuracy", accuracy)
            
            return accuracy
    
    # Create study
    study = optuna.create_study(direction='maximize')
    
    # Parent run
    with mlflow.start_run(run_name="optuna_hyperparameter_tuning"):
        mlflow.log_param("optimization_trials", n_trials)
        mlflow.log_param("optimization_library", "optuna")
        
        # Optimize
        study.optimize(objective, n_trials=n_trials)
        
        # Log best parameters
        mlflow.log_params(study.best_params)
        mlflow.log_metric("best_accuracy", study.best_value)
        
        # Train final model
        best_model = RandomForestClassifier(**study.best_params, random_state=42)
        best_model.fit(X, y)
        
        # Log best model
        mlflow.sklearn.log_model(best_model, "best_model")
        
        return best_model, study.best_params
```

### 5.2 Model Registry and Versioning

The Model Registry provides a centralized repository for model versions and metadata.

#### Model Registry Operations

**Registering Models:**
```python
# model_registry.py
import mlflow
import mlflow.sklearn
from mlflow.tracking import MlflowClient

class ModelRegistry:
    def __init__(self):
        self.client = MlflowClient()
    
    def register_model(self, run_id, model_name, model_path="model"):
        """Register a model from an MLflow run"""
        
        # Create model version
        model_version = mlflow.register_model(
            model_uri=f"runs:/{run_id}/{model_path}",
            name=model_name
        )
        
        print(f"Model registered: {model_name} v{model_version.version}")
        return model_version
    
    def promote_model(self, model_name, version, stage):
        """Promote model to different stages"""
        
        # Transition model version to stage
        self.client.transition_model_version_stage(
            name=model_name,
            version=version,
            stage=stage  # "Staging", "Production", "Archived"
        )
        
        print(f"Model {model_name} v{version} promoted to {stage}")
    
    def get_model_info(self, model_name):
        """Get information about a registered model"""
        
        # Get model versions
        versions = self.client.get_latest_versions(model_name)
        
        model_info = {
            "name": model_name,
            "versions": []
        }
        
        for version in versions:
            version_info = {
                "version": version.version,
                "stage": version.current_stage,
                "run_id": version.run_id,
                "creation_timestamp": version.creation_timestamp,
                "description": version.description
            }
            model_info["versions"].append(version_info)
        
        return model_info
    
    def compare_models(self, model_name, version1, version2):
        """Compare two model versions"""
        
        # Get model versions
        mv1 = self.client.get_model_version(model_name, version1)
        mv2 = self.client.get_model_version(model_name, version2)
        
        # Get run data
        run1 = self.client.get_run(mv1.run_id)
        run2 = self.client.get_run(mv2.run_id)
        
        comparison = {
            "version_1": {
                "version": version1,
                "stage": mv1.current_stage,
                "metrics": run1.data.metrics,
                "params": run1.data.params
            },
            "version_2": {
                "version": version2,
                "stage": mv2.current_stage,
                "metrics": run2.data.metrics,
                "params": run2.data.params
            }
        }
        
        return comparison
    
    def archive_old_versions(self, model_name, keep_versions=5):
        """Archive old model versions"""
        
        # Get all versions
        versions = self.client.get_latest_versions(model_name, stages=["None", "Staging"])
        
        # Sort by version number (descending)
        versions.sort(key=lambda x: int(x.version), reverse=True)
        
        # Archive versions beyond keep limit
        for version in versions[keep_versions:]:
            self.client.transition_model_version_stage(
                name=model_name,
                version=version.version,
                stage="Archived"
            )
            print(f"Archived {model_name} v{version.version}")

# Usage example
if __name__ == "__main__":
    registry = ModelRegistry()
    
    # Register a model
    model_version = registry.register_model(
        run_id="your_run_id",
        model_name="customer_churn_model"
    )
    
    # Promote to staging
    registry.promote_model("customer_churn_model", model_version.version, "Staging")
    
    # Get model info
    info = registry.get_model_info("customer_churn_model")
    print(info)
```

#### Model Versioning Best Practices

**Semantic Versioning for Models:**
```python
# model_versioning.py
import semver
from datetime import datetime

class ModelVersionManager:
    def __init__(self):
        self.version_format = "MAJOR.MINOR.PATCH"
    
    def generate_version(self, breaking_changes=False, new_features=False, bug_fixes=False):
        """Generate next version based on changes"""
        
        # Read current version from file or database
        current_version = self.get_current_version()
        
        if breaking_changes:
            # Increment major version
            new_version = semver.VersionInfo.parse(current_version).bump_major()
        elif new_features:
            # Increment minor version
            new_version = semver.VersionInfo.parse(current_version).bump_minor()
        elif bug_fixes:
            # Increment patch version
            new_version = semver.VersionInfo.parse(current_version).bump_patch()
        else:
            # No changes, return current version
            return current_version
        
        return str(new_version)
    
    def get_current_version(self):
        """Get current model version"""
        # Implementation to read from version file or database
        try:
            with open("model_version.txt", "r") as f:
                return f.read().strip()
        except FileNotFoundError:
            return "0.1.0"  # Default starting version
    
    def update_version_file(self, new_version):
        """Update version file"""
        with open("model_version.txt", "w") as f:
            f.write(new_version)
        
        # Also update metadata
        metadata = {
            "version": new_version,
            "updated_at": datetime.now().isoformat(),
            "updated_by": "mlops_pipeline"
        }
        
        import json
        with open("model_metadata.json", "w") as f:
            json.dump(metadata, f, indent=2)

# Model metadata tracking
def create_model_metadata(model, model_name, version, metrics, params):
    """Create comprehensive model metadata"""
    
    metadata = {
        "name": model_name,
        "version": version,
        "created_at": datetime.now().isoformat(),
        "framework": "scikit-learn",
        "model_type": type(model).__name__,
        "metrics": metrics,
        "parameters": params,
        "data_info": {
            "training_samples": 10000,  # Example
            "features": 20,
            "target_classes": 2
        },
        "performance": {
            "accuracy": metrics.get("accuracy", 0),
            "precision": metrics.get("precision", 0),
            "recall": metrics.get("recall", 0)
        },
        "artifacts": [
            "model.pkl",
            "feature_importance.png",
            "requirements.txt"
        ]
    }
    
    return metadata
```

### 5.3 Model Serving Infrastructure

Deploying models as production-ready APIs requires robust serving infrastructure.

#### FastAPI Model Serving

**Basic Model API:**
```python
# model_api.py
from fastapi import FastAPI, HTTPException, BackgroundTasks
from pydantic import BaseModel, Field
import joblib
import numpy as np
import logging
from typing import List, Optional
import time
from datetime import datetime

# Configure logging
logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

app = FastAPI(
    title="ML Model API",
    description="Customer Churn Prediction API",
    version="1.0.0"
)

# Load model at startup
model = None
model_metadata = None

@app.on_event("startup")
async def load_model():
    global model, model_metadata
    try:
        model = joblib.load("models/model.pkl")
        # Load metadata if available
        try:
            import json
            with open("models/metadata.json", "r") as f:
                model_metadata = json.load(f)
        except FileNotFoundError:
            model_metadata = {"version": "unknown"}
        logger.info(f"Model loaded successfully: {model_metadata.get('version', 'unknown')}")
    except Exception as e:
        logger.error(f"Failed to load model: {e}")
        raise

# Request/Response models
class PredictionRequest(BaseModel):
    features: List[float] = Field(..., description="List of feature values")
    customer_id: Optional[str] = Field(None, description="Customer identifier")
    
    class Config:
        schema_extra = {
            "example": {
                "features": [0.5, 0.3, 0.8, 0.2, 0.9],
                "customer_id": "CUST_001"
            }
        }

class PredictionResponse(BaseModel):
    prediction: int
    probability: float
    customer_id: Optional[str]
    model_version: str
    timestamp: str
    processing_time_ms: float

class BatchPredictionRequest(BaseModel):
    predictions: List[PredictionRequest]

class BatchPredictionResponse(BaseModel):
    results: List[PredictionResponse]

# Health check
@app.get("/health")
async def health_check():
    """Health check endpoint"""
    return {
        "status": "healthy",
        "model_loaded": model is not None,
        "model_version": model_metadata.get("version", "unknown") if model_metadata else "unknown",
        "timestamp": datetime.now().isoformat()
    }

# Single prediction
@app.post("/predict", response_model=PredictionResponse)
async def predict(request: PredictionRequest, background_tasks: BackgroundTasks):
    """Make prediction for single customer"""
    start_time = time.time()
    
    try:
        # Validate input
        if not request.features:
            raise HTTPException(status_code=400, detail="Features list cannot be empty")
        
        # Convert to numpy array
        features = np.array(request.features).reshape(1, -1)
        
        # Make prediction
        prediction = model.predict(features)[0]
        probability = model.predict_proba(features)[0][prediction]
        
        processing_time = (time.time() - start_time) * 1000
        
        # Log prediction (in background to not block response)
        background_tasks.add_task(
            log_prediction,
            request.customer_id,
            prediction,
            probability,
            processing_time
        )
        
        return PredictionResponse(
            prediction=int(prediction),
            probability=float(probability),
            customer_id=request.customer_id,
            model_version=model_metadata.get("version", "unknown"),
            timestamp=datetime.now().isoformat(),
            processing_time_ms=processing_time
        )
        
    except Exception as e:
        logger.error(f"Prediction error: {e}")
        raise HTTPException(status_code=500, detail="Prediction failed")

# Batch prediction
@app.post("/predict/batch", response_model=BatchPredictionResponse)
async def predict_batch(request: BatchPredictionRequest):
    """Make predictions for multiple customers"""
    start_time = time.time()
    
    try:
        if not request.predictions:
            raise HTTPException(status_code=400, detail="Predictions list cannot be empty")
        
        results = []
        for pred_request in request.predictions:
            # Convert to numpy array
            features = np.array(pred_request.features).reshape(1, -1)
            
            # Make prediction
            prediction = model.predict(features)[0]
            probability = model.predict_proba(features)[0][prediction]
            
            result = PredictionResponse(
                prediction=int(prediction),
                probability=float(probability),
                customer_id=pred_request.customer_id,
                model_version=model_metadata.get("version", "unknown"),
                timestamp=datetime.now().isoformat(),
                processing_time_ms=0  # Will be set by individual predictions
            )
            results.append(result)
        
        total_time = (time.time() - start_time) * 1000
        
        return BatchPredictionResponse(results=results)
        
    except Exception as e:
        logger.error(f"Batch prediction error: {e}")
        raise HTTPException(status_code=500, detail="Batch prediction failed")

# Model info
@app.get("/model/info")
async def model_info():
    """Get model information"""
    if model_metadata:
        return model_metadata
    else:
        return {
            "model_type": type(model).__name__ if model else "unknown",
            "version": "unknown",
            "status": "loaded" if model else "not_loaded"
        }

# Logging function
def log_prediction(customer_id, prediction, probability, processing_time):
    """Log prediction for monitoring"""
    logger.info(
        f"Prediction: customer={customer_id}, "
        f"prediction={prediction}, probability={probability:.4f}, "
        f"processing_time={processing_time:.2f}ms"
    )

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

#### Advanced Serving Patterns

**A/B Testing for Models:**
```python
# ab_testing_api.py
import random
from typing import Dict
from fastapi import FastAPI, HTTPException
import joblib

class ModelABTester:
    def __init__(self):
        self.models = {}
        self.traffic_distribution = {}  # model_name -> percentage
        
    def register_model(self, model_name: str, model_path: str, traffic_percentage: float):
        """Register a model for A/B testing"""
        self.models[model_name] = joblib.load(model_path)
        self.traffic_distribution[model_name] = traffic_percentage
        
        # Normalize percentages
        total = sum(self.traffic_distribution.values())
        self.traffic_distribution = {k: v/total for k, v in self.traffic_distribution.items()}
    
    def select_model(self) -> str:
        """Select model based on traffic distribution"""
        rand = random.random()
        cumulative = 0.0
        
        for model_name, percentage in self.traffic_distribution.items():
            cumulative += percentage
            if rand <= cumulative:
                return model_name
        
        # Fallback to first model
        return list(self.models.keys())[0]
    
    def predict(self, model_name: str, features):
        """Make prediction with specific model"""
        if model_name not in self.models:
            raise ValueError(f"Model {model_name} not found")
        
        model = self.models[model_name]
        return model.predict(features)

# Global A/B tester
ab_tester = ModelABTester()

app = FastAPI(title="A/B Testing Model API")

@app.post("/predict")
async def predict_with_ab_testing(request: PredictionRequest):
    """Make prediction with A/B testing"""
    
    # Select model for this request
    selected_model = ab_tester.select_model()
    
    # Make prediction
    features = np.array(request.features).reshape(1, -1)
    prediction = ab_tester.predict(selected_model, features)[0]
    probability = ab_tester.predict_proba(selected_model, features)[0][prediction]
    
    return {
        "prediction": int(prediction),
        "probability": float(probability),
        "model_used": selected_model,
        "customer_id": request.customer_id
    }

@app.post("/register-model")
async def register_model(model_name: str, model_path: str, traffic_percentage: float):
    """Register a new model for A/B testing"""
    try:
        ab_tester.register_model(model_name, model_path, traffic_percentage)
        return {"message": f"Model {model_name} registered successfully"}
    except Exception as e:
        raise HTTPException(status_code=500, detail=str(e))

@app.get("/ab-status")
async def get_ab_status():
    """Get current A/B testing status"""
    return {
        "models": list(ab_tester.models.keys()),
        "traffic_distribution": ab_tester.traffic_distribution
    }
```

**Model Performance Monitoring:**
```python
# monitoring_middleware.py
from fastapi import Request, Response
from starlette.middleware.base import BaseHTTPMiddleware
import time
import logging
from collections import defaultdict
import psutil
import threading

logger = logging.getLogger(__name__)

class ModelMonitoringMiddleware(BaseHTTPMiddleware):
    def __init__(self, app):
        super().__init__(app)
        self.metrics = defaultdict(int)
        self.response_times = []
        self.error_counts = defaultdict(int)
        
        # Start background monitoring
        self.monitoring_thread = threading.Thread(target=self._background_monitoring)
        self.monitoring_thread.daemon = True
        self.monitoring_thread.start()
    
    async def dispatch(self, request: Request, call_next):
        start_time = time.time()
        
        # Track request
        self.metrics["total_requests"] += 1
        
        try:
            response = await call_next(request)
            
            # Track response time
            response_time = time.time() - start_time
            self.response_times.append(response_time)
            
            # Keep only last 1000 response times
            if len(self.response_times) > 1000:
                self.response_times.pop(0)
            
            # Track status codes
            status_code = response.status_code
            self.metrics[f"status_{status_code}"] += 1
            
            # Log slow requests
            if response_time > 1.0:  # More than 1 second
                logger.warning(f"Slow request: {request.url.path} took {response_time:.2f}s")
            
            return response
            
        except Exception as e:
            # Track errors
            self.error_counts[str(type(e).__name__)] += 1
            self.metrics["total_errors"] += 1
            logger.error(f"Request error: {e}")
            raise
    
    def _background_monitoring(self):
        """Background monitoring of system resources"""
        while True:
            try:
                # CPU and memory usage
                cpu_percent = psutil.cpu_percent(interval=60)
                memory_percent = psutil.virtual_memory().percent
                
                logger.info(f"System metrics: CPU={cpu_percent:.1f}%, Memory={memory_percent:.1f}%")
                
                # Log metrics periodically
                if len(self.response_times) > 0:
                    avg_response_time = sum(self.response_times) / len(self.response_times)
                    logger.info(f"Average response time: {avg_response_time:.3f}s")
                
            except Exception as e:
                logger.error(f"Monitoring error: {e}")
    
    def get_metrics(self):
        """Get current metrics"""
        avg_response_time = sum(self.response_times) / len(self.response_times) if self.response_times else 0
        
        return {
            "total_requests": self.metrics["total_requests"],
            "total_errors": self.metrics["total_errors"],
            "average_response_time": avg_response_time,
            "status_codes": {k: v for k, v in self.metrics.items() if k.startswith("status_")},
            "error_types": dict(self.error_counts)
        }

# Add to FastAPI app
# app.add_middleware(ModelMonitoringMiddleware)

@app.get("/metrics")
async def get_metrics():
    """Get application metrics"""
    # This would integrate with the middleware
    return {"message": "Metrics endpoint - integrate with monitoring middleware"}
```

This comprehensive model management and serving infrastructure provides the foundation for reliable, scalable ML deployment in production environments. The combination of experiment tracking, model versioning, and robust serving APIs ensures that ML models can be effectively managed throughout their lifecycle.

## 6. Monitoring and Observability

### 6.1 Prometheus Metrics Collection

#### What is Prometheus?

**Prometheus** is an open-source systems monitoring and alerting toolkit originally built at SoundCloud. It collects metrics from configured targets at given intervals, evaluates rule expressions, displays the results, and can trigger alerts when specified conditions are observed.

**Core Concepts**:
- **Metrics**: Numerical measurements collected at regular intervals
- **Targets**: Systems or applications being monitored
- **Scraping**: Process of collecting metrics from targets
- **Time Series**: Sequence of data points indexed in time order
- **Labels**: Key-value pairs that add dimensions to metrics

**Why Prometheus for MLOps**:
- **Multi-dimensional**: Rich labeling system for complex queries
- **Powerful Query Language**: PromQL for complex metric analysis
- **Reliable**: Pull-based model with service discovery
- **Scalable**: Handles millions of time series efficiently
- **Integrated**: Works seamlessly with Grafana and Alertmanager

#### Setting Up Prometheus

**Docker Compose with Prometheus:**
```yaml
# docker-compose.monitoring.yml
version: '3.8'

services:
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--storage.tsdb.retention.time=200h'
      - '--web.enable-lifecycle'
    networks:
      - monitoring

  node-exporter:
    image: prom/node-exporter:latest
    ports:
      - "9100:9100"
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    networks:
      - monitoring

volumes:
  prometheus_data:

networks:
  monitoring:
    driver: bridge
```

**Prometheus Configuration:**
```yaml
# monitoring/prometheus.yml
global:
  scrape_interval: 15s        # How frequently to scrape targets
  evaluation_interval: 15s    # How frequently to evaluate rules
  scrape_timeout: 10s         # Timeout for scrape requests

rule_files:
  - "alert_rules.yml"

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - alertmanager:9093

scrape_configs:
  # Monitor Prometheus itself
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  # Monitor host system metrics
  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']
    scrape_interval: 5s

  # Monitor ML API
  - job_name: 'ml-api'
    static_configs:
      - targets: ['ml-api:8000']
    scrape_interval: 10s
    metrics_path: '/metrics'

  # Monitor Kubernetes API server
  - job_name: 'kubernetes-apiservers'
    kubernetes_sd_configs:
      - role: endpoints
    scheme: https
    tls_config:
      ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      insecure_skip_verify: true
    bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
    relabel_configs:
    - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_service_name, __meta_kubernetes_endpoint_port_name]
      action: keep
      regex: default;kubernetes;https

  # Monitor Kubernetes nodes
  - job_name: 'kubernetes-nodes'
    scheme: https
    tls_config:
      ca_file: /var/run/secrets/kubernetes.io/serviceaccount/ca.crt
      insecure_skip_verify: true
    bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
    kubernetes_sd_configs:
      - role: node
    relabel_configs:
    - action: labelmap
      regex: __meta_kubernetes_node_label_(.+)
    - target_label: __address__
      replacement: kubernetes.default.svc:443
    - source_labels: [__meta_kubernetes_node_name]
      regex: (.+)
      target_label: __metrics_path__
      replacement: /api/v1/nodes/${1}/proxy/metrics

  # Monitor Kubernetes pods
  - job_name: 'kubernetes-pods'
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
    - action: labelmap
      regex: __meta_kubernetes_pod_label_(.+)
    - source_labels: [__meta_kubernetes_namespace]
      action: replace
      target_label: namespace
    - source_labels: [__meta_kubernetes_pod_name]
      action: replace
      target_label: pod
    - source_labels: [__meta_kubernetes_pod_container_name]
      action: replace
      target_label: container
```

#### ML Application Metrics

**Custom Metrics for ML APIs:**
```python
# metrics.py
from prometheus_client import Counter, Histogram, Gauge, generate_latest, CONTENT_TYPE_LATEST
from fastapi import Response
import time
from typing import Callable

# Request metrics
REQUEST_COUNT = Counter(
    'http_requests_total',
    'Total number of HTTP requests',
    ['method', 'endpoint', 'status_code']
)

REQUEST_LATENCY = Histogram(
    'http_request_duration_seconds',
    'HTTP request latency in seconds',
    ['method', 'endpoint']
)

# Model metrics
MODEL_PREDICTIONS = Counter(
    'model_predictions_total',
    'Total number of model predictions',
    ['model_name', 'model_version']
)

MODEL_LATENCY = Histogram(
    'model_prediction_duration_seconds',
    'Model prediction latency in seconds',
    ['model_name', 'model_version']
)

# Business metrics
ACCURACY_GAUGE = Gauge(
    'model_accuracy',
    'Current model accuracy',
    ['model_name', 'model_version']
)

DATA_DRIFT_GAUGE = Gauge(
    'data_drift_score',
    'Data drift detection score',
    ['feature_name']
)

# System metrics
MEMORY_USAGE = Gauge(
    'memory_usage_bytes',
    'Current memory usage in bytes',
    ['type']  # heap, stack, etc.
)

CPU_USAGE = Gauge(
    'cpu_usage_percent',
    'Current CPU usage percentage'
)

def metrics_endpoint():
    """Prometheus metrics endpoint"""
    return Response(generate_latest(), media_type=CONTENT_TYPE_LATEST)

def track_requests(method: str, endpoint: str):
    """Decorator to track HTTP requests"""
    def decorator(func: Callable):
        async def wrapper(*args, **kwargs):
            start_time = time.time()
            try:
                result = await func(*args, **kwargs)
                status_code = getattr(result, 'status_code', 200)
                REQUEST_COUNT.labels(method=method, endpoint=endpoint, status_code=status_code).inc()
                REQUEST_LATENCY.labels(method=method, endpoint=endpoint).observe(time.time() - start_time)
                return result
            except Exception as e:
                REQUEST_COUNT.labels(method=method, endpoint=endpoint, status_code=500).inc()
                raise e
        return wrapper
    return decorator

def track_predictions(model_name: str, model_version: str):
    """Decorator to track model predictions"""
    def decorator(func: Callable):
        async def wrapper(*args, **kwargs):
            start_time = time.time()
            try:
                result = await func(*args, **kwargs)
                MODEL_PREDICTIONS.labels(model_name=model_name, model_version=model_version).inc()
                MODEL_LATENCY.labels(model_name=model_name, model_version=model_version).observe(time.time() - start_time)
                return result
            except Exception as e:
                raise e
        return wrapper
    return decorator

class MetricsCollector:
    """Advanced metrics collector for ML applications"""

    def __init__(self):
        self.prediction_errors = Counter(
            'model_prediction_errors_total',
            'Total number of prediction errors',
            ['model_name', 'error_type']
        )

        self.data_quality_metrics = Gauge(
            'data_quality_score',
            'Data quality score (0-1)',
            ['dataset_name', 'metric_type']
        )

        self.model_performance_metrics = Gauge(
            'model_performance_score',
            'Model performance score',
            ['model_name', 'metric_name']
        )

    def record_prediction_error(self, model_name: str, error_type: str):
        """Record prediction error"""
        self.prediction_errors.labels(model_name=model_name, error_type=error_type).inc()

    def update_data_quality(self, dataset_name: str, completeness: float, accuracy: float):
        """Update data quality metrics"""
        self.data_quality_metrics.labels(dataset_name=dataset_name, metric_type='completeness').set(completeness)
        self.data_quality_metrics.labels(dataset_name=dataset_name, metric_type='accuracy').set(accuracy)

    def update_model_performance(self, model_name: str, accuracy: float, precision: float, recall: float):
        """Update model performance metrics"""
        self.model_performance_metrics.labels(model_name=model_name, metric_name='accuracy').set(accuracy)
        self.model_performance_metrics.labels(model_name=model_name, metric_name='precision').set(precision)
        self.model_performance_metrics.labels(model_name=model_name, metric_name='recall').set(recall)

# Global metrics collector
metrics_collector = MetricsCollector()
```

**Integration with FastAPI:**
```python
# app.py
from fastapi import FastAPI, Request, Response
from metrics import (
    metrics_endpoint, track_requests, track_predictions,
    metrics_collector, ACCURACY_GAUGE, DATA_DRIFT_GAUGE
)
import time
import logging

logger = logging.getLogger(__name__)

app = FastAPI(title="ML API with Monitoring")

@app.on_event("startup")
async def startup_event():
    """Initialize metrics on startup"""
    # Set initial model accuracy
    ACCURACY_GAUGE.labels(model_name="churn-model", model_version="v1.0").set(0.85)

    # Initialize data drift monitoring
    DATA_DRIFT_GAUGE.labels(feature_name="age").set(0.0)
    DATA_DRIFT_GAUGE.labels(feature_name="income").set(0.0)

@app.get("/metrics")
async def get_metrics():
    """Prometheus metrics endpoint"""
    return metrics_endpoint()

@app.get("/health")
@track_requests("GET", "/health")
async def health_check():
    """Health check endpoint"""
    return {"status": "healthy", "timestamp": time.time()}

@app.post("/predict")
@track_requests("POST", "/predict")
@track_predictions("churn-model", "v1.0")
async def predict(request: PredictionRequest):
    """Prediction endpoint with monitoring"""
    try:
        # Mock prediction logic
        predictions = [0.8, 0.3]  # Replace with actual model prediction

        # Update business metrics
        metrics_collector.update_model_performance("churn-model", 0.85, 0.82, 0.88)

        return PredictionResponse(
            predictions=predictions,
            model_version="v1.0",
            processing_time=0.1,
            status="success"
        )

    except Exception as e:
        # Record error
        metrics_collector.record_prediction_error("churn-model", type(e).__name__)
        logger.error(f"Prediction error: {e}")
        raise HTTPException(status_code=500, detail="Prediction failed")

@app.post("/validate-data")
async def validate_data(data: dict):
    """Data validation endpoint"""
    try:
        # Mock data validation
        completeness = 0.95
        accuracy = 0.92

        # Update data quality metrics
        metrics_collector.update_data_quality("training_data", completeness, accuracy)

        return {"completeness": completeness, "accuracy": accuracy}

    except Exception as e:
        logger.error(f"Data validation error: {e}")
        raise HTTPException(status_code=500, detail="Data validation failed")
```

### 6.2 Grafana Dashboards

#### What is Grafana?

**Grafana** is an open-source platform for monitoring and observability. It allows you to query, visualize, alert on, and understand your metrics no matter where they are stored.

**Key Features**:
- **Data Sources**: Connect to multiple data sources (Prometheus, InfluxDB, etc.)
- **Dashboards**: Create interactive visualizations
- **Panels**: Individual visualization components
- **Alerts**: Define alert rules and notifications
- **Plugins**: Extend functionality with community plugins

#### Setting Up Grafana

**Docker Compose with Grafana:**
```yaml
# docker-compose.grafana.yml
version: '3.8'

services:
  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    volumes:
      - grafana_data:/var/lib/grafana
      - ./monitoring/grafana/provisioning:/etc/grafana/provisioning:ro
      - ./monitoring/grafana/dashboards:/var/lib/grafana/dashboards:ro
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
      - GF_USERS_ALLOW_SIGN_UP=false
      - GF_INSTALL_PLUGINS=grafana-piechart-panel,grafana-worldmap-panel
    networks:
      - monitoring

volumes:
  grafana_data:

networks:
  monitoring:
    driver: bridge
```

**Grafana Configuration:**
```yaml
# monitoring/grafana/provisioning/datasources/prometheus.yml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    url: http://prometheus:9090
    isDefault: true
    editable: true
```

**Dashboard Provisioning:**
```yaml
# monitoring/grafana/provisioning/dashboards/dashboard.yml
apiVersion: 1

providers:
  - name: 'ML Monitoring'
    type: file
    disableDeletion: false
    updateIntervalSeconds: 10
    allowUiUpdates: true
    options:
      path: /var/lib/grafana/dashboards
```

#### ML Monitoring Dashboard

**System Metrics Dashboard:**
```json
{
  "dashboard": {
    "title": "ML System Monitoring",
    "tags": ["ml", "monitoring"],
    "timezone": "browser",
    "panels": [
      {
        "title": "API Request Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total[5m])",
            "legendFormat": "{{method}} {{endpoint}}"
          }
        ]
      },
      {
        "title": "API Response Time",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "95th percentile"
          }
        ]
      },
      {
        "title": "Model Prediction Latency",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(model_prediction_duration_seconds_bucket[5m]))",
            "legendFormat": "{{model_name}} {{model_version}}"
          }
        ]
      },
      {
        "title": "Model Accuracy Over Time",
        "type": "graph",
        "targets": [
          {
            "expr": "model_accuracy",
            "legendFormat": "{{model_name}}"
          }
        ]
      },
      {
        "title": "Data Drift Detection",
        "type": "table",
        "targets": [
          {
            "expr": "data_drift_score > 0.5",
            "legendFormat": "{{feature_name}}"
          }
        ]
      },
      {
        "title": "System Resources",
        "type": "graph",
        "targets": [
          {
            "expr": "100 - (avg by(instance) (irate(node_cpu_seconds_total{mode=\"idle\"}[5m])) * 100)",
            "legendFormat": "CPU Usage %"
          },
          {
            "expr": "(1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes) * 100",
            "legendFormat": "Memory Usage %"
          }
        ]
      }
    ]
  }
}
```

**Business Metrics Dashboard:**
```json
{
  "dashboard": {
    "title": "ML Business Metrics",
    "tags": ["ml", "business"],
    "panels": [
      {
        "title": "Daily Predictions",
        "type": "stat",
        "targets": [
          {
            "expr": "sum(increase(model_predictions_total[24h]))",
            "legendFormat": "Total Predictions"
          }
        ]
      },
      {
        "title": "Model Performance Trends",
        "type": "graph",
        "targets": [
          {
            "expr": "model_performance_score",
            "legendFormat": "{{model_name}} - {{metric_name}}"
          }
        ]
      },
      {
        "title": "Data Quality Metrics",
        "type": "table",
        "targets": [
          {
            "expr": "data_quality_score",
            "legendFormat": "{{dataset_name}} - {{metric_type}}"
          }
        ]
      },
      {
        "title": "Error Rate",
        "type": "stat",
        "targets": [
          {
            "expr": "rate(model_prediction_errors_total[5m]) / rate(model_predictions_total[5m]) * 100",
            "legendFormat": "Error Rate %"
          }
        ]
      }
    ]
  }
}
```

### 6.3 Logging with ELK Stack

#### What is the ELK Stack?

**ELK Stack** is a collection of three open-source products — Elasticsearch, Logstash, and Kibana — that work together to provide powerful logging and analytics capabilities.

**Components**:
- **Elasticsearch**: Search and analytics engine
- **Logstash**: Data processing pipeline
- **Kibana**: Visualization and exploration interface
- **Beats**: Lightweight data shippers

**Why ELK for MLOps**:
- **Centralized Logging**: Aggregate logs from all components
- **Full-text Search**: Powerful search capabilities
- **Real-time Analytics**: Process and analyze logs in real-time
- **Rich Visualizations**: Create dashboards and charts
- **Scalable**: Handle large volumes of log data

#### Setting Up ELK Stack

**Docker Compose ELK:**
```yaml
# docker-compose.elk.yml
version: '3.8'

services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.6.0
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ports:
      - "9200:9200"
      - "9300:9300"
    volumes:
      - elasticsearch_data:/usr/share/elasticsearch/data
    networks:
      - elk

  logstash:
    image: docker.elastic.co/logstash/logstash:8.6.0
    ports:
      - "5044:5044"
      - "5000:5000"
      - "9600:9600"
    volumes:
      - ./monitoring/logstash/pipeline:/usr/share/logstash/pipeline:ro
      - ./monitoring/logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml:ro
    environment:
      LS_JAVA_OPTS: "-Xmx256m -Xms256m"
    networks:
      - elk
    depends_on:
      - elasticsearch

  kibana:
    image: docker.elastic.co/kibana/kibana:8.6.0
    ports:
      - "5601:5601"
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    networks:
      - elk
    depends_on:
      - elasticsearch

  filebeat:
    image: docker.elastic.co/beats/filebeat:8.6.0
    user: root
    volumes:
      - ./monitoring/filebeat/filebeat.yml:/usr/share/filebeat/filebeat.yml:ro
      - /var/lib/docker/containers:/var/lib/docker/containers:ro
      - /var/run/docker.sock:/var/run/docker.sock:ro
    networks:
      - elk

volumes:
  elasticsearch_data:

networks:
  elk:
    driver: bridge
```

**Logstash Configuration:**
```yaml
# monitoring/logstash/pipeline/logstash.conf
input {
  beats {
    port => 5044
  }

  http {
    port => 5000
    codec => json
  }
}

filter {
  if [kubernetes] {
    mutate {
      add_field => {
        "container_name" => "%{[kubernetes][container][name]}"
        "namespace" => "%{[kubernetes][namespace]}"
        "pod" => "%{[kubernetes][pod][name]}"
      }
    }
  }

  # Parse JSON logs
  json {
    source => "message"
    target => "parsed_json"
  }

  # Extract log level
  grok {
    match => { "message" => "%{LOGLEVEL:log_level}" }
  }

  # Add timestamp
  date {
    match => [ "timestamp", "ISO8601" ]
    target => "@timestamp"
  }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "ml-logs-%{+YYYY.MM.dd}"
  }

  stdout {
    codec => rubydebug
  }
}
```

**Filebeat Configuration:**
```yaml
# monitoring/filebeat/filebeat.yml
filebeat.inputs:
- type: container
  paths:
    - /var/lib/docker/containers/*/*.log
  processors:
  - add_docker_metadata:
      host: "unix:///var/run/docker.sock"
  - decode_json_fields:
      fields: ["message"]
      target: "json"
  - drop_fields:
      fields: ["docker", "container"]

output.logstash:
  hosts: ["logstash:5044"]
```

#### Structured Logging in Python

**Logging Configuration:**
```python
# logging_config.py
import logging
import logging.config
import json
import sys
from datetime import datetime
from typing import Dict, Any

class StructuredFormatter(logging.Formatter):
    """Custom formatter for structured JSON logging"""

    def format(self, record: logging.LogRecord) -> str:
        # Create structured log entry
        log_entry = {
            "timestamp": datetime.utcnow().isoformat() + "Z",
            "level": record.levelname,
            "logger": record.name,
            "message": record.getMessage(),
            "module": record.module,
            "function": record.funcName,
            "line": record.lineno
        }

        # Add extra fields
        if hasattr(record, 'extra_fields'):
            log_entry.update(record.extra_fields)

        # Add exception info
        if record.exc_info:
            log_entry["exception"] = self.formatException(record.exc_info)

        return json.dumps(log_entry)

def setup_logging(log_level: str = "INFO", service_name: str = "ml-api") -> None:
    """Setup structured logging configuration"""

    config = {
        "version": 1,
        "disable_existing_loggers": False,
        "formatters": {
            "structured": {
                "()": StructuredFormatter,
            },
            "simple": {
                "format": "%(asctime)s - %(name)s - %(levelname)s - %(message)s"
            }
        },
        "handlers": {
            "console": {
                "class": "logging.StreamHandler",
                "formatter": "structured",
                "stream": sys.stdout
            },
            "file": {
                "class": "logging.FileHandler",
                "filename": f"/var/log/{service_name}.log",
                "formatter": "structured"
            }
        },
        "root": {
            "level": log_level,
            "handlers": ["console", "file"]
        },
        "loggers": {
            "uvicorn": {
                "level": log_level,
                "handlers": ["console"],
                "propagate": False
            },
            "fastapi": {
                "level": log_level,
                "handlers": ["console"],
                "propagate": False
            }
        }
    }

    logging.config.dictConfig(config)

class StructuredLogger:
    """Structured logger with context"""

    def __init__(self, name: str):
        self.logger = logging.getLogger(name)

    def _log_with_context(self, level: int, message: str, **context: Any) -> None:
        """Log with additional context"""
        extra = {"extra_fields": context} if context else {}
        self.logger.log(level, message, extra=extra)

    def info(self, message: str, **context: Any) -> None:
        self._log_with_context(logging.INFO, message, **context)

    def error(self, message: str, **context: Any) -> None:
        self._log_with_context(logging.ERROR, message, **context)

    def warning(self, message: str, **context: Any) -> None:
        self._log_with_context(logging.WARNING, message, **context)

    def debug(self, message: str, **context: Any) -> None:
        self._log_with_context(logging.DEBUG, message, **context)

# Global logger instance
logger = StructuredLogger("ml-api")
```

**Usage in ML Application:**
```python
# app.py
from logging_config import logger, setup_logging
from fastapi import Request
import time

# Setup logging on startup
setup_logging(log_level="INFO", service_name="ml-api")

@app.middleware("http")
async def logging_middleware(request: Request, call_next):
    """Middleware for request logging"""
    start_time = time.time()

    # Log request
    logger.info(
        "Request started",
        method=request.method,
        url=str(request.url),
        headers=dict(request.headers),
        client_ip=request.client.host if request.client else None
    )

    try:
        response = await call_next(request)

        # Log response
        process_time = time.time() - start_time
        logger.info(
            "Request completed",
            method=request.method,
            url=str(request.url),
            status_code=response.status_code,
            process_time=process_time
        )

        return response

    except Exception as e:
        # Log error
        process_time = time.time() - start_time
        logger.error(
            "Request failed",
            method=request.method,
            url=str(request.url),
            error=str(e),
            process_time=process_time
        )
        raise

@app.post("/predict")
async def predict(request: PredictionRequest):
    """Prediction endpoint with structured logging"""
    logger.info(
        "Starting prediction",
        model_version=request.model_version,
        input_count=len(request.features)
    )

    try:
        # Prediction logic
        predictions = [0.8, 0.3]  # Mock predictions

        logger.info(
            "Prediction completed successfully",
            model_version=request.model_version,
            prediction_count=len(predictions),
            avg_prediction=sum(predictions) / len(predictions)
        )

        return PredictionResponse(
            predictions=predictions,
            model_version=request.model_version,
            processing_time=0.1,
            status="success"
        )

    except Exception as e:
        logger.error(
            "Prediction failed",
            model_version=request.model_version,
            error=str(e),
            error_type=type(e).__name__
        )
        raise HTTPException(status_code=500, detail="Prediction failed")
```

This comprehensive monitoring and observability section provides the foundation for tracking, analyzing, and maintaining ML systems in production environments.
```yaml
# docker-compose.monitoring.yml
version: '3.8'

services:
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./monitoring/prometheus.yml:/etc/prometheus/prometheus.yml:ro
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--web.console.libraries=/etc/prometheus/console_libraries'
      - '--web.console.templates=/etc/prometheus/consoles'
      - '--storage.tsdb.retention.time=200h'
      - '--web.enable-lifecycle'
    networks:
      - monitoring

  node-exporter:
    image: prom/node-exporter:latest
    ports:
      - "9100:9100"
    volumes:
      - /proc:/host/proc:ro
      - /sys:/host/sys:ro
      - /:/rootfs:ro
    command:
      - '--path.procfs=/host/proc'
      - '--path.rootfs=/rootfs'
      - '--path.sysfs=/host/sys'
      - '--collector.filesystem.mount-points-exclude=^/(sys|proc|dev|host|etc)($$|/)'
    networks:
      - monitoring

volumes:
  prometheus_data:

networks:
  monitoring:
    driver: bridge
```

**Prometheus Configuration:**
```yaml
# monitoring/prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "alert_rules.yml"

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - alertmanager:9093

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']

  - job_name: 'ml-api'
    static_configs:
      - targets: ['ml-api:8000']
    scrape_interval: 5s
    metrics_path: /metrics

  - job_name: 'kubernetes-pods'
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
      - action: labelmap
        regex: __meta_kubernetes_pod_label_(.+)
      - source_labels: [__meta_kubernetes_namespace]
        action: replace
        target_label: kubernetes_namespace
      - source_labels: [__meta_kubernetes_pod_name]
        action: replace
        target_label: kubernetes_pod_name
```

#### Custom ML Application Metrics

**FastAPI Metrics Integration:**
```python
# metrics.py
from prometheus_client import Counter, Histogram, Gauge, generate_latest, CONTENT_TYPE_LATEST
from fastapi import Response, Request
import time
from typing import Callable

# Define metrics
REQUEST_COUNT = Counter(
    'http_requests_total',
    'Total number of HTTP requests',
    ['method', 'endpoint', 'status_code']
)

REQUEST_LATENCY = Histogram(
    'http_request_duration_seconds',
    'HTTP request latency in seconds',
    ['method', 'endpoint']
)

ACTIVE_REQUESTS = Gauge(
    'http_requests_active',
    'Number of active HTTP requests',
    ['method', 'endpoint']
)

MODEL_PREDICTIONS = Counter(
    'model_predictions_total',
    'Total number of model predictions',
    ['model_name', 'prediction_class']
)

MODEL_LATENCY = Histogram(
    'model_prediction_duration_seconds',
    'Model prediction latency in seconds',
    ['model_name']
)

DATA_DRIFT_SCORE = Gauge(
    'data_drift_score',
    'Data drift detection score',
    ['feature_name']
)

MODEL_ACCURACY = Gauge(
    'model_accuracy',
    'Current model accuracy on recent data',
    ['model_name']
)

# Custom metrics for ML
FEATURE_COUNT = Counter(
    'feature_requests_total',
    'Total number of feature requests',
    ['feature_type']
)

CACHE_HITS = Counter(
    'cache_hits_total',
    'Total number of cache hits',
    ['cache_type']
)

CACHE_MISSES = Counter(
    'cache_misses_total',
    'Total number of cache misses',
    ['cache_type']
)

def metrics_endpoint():
    """Prometheus metrics endpoint"""
    return Response(generate_latest(), media_type=CONTENT_TYPE_LATEST)

# Middleware for automatic metrics collection
class MetricsMiddleware:
    def __init__(self, app):
        self.app = app
    
    async def __call__(self, scope, receive, send):
        if scope["type"] != "http":
            await self.app(scope, receive, send)
            return
        
        start_time = time.time()
        method = scope["method"]
        path = scope["path"]
        
        # Increment active requests
        ACTIVE_REQUESTS.labels(method=method, endpoint=path).inc()
        
        # Create response handler
        async def send_wrapper(message):
            if message["type"] == "http.response.start":
                status_code = message["status"]
                REQUEST_COUNT.labels(
                    method=method,
                    endpoint=path,
                    status_code=status_code
                ).inc()
            
            if message["type"] == "http.response.body":
                # Decrement active requests
                ACTIVE_REQUESTS.labels(method=method, endpoint=path).dec()
                
                # Record latency
                latency = time.time() - start_time
                REQUEST_LATENCY.labels(method=method, endpoint=path).observe(latency)
            
            await send(message)
        
        await self.app(scope, receive, send_wrapper)

# Model monitoring functions
def record_prediction(model_name: str, prediction_class: int, latency: float):
    """Record model prediction metrics"""
    MODEL_PREDICTIONS.labels(model_name=model_name, prediction_class=prediction_class).inc()
    MODEL_LATENCY.labels(model_name=model_name).observe(latency)

def update_data_drift_score(feature_name: str, score: float):
    """Update data drift score"""
    DATA_DRIFT_SCORE.labels(feature_name=feature_name).set(score)

def update_model_accuracy(model_name: str, accuracy: float):
    """Update model accuracy metric"""
    MODEL_ACCURACY.labels(model_name=model_name).set(accuracy)

def record_feature_request(feature_type: str):
    """Record feature engineering requests"""
    FEATURE_COUNT.labels(feature_type=feature_type).inc()

def record_cache_operation(cache_type: str, hit: bool):
    """Record cache operations"""
    if hit:
        CACHE_HITS.labels(cache_type=cache_type).inc()
    else:
        CACHE_MISSES.labels(cache_type=cache_type).inc()
```

**Integration with FastAPI:**
```python
# main.py
from fastapi import FastAPI, Request
from metrics import (
    metrics_endpoint, MetricsMiddleware, record_prediction,
    update_model_accuracy, MODEL_LATENCY
)
import time
import numpy as np

app = FastAPI()

# Add metrics middleware
app.middleware("http")(MetricsMiddleware)

# Metrics endpoint
@app.get("/metrics")
async def get_metrics():
    return metrics_endpoint()

# Example prediction endpoint with monitoring
@app.post("/predict")
async def predict(request: Request):
    start_time = time.time()
    
    # Simulate prediction
    prediction = np.random.randint(0, 2)
    latency = time.time() - start_time
    
    # Record metrics
    record_prediction("churn_model", prediction, latency)
    
    # Update accuracy (would be calculated from recent predictions)
    update_model_accuracy("churn_model", 0.85)
    
    return {
        "prediction": prediction,
        "latency": latency,
        "model_version": "v1.0.0"
    }

# Health check with metrics
@app.get("/health")
async def health():
    return {"status": "healthy"}
```

#### Alert Rules Configuration

**Alert Rules:**
```yaml
# monitoring/alert_rules.yml
groups:
  - name: ml_api_alerts
    rules:
      - alert: HighRequestLatency
        expr: histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m])) > 2
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High request latency detected"
          description: "95th percentile request latency is {{ $value }}s"

      - alert: HighErrorRate
        expr: rate(http_requests_total{status_code=~"5.."}[5m]) / rate(http_requests_total[5m]) > 0.05
        for: 2m
        labels:
          severity: critical
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value | humanizePercentage }}"

      - alert: ModelAccuracyDrop
        expr: model_accuracy < 0.8
        for: 10m
        labels:
          severity: warning
        annotations:
          summary: "Model accuracy dropped"
          description: "Model accuracy is {{ $value }}"

      - alert: DataDriftDetected
        expr: data_drift_score > 0.7
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "Data drift detected"
          description: "Data drift score for {{ $labels.feature_name }} is {{ $value }}"

      - alert: HighMemoryUsage
        expr: (1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes) > 0.9
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High memory usage"
          description: "Memory usage is {{ $value | humanizePercentage }}"

      - alert: HighCPUUsage
        expr: rate(node_cpu_seconds_total{mode!="idle"}[5m]) > 0.9
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High CPU usage"
          description: "CPU usage is {{ $value | humanizePercentage }}"
```

### 6.2 Grafana Dashboards

Grafana provides visualization capabilities for monitoring data collected by Prometheus.

#### Setting Up Grafana

**Docker Compose Configuration:**
```yaml
# docker-compose.grafana.yml
version: '3.8'

services:
  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin
      - GF_USERS_ALLOW_SIGN_UP=false
    volumes:
      - grafana_data:/var/lib/grafana
      - ./monitoring/grafana/provisioning:/etc/grafana/provisioning
      - ./monitoring/grafana/dashboards:/var/lib/grafana/dashboards
    networks:
      - monitoring

volumes:
  grafana_data:

networks:
  monitoring:
    external: true
```

#### Grafana Provisioning

**Data Source Configuration:**
```yaml
# monitoring/grafana/provisioning/datasources/prometheus.yml
apiVersion: 1

datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    url: http://prometheus:9090
    isDefault: true
    editable: true
```

**Dashboard Provisioning:**
```yaml
# monitoring/grafana/provisioning/dashboards/dashboard.yml
apiVersion: 1

providers:
  - name: 'ML Monitoring'
    type: file
    disableDeletion: false
    updateIntervalSeconds: 10
    allowUiUpdates: true
    options:
      path: /var/lib/grafana/dashboards
```

#### ML Application Dashboard

**Dashboard JSON:**
```json
{
  "dashboard": {
    "title": "ML Application Monitoring",
    "tags": ["ml", "monitoring"],
    "timezone": "browser",
    "panels": [
      {
        "title": "Request Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total[5m])",
            "legendFormat": "Requests per second"
          }
        ],
        "yAxes": [
          {
            "unit": "reqps"
          }
        ]
      },
      {
        "title": "Request Latency",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "95th percentile"
          },
          {
            "expr": "histogram_quantile(0.50, rate(http_request_duration_seconds_bucket[5m]))",
            "legendFormat": "50th percentile"
          }
        ],
        "yAxes": [
          {
            "unit": "s"
          }
        ]
      },
      {
        "title": "Error Rate",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(http_requests_total{status_code=~\"5..\"}[5m]) / rate(http_requests_total[5m]) * 100",
            "legendFormat": "Error rate %"
          }
        ],
        "yAxes": [
          {
            "unit": "percent"
          }
        ]
      },
      {
        "title": "Model Predictions",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(model_predictions_total[5m])",
            "legendFormat": "{{ prediction_class }}"
          }
        ]
      },
      {
        "title": "Model Latency",
        "type": "graph",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(model_prediction_duration_seconds_bucket[5m]))",
            "legendFormat": "95th percentile"
          }
        ],
        "yAxes": [
          {
            "unit": "s"
          }
        ]
      },
      {
        "title": "Model Accuracy",
        "type": "gauge",
        "targets": [
          {
            "expr": "model_accuracy",
            "legendFormat": "{{ model_name }}"
          }
        ],
        "fieldConfig": {
          "defaults": {
            "min": 0,
            "max": 1,
            "unit": "percentunit"
          }
        }
      },
      {
        "title": "Data Drift Score",
        "type": "graph",
        "targets": [
          {
            "expr": "data_drift_score",
            "legendFormat": "{{ feature_name }}"
          }
        ]
      },
      {
        "title": "System Resources",
        "type": "row",
        "collapsed": false
      },
      {
        "title": "CPU Usage",
        "type": "graph",
        "targets": [
          {
            "expr": "rate(node_cpu_seconds_total{mode!=\"idle\"}[5m]) * 100",
            "legendFormat": "CPU Usage %"
          }
        ]
      },
      {
        "title": "Memory Usage",
        "type": "graph",
        "targets": [
          {
            "expr": "(1 - node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes) * 100",
            "legendFormat": "Memory Usage %"
          }
        ]
      },
      {
        "title": "Disk Usage",
        "type": "graph",
        "targets": [
          {
            "expr": "(1 - node_filesystem_avail_bytes / node_filesystem_size_bytes) * 100",
            "legendFormat": "{{ mountpoint }}"
          }
        ]
      }
    ],
    "time": {
      "from": "now-1h",
      "to": "now"
    },
    "refresh": "30s"
  }
}
```

### 6.3 Logging with ELK Stack

The ELK stack (Elasticsearch, Logstash, Kibana) provides comprehensive log aggregation and analysis.

#### ELK Stack Setup

**Docker Compose Configuration:**
```yaml
# docker-compose.elk.yml
version: '3.8'

services:
  elasticsearch:
    image: docker.elastic.co/elasticsearch/elasticsearch:8.6.0
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ports:
      - "9200:9200"
      - "9300:9300"
    volumes:
      - elasticsearch_data:/usr/share/elasticsearch/data
    networks:
      - logging

  logstash:
    image: docker.elastic.co/logstash/logstash:8.6.0
    ports:
      - "5044:5044"
      - "5000:5000"
      - "9600:9600"
    volumes:
      - ./monitoring/logstash/pipeline:/usr/share/logstash/pipeline:ro
      - ./monitoring/logstash/config/logstash.yml:/usr/share/logstash/config/logstash.yml:ro
    environment:
      LS_JAVA_OPTS: "-Xmx256m -Xms256m"
    networks:
      - logging
    depends_on:
      - elasticsearch

  kibana:
    image: docker.elastic.co/kibana/kibana:8.6.0
    ports:
      - "5601:5601"
    environment:
      - ELASTICSEARCH_HOSTS=http://elasticsearch:9200
    networks:
      - logging
    depends_on:
      - elasticsearch

volumes:
  elasticsearch_data:

networks:
  logging:
    driver: bridge
```

#### Logstash Configuration

**Pipeline Configuration:**
```yaml
# monitoring/logstash/pipeline/logstash.conf
input {
  tcp {
    port => 5000
    codec => json
  }
  
  http {
    port => 8080
    codec => json
  }
}

filter {
  # Parse timestamp
  date {
    match => ["timestamp", "ISO8601"]
    target => "@timestamp"
  }
  
  # Add geoip information
  if [client_ip] {
    geoip {
      source => "client_ip"
      target => "geoip"
    }
  }
  
  # Parse user agent
  if [user_agent] {
    useragent {
      source => "user_agent"
      target => "useragent"
    }
  }
  
  # ML-specific filtering
  if [level] == "ERROR" or [status_code] =~ /^5/ {
    mutate {
      add_tag => ["error"]
    }
  }
  
  if [endpoint] =~ /predict/ {
    mutate {
      add_tag => ["prediction"]
    }
  }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "ml-logs-%{+YYYY.MM.dd}"
  }
  
  # Also output to stdout for debugging
  stdout {
    codec => rubydebug
  }
}
```

#### Structured Logging in Python

**Logging Configuration:**
```python
# logging_config.py
import logging
import logging.config
import json
import sys
from datetime import datetime
from pythonjsonlogger import jsonlogger

class MLJsonFormatter(jsonlogger.JsonFormatter):
    """Custom JSON formatter for ML applications"""
    
    def add_fields(self, log_record, record, message_dict):
        super().add_fields(log_record, record, message_dict)
        
        # Add ML-specific fields
        log_record['timestamp'] = datetime.utcnow().isoformat()
        log_record['service'] = 'ml-api'
        log_record['version'] = '1.0.0'
        
        # Add request context if available
        if hasattr(record, 'request_id'):
            log_record['request_id'] = record.request_id
        
        if hasattr(record, 'user_id'):
            log_record['user_id'] = record.user_id
        
        # Add model context
        if hasattr(record, 'model_name'):
            log_record['model_name'] = record.model_name
        
        if hasattr(record, 'model_version'):
            log_record['model_version'] = record.model_version

def setup_logging(log_level=logging.INFO, log_to_file=True):
    """Setup structured logging for ML application"""
    
    # Create logger
    logger = logging.getLogger()
    logger.setLevel(log_level)
    
    # Remove existing handlers
    for handler in logger.handlers[:]:
        logger.removeHandler(handler)
    
    # JSON formatter for structured logging
    json_formatter = MLJsonFormatter(
        '%(timestamp)s %(levelname)s %(service)s %(message)s'
    )
    
    # Console handler
    console_handler = logging.StreamHandler(sys.stdout)
    console_handler.setFormatter(json_formatter)
    logger.addHandler(console_handler)
    
    # File handler (if enabled)
    if log_to_file:
        file_handler = logging.FileHandler('logs/ml-api.log')
        file_handler.setFormatter(json_formatter)
        logger.addHandler(file_handler)
    
    return logger

# Custom log record factory to add context
old_factory = logging.getLogRecordFactory()

def record_factory(*args, **kwargs):
    record = old_factory(*args, **kwargs)
    
    # Add context from thread-local or context variables
    try:
        from flask import g, has_request_context
        if has_request_context():
            record.request_id = getattr(g, 'request_id', None)
            record.user_id = getattr(g, 'user_id', None)
    except ImportError:
        pass
    
    return record

logging.setLogRecordFactory(record_factory)

# Usage example
logger = setup_logging()

# Basic logging
logger.info("Application started", extra={"startup_time": 1.2})

# Request logging
logger.info("Prediction request received", extra={
    "request_id": "req-123",
    "model_name": "churn_model",
    "model_version": "v1.0.0",
    "input_features": 15
})

# Error logging
try:
    # Some operation that might fail
    result = risky_operation()
except Exception as e:
    logger.error("Operation failed", extra={
        "error_type": type(e).__name__,
        "error_message": str(e),
        "request_id": "req-123"
    })
```

#### Kibana Dashboards for Log Analysis

**Kibana Index Pattern:**
```json
{
  "title": "ml-logs-*",
  "timeFieldName": "@timestamp",
  "fields": [
    {
      "name": "@timestamp",
      "type": "date"
    },
    {
      "name": "level",
      "type": "keyword"
    },
    {
      "name": "message",
      "type": "text"
    },
    {
      "name": "service",
      "type": "keyword"
    },
    {
      "name": "request_id",
      "type": "keyword"
    }
  ]
}
```

**Sample Kibana Queries:**
```json
// Error logs from last hour
{
  "query": {
    "bool": {
      "must": [
        { "term": { "level": "ERROR" } },
        { "range": { "@timestamp": { "gte": "now-1h" } } }
      ]
    }
  }
}

// Prediction requests by model
{
  "query": {
    "bool": {
      "must": [
        { "term": { "endpoint": "/predict" } },
        { "term": { "method": "POST" } }
      ]
    }
  },
  "aggs": {
    "by_model": {
      "terms": { "field": "model_name" }
    }
  }
}

// Slow requests (>1 second)
{
  "query": {
    "bool": {
      "must": [
        { "range": { "response_time": { "gte": 1000 } } }
      ]
    }
  }
}
```

#### Distributed Tracing

**OpenTelemetry Integration:**
```python
# tracing.py
from opentelemetry import trace
from opentelemetry.exporter.jaeger import JaegerExporter
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.instrumentation.fastapi import FastAPIInstrumentor
from opentelemetry.instrumentation.requests import RequestsInstrumentor

def setup_tracing(service_name="ml-api"):
    """Setup distributed tracing with OpenTelemetry"""
    
    # Set up tracer provider
    trace.set_tracer_provider(TracerProvider())
    tracer = trace.get_tracer(__name__)
    
    # Configure Jaeger exporter
    jaeger_exporter = JaegerExporter(
        agent_host_name="jaeger",
        agent_port=6831,
    )
    
    # Add span processor
    span_processor = BatchSpanProcessor(jaeger_exporter)
    trace.get_tracer_provider().add_span_processor(span_processor)
    
    return tracer

# Usage in FastAPI app
from fastapi import FastAPI
from tracing import setup_tracing

app = FastAPI()
tracer = setup_tracing()

# Instrument FastAPI
FastAPIInstrumentor.instrument_app(app)

# Instrument HTTP requests
RequestsInstrumentor().instrument()

@app.post("/predict")
async def predict(request_data: dict):
    with tracer.start_as_current_span("prediction_pipeline") as span:
        span.set_attribute("model.name", "churn_model")
        span.set_attribute("model.version", "v1.0.0")
        span.set_attribute("input.features_count", len(request_data.get("features", [])))
        
        with tracer.start_as_current_span("data_preprocessing") as child_span:
            # Preprocessing logic
            child_span.set_attribute("preprocessing.steps", 3)
            # ... preprocessing code ...
        
        with tracer.start_as_current_span("model_inference") as child_span:
            # Model inference
            start_time = time.time()
            # ... inference code ...
            inference_time = time.time() - start_time
            child_span.set_attribute("inference.time_ms", inference_time * 1000)
        
        return {"prediction": 1, "confidence": 0.85}
```

This comprehensive monitoring and observability setup provides deep insights into ML system performance, reliability, and user experience. The combination of metrics, logs, and traces enables proactive issue detection and rapid troubleshooting in production environments.

## 7. Security and Compliance

### 7.1 Container Security

#### What is Container Security?

**Container Security** encompasses the practices, tools, and policies designed to protect containerized applications and their underlying infrastructure from security threats. It addresses the unique security challenges introduced by containerization, including image vulnerabilities, runtime threats, and orchestration security.

**Key Security Principles**:
- **Defense in Depth**: Multiple layers of security controls
- **Least Privilege**: Minimal required permissions and access
- **Secure by Default**: Security features enabled by default
- **Continuous Monitoring**: Ongoing security assessment and monitoring
- **Immutable Infrastructure**: Containers are immutable and replaced rather than modified

**Why Container Security Matters in MLOps**:
- **Model Protection**: ML models contain valuable intellectual property
- **Data Privacy**: Sensitive training data and user data protection
- **Supply Chain Security**: Dependencies and base images may contain vulnerabilities
- **Runtime Threats**: Containers run in shared environments with potential lateral movement
- **Compliance Requirements**: Regulatory requirements for data protection and privacy

#### Docker Security Best Practices

**Secure Dockerfile:**
```dockerfile
# Use official base images from trusted registries
FROM python:3.9-slim@sha256:abcdef1234567890

# Create non-root user at the beginning
RUN groupadd -r mluser --gid=1000 && \
    useradd -r -g mluser --uid=1000 --shell=/bin/bash mluser

# Set working directory with proper permissions
WORKDIR /app
RUN chown mluser:mluser /app

# Install system dependencies securely
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        ca-certificates \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get clean \
    && rm -rf /var/cache/apt/*

# Copy and install Python dependencies
COPY --chown=mluser:mluser requirements.txt ./
RUN pip install --no-cache-dir --user --no-deps -r requirements.txt

# Copy application code with proper ownership
COPY --chown=mluser:mluser src/ ./src/
COPY --chown=mluser:mluser models/ ./models/

# Create necessary directories with proper permissions
RUN mkdir -p /app/logs /app/data && \
    chown -R mluser:mluser /app/logs /app/data

# Switch to non-root user before final operations
USER mluser

# Add security-related environment variables
ENV PYTHONPATH=/app/src:$PYTHONPATH \
    PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

# Health check with security considerations
HEALTHCHECK --interval=30s --timeout=10s --start-period=30s --retries=3 \
    CMD python -c "import sys; sys.exit(0)" || exit 1

# Expose only necessary port
EXPOSE 8000

# Use exec form for CMD to avoid shell injection
CMD ["python", "-m", "uvicorn", "src.app:app", "--host", "0.0.0.0", "--port", "8000"]
```

**Security Scanning:**
```bash
# Trivy - Comprehensive vulnerability scanner
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
    aquasec/trivy:latest image \
    --format json \
    --output trivy-results.json \
    your-registry/ml-api:latest

# Clair - Open-source vulnerability scanner
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
    --network container:clair \
    quay.io/projectquay/clair:latest \
    clair-scanner --ip clair your-registry/ml-api:latest

# Snyk - Developer-first security testing
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
    -e SNYK_TOKEN=$SNYK_TOKEN \
    snyk/snyk:docker your-registry/ml-api:latest

# Anchore Engine - Detailed image analysis
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock \
    anchore/engine-cli:latest \
    anchore-cli image add your-registry/ml-api:latest

# Check results
anchore-cli image vuln your-registry/ml-api:latest all
```

#### Container Runtime Security

**Seccomp Profiles:**
Seccomp (Secure Computing Mode) is a Linux kernel feature that restricts the system calls available to a process.

```json
{
  "defaultAction": "SCMP_ACT_ERRNO",
  "architectures": ["SCMP_ARCH_X86_64"],
  "syscalls": [
    {
      "names": ["accept", "accept4", "access", "bind", "brk", "capget", "capset"],
      "action": "SCMP_ACT_ALLOW"
    },
    {
      "names": ["clone", "close", "connect", "dup", "dup2", "dup3"],
      "action": "SCMP_ACT_ALLOW"
    }
  ]
}
```

**AppArmor/SELinux Profiles:**
```yaml
# Kubernetes Security Context
apiVersion: v1
kind: Pod
metadata:
  name: secure-ml-pod
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 1000
    fsGroup: 1000
    runAsNonRoot: true
  containers:
  - name: ml-api
    image: secure-ml-api:latest
    securityContext:
      allowPrivilegeEscalation: false
      readOnlyRootFilesystem: true
      capabilities:
        drop:
        - ALL
        add:
        - NET_BIND_SERVICE
      seccompProfile:
        type: Localhost
        localhostProfile: profiles/secure-ml-profile.json
    volumeMounts:
    - name: tmp-volume
      mountPath: /tmp
    - name: models-volume
      mountPath: /models
      readOnly: true
  volumes:
  - name: tmp-volume
    emptyDir: {}
  - name: models-volume
    persistentVolumeClaim:
      claimName: models-pvc
```

**Runtime Security Monitoring:**
```python
# runtime_security.py
import docker
import logging
from typing import Dict, List
import time
from dataclasses import dataclass

@dataclass
class SecurityEvent:
    container_id: str
    event_type: str
    severity: str
    description: str
    timestamp: float

class ContainerSecurityMonitor:
    """Monitor container security events"""

    def __init__(self):
        self.client = docker.from_env()
        self.logger = logging.getLogger(__name__)
        self.security_events: List[SecurityEvent] = []

    def monitor_containers(self):
        """Monitor running containers for security events"""
        while True:
            try:
                containers = self.client.containers.list()

                for container in containers:
                    self.check_container_security(container)

                time.sleep(60)  # Check every minute

            except Exception as e:
                self.logger.error(f"Monitoring error: {e}")

    def check_container_security(self, container):
        """Check individual container security"""
        container_info = container.attrs

        # Check if running as root
        user = container_info.get('Config', {}).get('User', '')
        if not user or user == '0' or user == 'root':
            self.log_security_event(
                container.id,
                "privilege_escalation",
                "HIGH",
                "Container running as root user"
            )

        # Check for sensitive mounts
        mounts = container_info.get('Mounts', [])
        for mount in mounts:
            if mount.get('Source', '').startswith('/etc') or \
               mount.get('Source', '').startswith('/var/run'):
                self.log_security_event(
                    container.id,
                    "sensitive_mount",
                    "MEDIUM",
                    f"Sensitive host path mounted: {mount.get('Source')}"
                )

        # Check capabilities
        security_opts = container_info.get('HostConfig', {}).get('SecurityOpt', [])
        if not any('no-new-privileges' in opt for opt in security_opts):
            self.log_security_event(
                container.id,
                "missing_security_option",
                "MEDIUM",
                "Container missing no-new-privileges security option"
            )

    def log_security_event(self, container_id: str, event_type: str,
                          severity: str, description: str):
        """Log security event"""
        event = SecurityEvent(
            container_id=container_id,
            event_type=event_type,
            severity=severity,
            description=description,
            timestamp=time.time()
        )

        self.security_events.append(event)
        self.logger.warning(f"Security Event: {event}")

        # In production, send to SIEM or alerting system
        if severity == "HIGH":
            self.alert_security_team(event)

    def alert_security_team(self, event: SecurityEvent):
        """Send alert to security team"""
        # Implementation would integrate with PagerDuty, Slack, etc.
        self.logger.critical(f"CRITICAL SECURITY ALERT: {event}")

# Global security monitor
security_monitor = ContainerSecurityMonitor()
```

### 7.2 Infrastructure Security

#### Cloud Infrastructure Security

**AWS Security Best Practices:**
```yaml
# CloudFormation template with security controls
AWSTemplateFormatVersion: '2010-09-09'
Description: 'Secure ML Infrastructure'

Resources:
  VPC:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: 10.0.0.0/16
      EnableDnsHostnames: true
      EnableDnsSupport: true
      Tags:
        - Key: Name
          Value: ml-vpc

  # Security Groups with minimal access
  MLSecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Security group for ML API
      VpcId: !Ref VPC
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 443
          ToPort: 443
          CidrIp: 0.0.0.0/0  # Restrict in production
        - IpProtocol: tcp
          FromPort: 80
          ToPort: 80
          CidrIp: 0.0.0.0/0  # Restrict in production

  # IAM Role with least privilege
  MLIAMRole:
    Type: AWS::IAM::Role
    Properties:
      RoleName: ml-api-role
      AssumeRolePolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Principal:
              Service: ec2.amazonaws.com
            Action: sts:AssumeRole
      ManagedPolicyArns:
        - arn:aws:iam::aws:policy/AmazonEC2ReadOnlyAccess
        - arn:aws:iam::aws:policy/CloudWatchLogsFullAccess
      Policies:
        - PolicyName: MLS3Access
          PolicyDocument:
            Version: '2012-10-17'
            Statement:
              - Effect: Allow
                Action:
                  - s3:GetObject
                  - s3:PutObject
                Resource: arn:aws:s3:::ml-models-bucket/models/*

  # Encrypted EBS volume for models
  ModelVolume:
    Type: AWS::EC2::Volume
    Properties:
      Size: 100
      VolumeType: gp3
      Encrypted: true
      KmsKeyId: !Ref ModelKMSKey
      AvailabilityZone: !GetAtt EC2Instance.AvailabilityZone

  # KMS key for encryption
  ModelKMSKey:
    Type: AWS::KMS::Key
    Properties:
      Description: KMS key for ML model encryption
      KeyPolicy:
        Version: '2012-10-17'
        Statement:
          - Sid: Enable IAM User Permissions
            Effect: Allow
            Principal:
              AWS: !Sub arn:aws:iam::${AWS::AccountId}:root
            Action: kms:*
            Resource: '*'
```

**Network Security:**
```yaml
# Kubernetes Network Policies
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: ml-api-network-policy
  namespace: ml-production
spec:
  podSelector:
    matchLabels:
      app: ml-api
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: ingress-nginx
    ports:
    - protocol: TCP
      port: 8000
  - from:
    - podSelector:
        matchLabels:
          app: ml-monitoring
    ports:
    - protocol: TCP
      port: 8000
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: postgres
    ports:
    - protocol: TCP
      port: 5432
  - to:
    - podSelector:
        matchLabels:
          app: redis
    ports:
    - protocol: TCP
      port: 6379
  - to: []  # Deny all other egress traffic
```

#### Data Encryption

**At-Rest Encryption:**
```python
# encryption.py
from cryptography.fernet import Fernet
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC
import base64
import os
from typing import bytes, str

class DataEncryption:
    """Handle data encryption for ML models and sensitive data"""

    def __init__(self, key: bytes = None):
        if key is None:
            # Generate a key from environment variable or create new
            key_env = os.getenv('ENCRYPTION_KEY')
            if key_env:
                key = base64.urlsafe_b64decode(key_env)
            else:
                key = Fernet.generate_key()

        self.fernet = Fernet(key)
        self._key = key

    @classmethod
    def from_password(cls, password: str, salt: bytes = None) -> 'DataEncryption':
        """Create encryption instance from password"""
        if salt is None:
            salt = os.urandom(16)

        kdf = PBKDF2HMAC(
            algorithm=hashes.SHA256(),
            length=32,
            salt=salt,
            iterations=100000,
        )
        key = base64.urlsafe_b64encode(kdf.derive(password.encode()))
        return cls(key)

    def encrypt_data(self, data: bytes) -> bytes:
        """Encrypt data"""
        return self.fernet.encrypt(data)

    def decrypt_data(self, encrypted_data: bytes) -> bytes:
        """Decrypt data"""
        return self.fernet.decrypt(encrypted_data)

    def encrypt_file(self, input_path: str, output_path: str):
        """Encrypt a file"""
        with open(input_path, 'rb') as f:
            data = f.read()

        encrypted_data = self.encrypt_data(data)

        with open(output_path, 'wb') as f:
            f.write(encrypted_data)

    def decrypt_file(self, input_path: str, output_path: str):
        """Decrypt a file"""
        with open(input_path, 'rb') as f:
            encrypted_data = f.read()

        decrypted_data = self.decrypt_data(encrypted_data)

        with open(output_path, 'wb') as f:
            f.write(decrypted_data)

    @property
    def key_b64(self) -> str:
        """Get base64 encoded key for storage"""
        return base64.urlsafe_b64encode(self._key).decode()

# Model encryption wrapper
class ModelEncryption:
    """Encrypt and decrypt ML models"""

    def __init__(self, encryption_key: str = None):
        self.encryption = DataEncryption()
        if encryption_key:
            # Use provided key
            key_bytes = base64.urlsafe_b64decode(encryption_key)
            self.encryption = DataEncryption(key_bytes)

    def save_encrypted_model(self, model, filepath: str):
        """Save model in encrypted format"""
        import pickle

        # Serialize model
        model_data = pickle.dumps(model)

        # Encrypt
        encrypted_data = self.encryption.encrypt_data(model_data)

        # Save
        with open(filepath, 'wb') as f:
            f.write(encrypted_data)

    def load_encrypted_model(self, filepath: str):
        """Load encrypted model"""
        import pickle

        # Load encrypted data
        with open(filepath, 'rb') as f:
            encrypted_data = f.read()

        # Decrypt
        decrypted_data = self.encryption.decrypt_data(encrypted_data)

        # Deserialize
        model = pickle.loads(decrypted_data)
        return model
```

**In-Transit Encryption:**
```python
# secure_api.py
from fastapi import FastAPI, HTTPException, Request
from fastapi.security import HTTPBearer, HTTPAuthorizationCredentials
from fastapi.middleware.httpsredirect import HTTPSRedirectMiddleware
from starlette.middleware.base import BaseHTTPMiddleware
import jwt
import time
from typing import Optional
import logging

logger = logging.getLogger(__name__)

class SecurityHeadersMiddleware(BaseHTTPMiddleware):
    """Add security headers to all responses"""

    async def dispatch(self, request: Request, call_next):
        response = await call_next(request)

        # Security headers
        response.headers["X-Content-Type-Options"] = "nosniff"
        response.headers["X-Frame-Options"] = "DENY"
        response.headers["X-XSS-Protection"] = "1; mode=block"
        response.headers["Strict-Transport-Security"] = "max-age=31536000; includeSubDomains"
        response.headers["Content-Security-Policy"] = "default-src 'self'"

        # Remove server header
        response.headers.pop("Server", None)

        return response

class RateLimitMiddleware(BaseHTTPMiddleware):
    """Simple rate limiting middleware"""

    def __init__(self, app, requests_per_minute: int = 60):
        super().__init__(app)
        self.requests_per_minute = requests_per_minute
        self.requests = {}

    async def dispatch(self, request: Request, call_next):
        client_ip = request.client.host
        current_time = time.time()
        window_start = current_time - 60  # 1 minute window

        # Clean old requests
        if client_ip in self.requests:
            self.requests[client_ip] = [
                req_time for req_time in self.requests[client_ip]
                if req_time > window_start
            ]
        else:
            self.requests[client_ip] = []

        # Check rate limit
        if len(self.requests[client_ip]) >= self.requests_per_minute:
            raise HTTPException(status_code=429, detail="Rate limit exceeded")

        # Add current request
        self.requests[client_ip].append(current_time)

        response = await call_next(request)
        return response

app = FastAPI(title="Secure ML API")

# Add security middleware
app.add_middleware(SecurityHeadersMiddleware)
app.add_middleware(RateLimitMiddleware, requests_per_minute=100)
app.add_middleware(HTTPSRedirectMiddleware)  # Redirect HTTP to HTTPS

# JWT settings
JWT_SECRET = os.getenv("JWT_SECRET", "your-secret-key")
JWT_ALGORITHM = "HS256"

security = HTTPBearer()

def create_access_token(data: dict, expires_delta: Optional[int] = None):
    """Create JWT access token"""
    to_encode = data.copy()
    if expires_delta:
        expire = time.time() + expires_delta
    else:
        expire = time.time() + 900  # 15 minutes
    to_encode.update({"exp": expire})
    encoded_jwt = jwt.encode(to_encode, JWT_SECRET, algorithm=JWT_ALGORITHM)
    return encoded_jwt

def verify_token(credentials: HTTPAuthorizationCredentials = security):
    """Verify JWT token"""
    try:
        payload = jwt.decode(credentials.credentials, JWT_SECRET, algorithms=[JWT_ALGORITHM])
        username: str = payload.get("sub")
        if username is None:
            raise HTTPException(status_code=401, detail="Invalid token")
        return username
    except jwt.ExpiredSignatureError:
        raise HTTPException(status_code=401, detail="Token expired")
    except jwt.JWTError:
        raise HTTPException(status_code=401, detail="Invalid token")

@app.post("/auth/login")
async def login(username: str, password: str):
    """Authenticate user and return JWT token"""
    # In production, verify against database
    if username == "admin" and password == "secure_password":
        access_token = create_access_token(data={"sub": username})
        return {"access_token": access_token, "token_type": "bearer"}
    raise HTTPException(status_code=401, detail="Invalid credentials")

@app.post("/predict")
async def predict(request: PredictionRequest, username: str = verify_token):
    """Secure prediction endpoint"""
    logger.info(f"Prediction request from user: {username}")

    try:
        # Prediction logic here
        predictions = [0.8, 0.3]

        return PredictionResponse(
            predictions=predictions,
            model_version="v1.0",
            processing_time=0.1,
            status="success"
        )

    except Exception as e:
        logger.error(f"Prediction error for user {username}: {e}")
        raise HTTPException(status_code=500, detail="Prediction failed")
```

### 7.3 Compliance Automation

#### Regulatory Compliance Frameworks

**GDPR Compliance:**
```python
# gdpr_compliance.py
from datetime import datetime, timedelta
from typing import Dict, List, Optional
import json
import logging
from dataclasses import dataclass, asdict

logger = logging.getLogger(__name__)

@dataclass
class DataProcessingRecord:
    """Record of data processing activity for GDPR compliance"""
    user_id: str
    data_types: List[str]
    purpose: str
    processing_timestamp: datetime
    retention_period_days: int
    consent_given: bool
    consent_timestamp: Optional[datetime] = None
    data_location: str = "EU"

class GDPRComplianceManager:
    """Manage GDPR compliance for ML data processing"""

    def __init__(self):
        self.processing_records: List[DataProcessingRecord] = []
        self.retention_policies = {
            "training_data": 2555,  # 7 years
            "user_predictions": 365,  # 1 year
            "model_metadata": 1825,  # 5 years
        }

    def record_data_processing(self, record: DataProcessingRecord):
        """Record data processing activity"""
        self.processing_records.append(record)
        logger.info(f"Data processing recorded: {record.user_id} - {record.purpose}")

        # Check compliance
        self.check_compliance(record)

    def check_compliance(self, record: DataProcessingRecord):
        """Check GDPR compliance for data processing"""
        issues = []

        # Check consent
        if not record.consent_given:
            issues.append("No user consent recorded")

        # Check data minimization
        if len(record.data_types) > 10:  # Arbitrary threshold
            issues.append("Potential data minimization violation")

        # Check retention period
        max_retention = self.retention_policies.get(record.purpose, 365)
        if record.retention_period_days > max_retention:
            issues.append(f"Retention period exceeds policy: {max_retention} days")

        if issues:
            self.report_compliance_issue(record, issues)

    def report_compliance_issue(self, record: DataProcessingRecord, issues: List[str]):
        """Report compliance issues"""
        logger.warning(f"GDPR Compliance Issue for {record.user_id}: {issues}")

        # In production, this would:
        # 1. Notify compliance officer
        # 2. Log to audit system
        # 3. Potentially block processing
        # 4. Escalate to legal team

    def get_data_portability_request(self, user_id: str) -> Dict:
        """Handle GDPR data portability request"""
        user_records = [
            record for record in self.processing_records
            if record.user_id == user_id
        ]

        return {
            "user_id": user_id,
            "data_processing_records": [asdict(record) for record in user_records],
            "export_timestamp": datetime.now().isoformat(),
            "format": "JSON"
        }

    def handle_data_deletion_request(self, user_id: str) -> bool:
        """Handle GDPR right to erasure"""
        initial_count = len(self.processing_records)

        # Remove all records for user
        self.processing_records = [
            record for record in self.processing_records
            if record.user_id != user_id
        ]

        deleted_count = initial_count - len(self.processing_records)

        if deleted_count > 0:
            logger.info(f"Deleted {deleted_count} records for user {user_id}")
            return True

        return False

    def generate_compliance_report(self) -> Dict:
        """Generate compliance report"""
        total_records = len(self.processing_records)
        consent_rate = sum(1 for r in self.processing_records if r.consent_given) / total_records if total_records > 0 else 0

        # Check retention compliance
        expired_records = []
        for record in self.processing_records:
            retention_date = record.processing_timestamp + timedelta(days=record.retention_period_days)
            if datetime.now() > retention_date:
                expired_records.append(record)

        return {
            "total_processing_records": total_records,
            "consent_rate": consent_rate,
            "expired_records_count": len(expired_records),
            "data_locations": list(set(r.data_location for r in self.processing_records)),
            "report_generated": datetime.now().isoformat()
        }

# Global compliance manager
gdpr_manager = GDPRComplianceManager()
```

**Automated Compliance Monitoring:**
```python
# compliance_monitor.py
import schedule
import time
from datetime import datetime
import logging
from typing import Dict, List
import json

logger = logging.getLogger(__name__)

class ComplianceMonitor:
    """Automated compliance monitoring system"""

    def __init__(self):
        self.compliance_checks = []
        self.alerts = []

    def add_compliance_check(self, name: str, check_function, frequency_hours: int = 24):
        """Add a compliance check"""
        self.compliance_checks.append({
            'name': name,
            'function': check_function,
            'frequency': frequency_hours
        })

    def run_compliance_checks(self):
        """Run all compliance checks"""
        logger.info("Running compliance checks...")

        for check in self.compliance_checks:
            try:
                result = check['function']()
                if not result['compliant']:
                    self.handle_compliance_violation(check['name'], result)
                else:
                    logger.info(f"Compliance check passed: {check['name']}")
            except Exception as e:
                logger.error(f"Compliance check failed: {check['name']} - {e}")

    def handle_compliance_violation(self, check_name: str, result: Dict):
        """Handle compliance violation"""
        alert = {
            'check_name': check_name,
            'violation_details': result,
            'timestamp': datetime.now().isoformat(),
            'severity': result.get('severity', 'MEDIUM')
        }

        self.alerts.append(alert)
        logger.warning(f"Compliance violation: {alert}")

        # Escalate based on severity
        if alert['severity'] == 'HIGH':
            self.escalate_to_compliance_team(alert)
        elif alert['severity'] == 'CRITICAL':
            self.escalate_to_legal_team(alert)

    def escalate_to_compliance_team(self, alert: Dict):
        """Escalate to compliance team"""
        # Implementation would integrate with ticketing system, email, etc.
        logger.critical(f"COMPLIANCE ESCALATION: {alert}")

    def escalate_to_legal_team(self, alert: Dict):
        """Escalate to legal team"""
        logger.critical(f"LEGAL ESCALATION: {alert}")

    def generate_compliance_dashboard(self) -> Dict:
        """Generate compliance dashboard data"""
        recent_alerts = self.alerts[-10:]  # Last 10 alerts

        return {
            'total_checks': len(self.compliance_checks),
            'active_alerts': len([a for a in self.alerts if not a.get('resolved', False)]),
            'recent_alerts': recent_alerts,
            'last_check_time': datetime.now().isoformat()
        }

def check_data_encryption():
    """Check if sensitive data is properly encrypted"""
    # Implementation would check database, files, etc.
    return {
        'compliant': True,  # Mock result
        'details': 'All sensitive data is encrypted at rest',
        'severity': 'LOW'
    }

def check_access_controls():
    """Check access control policies"""
    return {
        'compliant': False,  # Mock violation
        'details': 'Some users have excessive permissions',
        'severity': 'HIGH',
        'affected_users': ['user1', 'user2']
    }

def check_audit_logging():
    """Check audit logging completeness"""
    return {
        'compliant': True,
        'details': 'All actions are properly logged',
        'severity': 'LOW'
    }

# Setup compliance monitoring
monitor = ComplianceMonitor()

# Add compliance checks
monitor.add_compliance_check("Data Encryption", check_data_encryption, 24)
monitor.add_compliance_check("Access Controls", check_access_controls, 12)
monitor.add_compliance_check("Audit Logging", check_audit_logging, 6)

# Schedule checks
schedule.every(24).hours.do(monitor.run_compliance_checks)
schedule.every(6).hours.do(monitor.run_compliance_checks)

def run_monitor():
    """Run the compliance monitor"""
    while True:
        schedule.run_pending()
        time.sleep(60)

if __name__ == "__main__":
    logger.info("Starting compliance monitor...")
    run_monitor()
```

This comprehensive security and compliance section provides the foundation for protecting ML systems and ensuring regulatory compliance in production environments.

**Seccomp and AppArmor Profiles:**
```json
// seccomp-profile.json
{
  "defaultAction": "SCMP_ACT_ERRNO",
  "architectures": ["SCMP_ARCH_X86_64"],
  "syscalls": [
    {
      "names": [
        "accept4",
        "access",
        "arch_prctl",
        "bind",
        "brk",
        "capget",
        "capset",
        "chdir",
        "chmod",
        "chown",
        "chown32",
        "clock_getres",
        "clock_gettime",
        "clock_nanosleep",
        "close",
        "connect",
        "creat",
        "dup",
        "dup2",
        "dup3",
        "epoll_create",
        "epoll_create1",
        "epoll_ctl",
        "epoll_pwait",
        "epoll_wait",
        "execve",
        "exit",
        "exit_group",
        "faccessat",
        "fchdir",
        "fchmod",
        "fchmodat",
        "fchown",
        "fchownat",
        "fcntl",
        "fcntl64",
        "fdatasync",
        "fgetxattr",
        "flistxattr",
        "flock",
        "fork",
        "fremovexattr",
        "fsetxattr",
        "fstat",
        "fstat64",
        "fstatat64",
        "fstatfs",
        "fstatfs64",
        "fsync",
        "ftruncate",
        "ftruncate64",
        "futex",
        "getcwd",
        "getdents",
        "getdents64",
        "getegid",
        "getegid32",
        "geteuid",
        "geteuid32",
        "getgid",
        "getgid32",
        "getgroups",
        "getgroups32",
        "getitimer",
        "getpeername",
        "getpgid",
        "getpgrp",
        "getpid",
        "getppid",
        "getpriority",
        "getrandom",
        "getresgid",
        "getresgid32",
        "getresuid",
        "getresuid32",
        "getrlimit",
        "getrusage",
        "getsid",
        "getsockname",
        "getsockopt",
        "gettid",
        "gettimeofday",
        "getuid",
        "getuid32",
        "getxattr",
        "inotify_add_watch",
        "inotify_init",
        "inotify_init1",
        "inotify_rm_watch",
        "ioctl",
        "ioprio_get",
        "ioprio_set",
        "kill",
        "lchown",
        "lchown32",
        "lgetxattr",
        "llistxattr",
        "lremovexattr",
        "lsetxattr",
        "lseek",
        "lstat",
        "lstat64",
        "madvise",
        "memfd_create",
        "mincore",
        "mkdir",
        "mkdirat",
        "mknod",
        "mknodat",
        "mlock",
        "mlockall",
        "mmap",
        "mmap2",
        "mprotect",
        "mq_getsetattr",
        "mq_notify",
        "mq_open",
        "mq_timedreceive",
        "mq_timedsend",
        "mq_unlink",
        "mremap",
        "msgctl",
        "msgget",
        "msgrcv",
        "msgsnd",
        "msync",
        "munlock",
        "munlockall",
        "munmap",
        "nanosleep",
        "newfstatat",
        "open",
        "openat",
        "pause",
        "pipe",
        "pipe2",
        "poll",
        "ppoll",
        "prctl",
        "pread64",
        "preadv",
        "prlimit64",
        "pselect6",
        "pwrite64",
        "pwritev",
        "read",
        "readahead",
        "readlink",
        "readlinkat",
        "readv",
        "recvfrom",
        "recvmmsg",
        "recvmsg",
        "remap_file_pages",
        "removexattr",
        "rename",
        "renameat",
        "renameat2",
        "rmdir",
        "rt_sigaction",
        "rt_sigpending",
        "rt_sigprocmask",
        "rt_sigsuspend",
        "rt_sigsuspend",
        "rt_sigtimedwait",
        "rt_tgsigqueueinfo",
        "sched_get_priority_max",
        "sched_get_priority_min",
        "sched_getaffinity",
        "sched_getattr",
        "sched_getparam",
        "sched_getscheduler",
        "sched_rr_get_interval",
        "sched_setaffinity",
        "sched_setattr",
        "sched_setparam",
        "sched_setscheduler",
        "sched_yield",
        "select",
        "semctl",
        "semget",
        "semop",
        "semtimedop",
        "semtimedop",
        "sendfile",
        "sendfile64",
        "sendmmsg",
        "sendmsg",
        "sendto",
        "set_robust_list",
        "set_tid_address",
        "setfsgid",
        "setfsgid32",
        "setfsgid32",
        "setfsuid",
        "setfsuid32",
        "setgid",
        "setgid32",
        "setgroups",
        "setgroups32",
        "sethostname",
        "setitimer",
        "setns",
        "setpgid",
        "setpriority",
        "setregid",
        "setregid32",
        "setresgid",
        "setresgid32",
        "setresuid",
        "setresuid32",
        "setreuid",
        "setreuid32",
        "setrlimit",
        "setsid",
        "setsockopt",
        "setuid",
        "setuid32",
        "setxattr",
        "shmat",
        "shmctl",
        "shmdt",
        "shmdt",
        "shmget",
        "shutdown",
        "sigaltstack",
        "signalfd",
        "signalfd4",
        "socket",
        "socketpair",
        "splice",
        "stat",
        "stat64",
        "statfs",
        "statfs64",
        "symlink",
        "symlinkat",
        "sync",
        "sync_file_range",
        "syncfs",
        "sysinfo",
        "syslog",
        "tee",
        "tgkill",
        "time",
        "timer_create",
        "timer_delete",
        "timer_getoverrun",
        "timer_gettime",
        "timer_settime",
        "timerfd_create",
        "timerfd_gettime",
        "timerfd_settime",
        "times",
        "tkill",
        "truncate",
        "truncate64",
        "umask",
        "uname",
        "unlink",
        "unlinkat",
        "unshare",
        "utime",
        "utimensat",
        "utimes",
        "vfork",
        "vmsplice",
        "wait4",
        "waitid",
        "waitpid",
        "write",
        "writev"
      ],
      "action": "SCMP_ACT_ALLOW"
    }
  ]
}
```

**Running Containers with Security:**
```bash
# Run container with security options
docker run --rm \
    --security-opt no-new-privileges:true \
    --security-opt seccomp:seccomp-profile.json \
    --cap-drop ALL \
    --cap-add NET_BIND_SERVICE \
    --read-only \
    --tmpfs /tmp \
    --tmpfs /app/logs \
    -v /app/models:/app/models:ro \
    -p 8000:8000 \
    your-ml-image:latest

# Podman alternative with better defaults
podman run --rm \
    --security-opt no-new-privileges \
    --cap-drop=all \
    --cap-add=NET_BIND_SERVICE \
    -p 8000:8000 \
    your-ml-image:latest
```

### 7.2 Infrastructure Security

Securing the underlying infrastructure that hosts ML workloads requires comprehensive security measures.

#### Kubernetes Security

**Pod Security Standards:**
```yaml
# pod-security-policy.yaml
apiVersion: policy/v1beta1
kind: PodSecurityPolicy
metadata:
  name: ml-workload-psp
spec:
  privileged: false
  allowPrivilegeEscalation: false
  requiredDropCapabilities:
    - ALL
  allowedCapabilities:
    - NET_BIND_SERVICE
  volumes:
    - 'configMap'
    - 'emptyDir'
    - 'projected'
    - 'secret'
    - 'downwardAPI'
    - 'persistentVolumeClaim'
  hostNetwork: false
  hostIPC: false
  hostPID: false
  runAsUser:
    rule: 'MustRunAsNonRoot'
  runAsGroup:
    rule: 'MustRunAs'
    ranges:
    - min: 1000
      max: 65535
  seLinux:
    rule: 'RunAsAny'
  supplementalGroups:
    rule: 'MustRunAs'
    ranges:
    - min: 1000
      max: 65535
  fsGroup:
    rule: 'MustRunAs'
    ranges:
    - min: 1000
      max: 65535
```

**Network Policies:**
```yaml
# network-policy.yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: ml-api-network-policy
  namespace: ml-production
spec:
  podSelector:
    matchLabels:
      app: ml-api
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
          app: ml-api-gateway
    ports:
    - protocol: TCP
      port: 8000
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: redis
    ports:
    - protocol: TCP
      port: 6379
  - to:
    - podSelector:
        matchLabels:
          app: postgres
    ports:
    - protocol: TCP
      port: 5432
  - to: []
    ports:
    - protocol: TCP
      port: 53
    - protocol: UDP
      port: 53
```

**RBAC Configuration:**
```yaml
# rbac.yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: ml-production
  name: ml-developer-role
rules:
- apiGroups: [""]
  resources: ["pods", "pods/log", "pods/exec"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
- apiGroups: ["apps"]
  resources: ["deployments", "replicasets"]
  verbs: ["get", "list", "watch", "create", "update", "patch", "delete"]
- apiGroups: ["mlops.example.com"]
  resources: ["mlmodels", "mlexperiments"]
  verbs: ["get", "list", "watch", "create", "update", "patch"]

---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: ml-developer-binding
  namespace: ml-production
subjects:
- kind: User
  name: ml-developer@example.com
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: ml-developer-role
  apiGroup: rbac.authorization.k8s.io
```

#### Secrets Management

**Kubernetes Secrets:**
```yaml
# secrets.yaml
apiVersion: v1
kind: Secret
metadata:
  name: ml-api-secrets
  namespace: ml-production
type: Opaque
data:
  # Base64 encoded values
  database-password: cGFzc3dvcmQ=  # password
  api-key: YXBpX2tleQ==  # api_key
  jwt-secret: and0dG9rZW4=  # jwt_token

---
apiVersion: v1
kind: Secret
metadata:
  name: ml-registry-secret
  namespace: ml-production
type: kubernetes.io/dockerconfigjson
data:
  .dockerconfigjson: eyJhdXRocyI6eyJyZWdpc3RyeS5leGFtcGxlLmNvbSI6eyJ1c2VybmFtZSI6InVzZXIiLCJwYXNzd29yZCI6InBhc3MiLCJhdXRoIjoiIn19fQ==
```

**External Secrets Operator:**
```yaml
# external-secret.yaml
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: ml-api-external-secret
  namespace: ml-production
spec:
  refreshInterval: 15s
  secretStoreRef:
    name: aws-secretsmanager
    kind: SecretStore
  target:
    name: ml-api-secret
    creationPolicy: Owner
  data:
  - secretKey: database-password
    remoteRef:
      key: prod/ml-api/database
      property: password
  - secretKey: api-key
    remoteRef:
      key: prod/ml-api/api-key
      property: key
```

### 7.3 Data Security and Privacy

Protecting sensitive data used in ML workflows requires encryption, access controls, and compliance measures.

#### Data Encryption

**Application-Level Encryption:**
```python
# encryption.py
import os
from cryptography.fernet import Fernet
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2HMAC
import base64

class DataEncryptor:
    def __init__(self, key: bytes = None):
        if key is None:
            key = self._generate_key()
        self.fernet = Fernet(key)
    
    def _generate_key(self) -> bytes:
        """Generate a new encryption key"""
        # In production, use a proper KMS or key management service
        salt = os.urandom(16)
        kdf = PBKDF2HMAC(
            algorithm=hashes.SHA256(),
            length=32,
            salt=salt,
            iterations=100000,
        )
        key = base64.urlsafe_b64encode(kdf.derive(b"your-secret-key"))
        return key
    
    def encrypt_data(self, data: str) -> str:
        """Encrypt string data"""
        return self.fernet.encrypt(data.encode()).decode()
    
    def decrypt_data(self, encrypted_data: str) -> str:
        """Decrypt string data"""
        return self.fernet.decrypt(encrypted_data.encode()).decode()
    
    def encrypt_dataframe(self, df):
        """Encrypt sensitive columns in pandas DataFrame"""
        encrypted_df = df.copy()
        
        # Define sensitive columns
        sensitive_columns = ['email', 'phone', 'ssn', 'credit_card']
        
        for col in sensitive_columns:
            if col in encrypted_df.columns:
                encrypted_df[col] = encrypted_df[col].astype(str).apply(self.encrypt_data)
        
        return encrypted_df
    
    def decrypt_dataframe(self, df):
        """Decrypt sensitive columns in pandas DataFrame"""
        decrypted_df = df.copy()
        
        sensitive_columns = ['email', 'phone', 'ssn', 'credit_card']
        
        for col in decrypted_df.columns:
            if col in sensitive_columns:
                decrypted_df[col] = decrypted_df[col].astype(str).apply(self.decrypt_data)
        
        return decrypted_df

# Usage
encryptor = DataEncryptor()

# Encrypt sensitive data
sensitive_data = "user@example.com"
encrypted = encryptor.encrypt_data(sensitive_data)
decrypted = encryptor.decrypt_data(encrypted)

print(f"Original: {sensitive_data}")
print(f"Encrypted: {encrypted}")
print(f"Decrypted: {decrypted}")
```

#### Access Control and Auditing

**Row-Level Security (PostgreSQL):**
```sql
-- Enable RLS on tables
ALTER TABLE user_data ENABLE ROW LEVEL SECURITY;

-- Create policy for data access
CREATE POLICY user_data_policy ON user_data
    FOR ALL
    USING (user_id = current_user_id());

-- Create audit trigger
CREATE OR REPLACE FUNCTION audit_trigger_function() RETURNS trigger AS $$
BEGIN
    INSERT INTO audit_log (
        table_name,
        operation,
        old_values,
        new_values,
        user_id,
        timestamp
    ) VALUES (
        TG_TABLE_NAME,
        TG_OP,
        CASE WHEN TG_OP != 'INSERT' THEN row_to_json(OLD) ELSE NULL END,
        CASE WHEN TG_OP != 'DELETE' THEN row_to_json(NEW) ELSE NULL END,
        current_user_id(),
        now()
    );
    RETURN COALESCE(NEW, OLD);
END;
$$ LANGUAGE plpgsql;

-- Apply audit trigger
CREATE TRIGGER user_data_audit_trigger
    AFTER INSERT OR UPDATE OR DELETE ON user_data
    FOR EACH ROW EXECUTE FUNCTION audit_trigger_function();
```

**API Access Control:**
```python
# access_control.py
from fastapi import HTTPException, Depends, Request
from fastapi.security import HTTPBearer, HTTPAuthorizationCredentials
import jwt
from datetime import datetime, timedelta
from typing import Optional
import os

security = HTTPBearer()

class AccessControl:
    def __init__(self):
        self.secret_key = os.getenv("JWT_SECRET_KEY", "your-secret-key")
        self.algorithm = "HS256"
    
    def create_access_token(self, data: dict, expires_delta: Optional[timedelta] = None):
        """Create JWT access token"""
        to_encode = data.copy()
        if expires_delta:
            expire = datetime.utcnow() + expires_delta
        else:
            expire = datetime.utcnow() + timedelta(minutes=15)
        
        to_encode.update({"exp": expire})
        encoded_jwt = jwt.encode(to_encode, self.secret_key, algorithm=self.algorithm)
        return encoded_jwt
    
    def verify_token(self, token: str):
        """Verify JWT token"""
        try:
            payload = jwt.decode(token, self.secret_key, algorithms=[self.algorithm])
            return payload
        except jwt.ExpiredSignatureError:
            raise HTTPException(status_code=401, detail="Token expired")
        except jwt.JWTError:
            raise HTTPException(status_code=401, detail="Invalid token")
    
    def check_permissions(self, user: dict, required_permissions: list):
        """Check if user has required permissions"""
        user_permissions = user.get("permissions", [])
        if not all(perm in user_permissions for perm in required_permissions):
            raise HTTPException(status_code=403, detail="Insufficient permissions")

# Dependency for authentication
def get_current_user(credentials: HTTPAuthorizationCredentials = Depends(security)):
    """Get current authenticated user"""
    ac = AccessControl()
    payload = ac.verify_token(credentials.credentials)
    return payload

def require_permissions(required_permissions: list):
    """Dependency for permission checking"""
    def permission_checker(user: dict = Depends(get_current_user)):
        ac = AccessControl()
        ac.check_permissions(user, required_permissions)
        return user
    return permission_checker

# Usage in FastAPI
from access_control import get_current_user, require_permissions

app = FastAPI()

@app.post("/predict")
async def predict(
    request: dict,
    user: dict = Depends(get_current_user),
    permissions = Depends(require_permissions(["predict"]))
):
    """Protected prediction endpoint"""
    # Log access for audit
    print(f"User {user['sub']} accessed prediction endpoint")
    
    # Implement prediction logic
    return {"prediction": 1, "user": user["sub"]}

@app.post("/admin/retrain")
async def retrain_model(
    user: dict = Depends(require_permissions(["admin", "retrain"]))
):
    """Admin-only endpoint for model retraining"""
    # Only users with admin and retrain permissions can access
    return {"message": "Model retraining initiated"}
```

#### Compliance Automation

**GDPR Compliance Helper:**
```python
# gdpr_compliance.py
from datetime import datetime, timedelta
import json
import os

class GDPRCompliance:
    def __init__(self):
        self.retention_period = timedelta(days=2555)  # 7 years for financial data
        self.consent_log = []
    
    def log_consent(self, user_id: str, consent_type: str, consented: bool):
        """Log user consent for data processing"""
        consent_record = {
            "user_id": user_id,
            "consent_type": consent_type,
            "consented": consented,
            "timestamp": datetime.utcnow().isoformat(),
            "ip_address": "logged_ip",  # Would get from request
            "user_agent": "logged_agent"  # Would get from request
        }
        
        self.consent_log.append(consent_record)
        
        # Save to file/database
        self._save_consent_log()
    
    def check_consent(self, user_id: str, consent_type: str) -> bool:
        """Check if user has given consent"""
        user_consents = [c for c in self.consent_log if c["user_id"] == user_id]
        
        # Get latest consent for this type
        relevant_consents = [c for c in user_consents if c["consent_type"] == consent_type]
        if not relevant_consents:
            return False
        
        latest_consent = max(relevant_consents, key=lambda x: x["timestamp"])
        return latest_consent["consented"]
    
    def handle_data_deletion_request(self, user_id: str):
        """Handle GDPR right to erasure"""
        # Log deletion request
        deletion_log = {
            "user_id": user_id,
            "request_type": "data_deletion",
            "timestamp": datetime.utcnow().isoformat(),
            "status": "initiated"
        }
        
        # In practice, this would:
        # 1. Mark data for deletion
        # 2. Schedule actual deletion
        # 3. Notify user
        # 4. Log the action
        
        print(f"Data deletion initiated for user {user_id}")
        return {"message": "Data deletion request processed", "request_id": "del-123"}
    
    def anonymize_data(self, data):
        """Anonymize personal data"""
        # Remove or hash personal identifiers
        anonymized = data.copy()
        
        # Remove direct identifiers
        direct_identifiers = ['name', 'email', 'phone', 'address']
        for field in direct_identifiers:
            if field in anonymized:
                anonymized[field] = self._hash_value(str(anonymized[field]))
        
        # Generalize quasi-identifiers
        if 'age' in anonymized:
            anonymized['age'] = self._generalize_age(anonymized['age'])
        
        if 'zipcode' in anonymized:
            anonymized['zipcode'] = anonymized['zipcode'][:3] + '**'
        
        return anonymized
    
    def _hash_value(self, value: str) -> str:
        """Hash sensitive values"""
        import hashlib
        return hashlib.sha256(value.encode()).hexdigest()
    
    def _generalize_age(self, age: int) -> str:
        """Generalize age for privacy"""
        if age < 18:
            return "<18"
        elif age < 30:
            return "18-29"
        elif age < 50:
            return "30-49"
        elif age < 70:
            return "50-69"
        else:
            return "70+"
    
    def _save_consent_log(self):
        """Save consent log to persistent storage"""
        with open("consent_log.json", "w") as f:
            json.dump(self.consent_log, f, indent=2)

# Usage
gdpr = GDPRCompliance()

# Log consent
gdpr.log_consent("user123", "marketing", True)
gdpr.log_consent("user123", "analytics", False)

# Check consent
can_use_for_marketing = gdpr.check_consent("user123", "marketing")
print(f"Can use for marketing: {can_use_for_marketing}")

# Handle deletion request
gdpr.handle_data_deletion_request("user123")
```

This comprehensive security and compliance framework ensures that ML systems are protected against various threats while maintaining regulatory compliance. The layered approach covers container security, infrastructure protection, data encryption, access controls, and automated compliance measures.

## 8. Optimization and Maintenance

### 8.1 Performance Optimization

#### What is Performance Optimization in MLOps?

**Performance Optimization** refers to the systematic process of improving the efficiency, speed, and resource utilization of ML systems in production environments. It encompasses code optimization, infrastructure tuning, model optimization, and operational efficiency improvements.

**Key Performance Metrics**:
- **Latency**: Time taken to process a single request
- **Throughput**: Number of requests processed per unit time
- **Resource Utilization**: CPU, memory, and storage efficiency
- **Cost Efficiency**: Performance per dollar spent
- **Scalability**: Ability to handle increased load
- **Reliability**: System availability and error rates

**Why Performance Optimization Matters**:
- **User Experience**: Faster response times improve user satisfaction
- **Cost Reduction**: Efficient resource usage reduces infrastructure costs
- **Scalability**: Optimized systems can handle more load with fewer resources
- **Competitive Advantage**: Better performance differentiates services
- **Sustainability**: Reduced resource consumption lowers environmental impact

#### Container Resource Tuning

**Kubernetes Resource Management:**
```yaml
# optimized-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api-optimized
  namespace: ml-production
  labels:
    app: ml-api
    version: v1.0.0
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  selector:
    matchLabels:
      app: ml-api
  template:
    metadata:
      labels:
        app: ml-api
        version: v1.0.0
    spec:
      # Node affinity for GPU workloads
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: accelerator
                operator: In
                values:
                - nvidia-tesla-k80
      containers:
      - name: ml-api
        image: your-registry/ml-api:v1.0.0
        imagePullPolicy: Always
        ports:
        - containerPort: 8000
          name: http
          protocol: TCP
        resources:
          requests:
            memory: "512Mi"
            cpu: "500m"
            nvidia.com/gpu: "1"  # GPU request
          limits:
            memory: "2Gi"
            cpu: "2000m"
            nvidia.com/gpu: "1"  # GPU limit
        env:
        - name: GUNICORN_WORKERS
          valueFrom:
            configMapKeyRef:
              name: ml-config
              key: gunicorn-workers
        - name: MODEL_CACHE_SIZE
          value: "100MB"
        - name: CUDA_VISIBLE_DEVICES
          value: "0"
        # Readiness probe
        readinessProbe:
          httpGet:
            path: /health/ready
            port: 8000
          initialDelaySeconds: 10
          periodSeconds: 5
          timeoutSeconds: 3
          successThreshold: 1
          failureThreshold: 3
        # Liveness probe
        livenessProbe:
          httpGet:
            path: /health/live
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
          timeoutSeconds: 5
          successThreshold: 1
          failureThreshold: 3
        # Startup probe for slow-starting containers
        startupProbe:
          httpGet:
            path: /health/startup
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 10
          timeoutSeconds: 5
          successThreshold: 1
          failureThreshold: 30
        # Volume mounts for model caching
        volumeMounts:
        - name: model-cache
          mountPath: /app/models/cache
        - name: tmp-volume
          mountPath: /tmp
      volumes:
      - name: model-cache
        persistentVolumeClaim:
          claimName: model-cache-pvc
      - name: tmp-volume
        emptyDir: {}
      # Security context
      securityContext:
        runAsUser: 1000
        runAsGroup: 1000
        fsGroup: 1000
        runAsNonRoot: true
```

**Horizontal Pod Autoscaling (HPA):**
```yaml
# hpa.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: ml-api-hpa
  namespace: ml-production
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: ml-api-optimized
  minReplicas: 2
  maxReplicas: 20
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  - type: Pods
    pods:
      metric:
        name: http_requests_per_second
      target:
        type: AverageValue
        averageValue: 100
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
      - type: Pods
        value: 2
        periodSeconds: 60
      selectPolicy: Min
    scaleUp:
      stabilizationWindowSeconds: 60
      policies:
      - type: Percent
        value: 100
        periodSeconds: 60
      - type: Pods
        value: 4
        periodSeconds: 60
      selectPolicy: Max
```

**Gunicorn Configuration for ML APIs:**
```python
# gunicorn.conf.py
import multiprocessing
import os

# Server socket
bind = "0.0.0.0:8000"
backlog = 2048

# Worker processes - optimized for ML workloads
workers = min(multiprocessing.cpu_count() * 2 + 1, 12)  # Cap at 12 workers
worker_class = "uvicorn.workers.UvicornWorker"
worker_connections = 1000
max_requests = 1000  # Restart worker after this many requests
max_requests_jitter = 50  # Add randomness to prevent thundering herd

# Timeout settings
timeout = 30
keepalive = 2
graceful_timeout = 30

# Logging
loglevel = os.getenv("LOG_LEVEL", "info")
accesslog = "-"
errorlog = "-"
access_log_format = '%(h)s %(l)s %(u)s %(t)s "%(r)s" %(s)s %(b)s "%(f)s" "%(a)s" %(D)s'

# Process naming
proc_name = "ml-api"

# Server mechanics
preload_app = True  # Load app before forking workers
pidfile = "/tmp/gunicorn.pid"
user = os.getenv("APP_USER", "mluser")
group = os.getenv("APP_GROUP", "mluser")
tmp_upload_dir = None  # Disable file uploads to disk

# SSL/TLS (if needed)
# keyfile = "/path/to/ssl/private.key"
# certfile = "/path/to/ssl/certificate.crt"

# Worker temporary directory
worker_tmp_dir = "/tmp"

def on_starting(server):
    """Called just before the master process is initialized"""
    print("Starting Gunicorn server...")

def on_reload(server):
    """Called when server is reloaded"""
    print("Reloading Gunicorn server...")

def worker_abort(worker):
    """Called when a worker is aborted"""
    worker.log.warning("Worker %s aborted", worker.pid)

def worker_int(worker):
    """Called when a worker receives INT signal"""
    worker.log.info("Worker %s received INT signal", worker.pid)
```

#### Model Optimization Techniques

**Model Quantization:**
```python
# model_quantization.py
import torch
import torch.nn as nn
from torch.quantization import QuantStub, DeQuantStub
import torch.quantization as quant
import logging

logger = logging.getLogger(__name__)

class QuantizedModel(nn.Module):
    """Quantization-ready model wrapper"""

    def __init__(self, model):
        super().__init__()
        self.model = model
        self.quant = QuantStub()
        self.dequant = DeQuantStub()

    def forward(self, x):
        x = self.quant(x)
        x = self.model(x)
        x = self.dequant(x)
        return x

class ModelOptimizer:
    """Optimize ML models for production deployment"""

    def __init__(self, model_path: str):
        self.model_path = model_path
        self.model = None

    def load_model(self):
        """Load model from disk"""
        self.model = torch.load(self.model_path)
        logger.info(f"Loaded model from {self.model_path}")
        return self.model

    def quantize_model(self, model, backend='fbgemm'):
        """Quantize model for reduced memory and faster inference"""

        # Prepare model for quantization
        quantized_model = QuantizedModel(model)

        # Set quantization configuration
        quantized_model.qconfig = quant.get_default_qconfig(backend)

        # Prepare for quantization
        quant.prepare(quantized_model, inplace=True)

        # Calibrate with sample data (you would use your actual calibration data)
        # quantized_model.eval()
        # with torch.no_grad():
        #     for data in calibration_loader:
        #         quantized_model(data)

        # Convert to quantized model
        quant.convert(quantized_model, inplace=True)

        logger.info("Model quantized successfully")
        return quantized_model

    def optimize_for_cpu(self, model):
        """Optimize model for CPU inference"""
        model.eval()

        # Use TorchScript for optimized execution
        with torch.no_grad():
            example_input = torch.randn(1, 3, 224, 224)  # Adjust based on your input shape
            scripted_model = torch.jit.trace(model, example_input)

        # Optimize for mobile/cpu
        optimized_model = torch.jit.optimize_for_inference(scripted_model)

        logger.info("Model optimized for CPU inference")
        return optimized_model

    def compress_model(self, model, compression_ratio=0.5):
        """Compress model using pruning"""

        # Implement model pruning
        parameters_to_prune = []
        for module_name, module in model.named_modules():
            if isinstance(module, torch.nn.Conv2d):
                parameters_to_prune.append((module, 'weight'))
            elif isinstance(module, torch.nn.Linear):
                parameters_to_prune.append((module, 'weight'))

        # Prune parameters
        import torch.nn.utils.prune as prune
        for module, param_name in parameters_to_prune:
            prune.l1_unstructured(module, param_name, amount=compression_ratio)

        # Remove pruning reparameterization
        for module, param_name in parameters_to_prune:
            prune.remove(module, param_name)

        logger.info(f"Model compressed with ratio {compression_ratio}")
        return model

    def benchmark_model(self, model, input_shape=(1, 3, 224, 224), num_runs=100):
        """Benchmark model performance"""

        model.eval()
        device = next(model.parameters()).device

        # Warmup
        with torch.no_grad():
            for _ in range(10):
                input_tensor = torch.randn(input_shape).to(device)
                _ = model(input_tensor)

        # Benchmark
        import time
        start_time = time.time()

        with torch.no_grad():
            for _ in range(num_runs):
                input_tensor = torch.randn(input_shape).to(device)
                _ = model(input_tensor)

        end_time = time.time()
        total_time = end_time - start_time
        avg_latency = total_time / num_runs * 1000  # ms

        # Memory usage
        memory_usage = torch.cuda.memory_allocated() if torch.cuda.is_available() else 0

        results = {
            'avg_latency_ms': avg_latency,
            'throughput': num_runs / total_time,
            'memory_usage_mb': memory_usage / 1024 / 1024 if memory_usage > 0 else 0,
            'device': str(device)
        }

        logger.info(f"Benchmark results: {results}")
        return results

    def save_optimized_model(self, model, output_path: str):
        """Save optimized model"""
        torch.save(model, output_path)
        logger.info(f"Optimized model saved to {output_path}")

# Usage example
def optimize_ml_model():
    """Complete model optimization pipeline"""

    optimizer = ModelOptimizer("models/churn_model.pth")

    # Load model
    model = optimizer.load_model()

    # Benchmark original model
    original_benchmark = optimizer.benchmark_model(model)

    # Quantize model
    quantized_model = optimizer.quantize_model(model)

    # Optimize for CPU
    optimized_model = optimizer.optimize_for_cpu(quantized_model)

    # Compress model
    compressed_model = optimizer.compress_model(optimized_model, compression_ratio=0.3)

    # Benchmark optimized model
    optimized_benchmark = optimizer.benchmark_model(compressed_model)

    # Save optimized model
    optimizer.save_optimized_model(compressed_model, "models/churn_model_optimized.pth")

    print(f"Original latency: {original_benchmark['avg_latency_ms']:.2f}ms")
    print(f"Optimized latency: {optimized_benchmark['avg_latency_ms']:.2f}ms")
    print(f"Improvement: {(original_benchmark['avg_latency_ms'] - optimized_benchmark['avg_latency_ms']) / original_benchmark['avg_latency_ms'] * 100:.1f}%")

    return compressed_model
```

#### Caching Strategies

**Multi-Level Caching:**
```python
# caching.py
import redis
import pickle
from typing import Any, Optional, Dict
import hashlib
import json
import logging
from functools import wraps
import time

logger = logging.getLogger(__name__)

class MultiLevelCache:
    """Multi-level caching system for ML applications"""

    def __init__(self, redis_host: str = "localhost", redis_port: int = 6379):
        self.redis_client = redis.Redis(host=redis_host, port=redis_port, decode_responses=False)
        self.local_cache: Dict[str, Dict] = {}
        self.cache_stats = {
            'hits': 0,
            'misses': 0,
            'local_hits': 0,
            'redis_hits': 0
        }

    def _generate_key(self, func_name: str, args: tuple, kwargs: dict) -> str:
        """Generate cache key from function call"""
        key_data = {
            'func': func_name,
            'args': str(args),
            'kwargs': str(sorted(kwargs.items()))
        }
        key_string = json.dumps(key_data, sort_keys=True)
        return hashlib.md5(key_string.encode()).hexdigest()

    def get(self, key: str) -> Optional[Any]:
        """Get value from cache"""
        # Check local cache first
        if key in self.local_cache:
            cache_entry = self.local_cache[key]
            if time.time() < cache_entry['expires']:
                self.cache_stats['hits'] += 1
                self.cache_stats['local_hits'] += 1
                return cache_entry['value']
            else:
                # Remove expired entry
                del self.local_cache[key]

        # Check Redis
        try:
            cached_data = self.redis_client.get(key)
            if cached_data:
                value = pickle.loads(cached_data)
                # Update local cache
                self.local_cache[key] = {
                    'value': value,
                    'expires': time.time() + 300  # 5 minutes local TTL
                }
                self.cache_stats['hits'] += 1
                self.cache_stats['redis_hits'] += 1
                return value
        except Exception as e:
            logger.warning(f"Redis cache error: {e}")

        self.cache_stats['misses'] += 1
        return None

    def set(self, key: str, value: Any, ttl_seconds: int = 3600):
        """Set value in cache"""
        try:
            # Store in Redis
            serialized_value = pickle.dumps(value)
            self.redis_client.setex(key, ttl_seconds, serialized_value)

            # Store in local cache
            self.local_cache[key] = {
                'value': value,
                'expires': time.time() + min(ttl_seconds, 300)  # Max 5 minutes local
            }
        except Exception as e:
            logger.error(f"Cache set error: {e}")

    def invalidate_pattern(self, pattern: str):
        """Invalidate cache keys matching pattern"""
        try:
            keys = self.redis_client.keys(pattern)
            if keys:
                self.redis_client.delete(*keys)
                # Remove from local cache
                for key in list(self.local_cache.keys()):
                    if pattern.replace('*', '') in key:
                        del self.local_cache[key]
        except Exception as e:
            logger.error(f"Cache invalidation error: {e}")

    def get_stats(self) -> Dict:
        """Get cache statistics"""
        total_requests = self.cache_stats['hits'] + self.cache_stats['misses']
        hit_rate = self.cache_stats['hits'] / total_requests if total_requests > 0 else 0

        return {
            **self.cache_stats,
            'hit_rate': hit_rate,
            'total_requests': total_requests
        }

# Global cache instance
cache = MultiLevelCache()

def cached(ttl_seconds: int = 3600, key_prefix: str = ""):
    """Decorator for caching function results"""
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            cache_key = f"{key_prefix}:{cache._generate_key(func.__name__, args, kwargs)}"

            # Try to get from cache
            cached_result = cache.get(cache_key)
            if cached_result is not None:
                return cached_result

            # Execute function
            result = func(*args, **kwargs)

            # Cache result
            cache.set(cache_key, result, ttl_seconds)

            return result
        return wrapper
    return decorator

class ModelCache:
    """Specialized cache for ML models and predictions"""

    def __init__(self):
        self.cache = MultiLevelCache()

    @cached(ttl_seconds=3600, key_prefix="prediction")
    def get_prediction(self, model_name: str, features: list) -> dict:
        """Cache prediction results"""
        # This would normally call your ML model
        # For demo, return mock prediction
        import random
        return {
            'prediction': random.random(),
            'confidence': random.uniform(0.7, 0.95),
            'model_version': 'v1.0.0'
        }

    def cache_model(self, model_name: str, model_object, ttl_seconds: int = 86400):
        """Cache loaded model object"""
        cache_key = f"model:{model_name}"
        self.cache.set(cache_key, model_object, ttl_seconds)

    def get_model(self, model_name: str):
        """Get cached model object"""
        cache_key = f"model:{model_name}"
        return self.cache.get(cache_key)

    def invalidate_model_cache(self, model_name: str):
        """Invalidate model cache"""
        self.cache.invalidate_pattern(f"model:{model_name}*")

    def warmup_cache(self, model_name: str, sample_features: list):
        """Warm up cache with sample predictions"""
        logger.info(f"Warming up cache for model {model_name}")

        # Generate sample predictions to populate cache
        for i in range(10):
            sample_features_varied = [f + i * 0.1 for f in sample_features]
            self.get_prediction(model_name, sample_features_varied)

        logger.info("Cache warmup completed")

# Global model cache instance
model_cache = ModelCache()
```

### 8.2 Maintenance Automation

#### Automated Maintenance Tasks

**Scheduled Maintenance Scripts:**
```python
# maintenance.py
import schedule
import time
import logging
from datetime import datetime, timedelta
import subprocess
import os
from typing import List, Dict, Callable

logger = logging.getLogger(__name__)

class MaintenanceScheduler:
    """Automated maintenance task scheduler"""

    def __init__(self):
        self.tasks = []
        self.maintenance_window = {
            'start_hour': 2,  # 2 AM
            'end_hour': 4,    # 4 AM
            'timezone': 'UTC'
        }

    def add_task(self, name: str, task_func: Callable, schedule_time: str,
                 maintenance_only: bool = False):
        """Add maintenance task"""
        self.tasks.append({
            'name': name,
            'function': task_func,
            'schedule': schedule_time,
            'maintenance_only': maintenance_only,
            'last_run': None,
            'status': 'scheduled'
        })

    def is_maintenance_window(self) -> bool:
        """Check if current time is within maintenance window"""
        now = datetime.utcnow()
        return self.maintenance_window['start_hour'] <= now.hour < self.maintenance_window['end_hour']

    def run_task(self, task: Dict):
        """Execute a maintenance task"""
        try:
            logger.info(f"Starting maintenance task: {task['name']}")

            # Check maintenance window for critical tasks
            if task['maintenance_only'] and not self.is_maintenance_window():
                logger.info(f"Skipping {task['name']} - outside maintenance window")
                return

            # Execute task
            result = task['function']()

            # Update task status
            task['last_run'] = datetime.utcnow()
            task['status'] = 'completed'
            task['last_result'] = result

            logger.info(f"Completed maintenance task: {task['name']}")

        except Exception as e:
            logger.error(f"Failed maintenance task {task['name']}: {e}")
            task['status'] = 'failed'
            task['error'] = str(e)

    def run_all_tasks(self):
        """Run all scheduled tasks"""
        logger.info("Running scheduled maintenance tasks...")

        for task in self.tasks:
            if task['status'] != 'running':  # Prevent concurrent execution
                task['status'] = 'running'
                self.run_task(task)

    def get_task_status(self) -> List[Dict]:
        """Get status of all maintenance tasks"""
        return [{
            'name': task['name'],
            'status': task['status'],
            'last_run': task['last_run'].isoformat() if task['last_run'] else None,
            'schedule': task['schedule'],
            'maintenance_only': task['maintenance_only']
        } for task in self.tasks]

def cleanup_old_logs():
    """Clean up old log files"""
    log_dir = "/var/log/ml-api"
    retention_days = 30

    if not os.path.exists(log_dir):
        return {"status": "skipped", "reason": "Log directory not found"}

    deleted_files = []
    cutoff_date = datetime.now() - timedelta(days=retention_days)

    for filename in os.listdir(log_dir):
        if filename.endswith('.log'):
            filepath = os.path.join(log_dir, filename)
            file_modified = datetime.fromtimestamp(os.path.getmtime(filepath))

            if file_modified < cutoff_date:
                os.remove(filepath)
                deleted_files.append(filename)

    return {
        "status": "completed",
        "deleted_files": len(deleted_files),
        "files": deleted_files
    }

def update_model_cache():
    """Update model cache and clear expired entries"""
    try:
        # Clear Redis expired keys (Redis does this automatically)
        # But we can add custom cleanup logic

        # Update model versions if needed
        # This would check for new model versions and update cache

        return {"status": "completed", "message": "Model cache updated"}
    except Exception as e:
        return {"status": "failed", "error": str(e)}

def backup_database():
    """Backup database during maintenance window"""
    try:
        # PostgreSQL backup
        backup_cmd = [
            "pg_dump",
            "-h", os.getenv("DB_HOST", "localhost"),
            "-U", os.getenv("DB_USER", "mluser"),
            "-d", os.getenv("DB_NAME", "ml_database"),
            "-f", f"/backups/ml_db_{datetime.now().strftime('%Y%m%d_%H%M%S')}.sql"
        ]

        result = subprocess.run(backup_cmd, capture_output=True, text=True)

        if result.returncode == 0:
            return {"status": "completed", "backup_file": backup_cmd[-1]}
        else:
            return {"status": "failed", "error": result.stderr}

    except Exception as e:
        return {"status": "failed", "error": str(e)}

def optimize_database():
    """Optimize database performance"""
    try:
        # PostgreSQL optimization
        optimize_cmd = [
            "psql",
            "-h", os.getenv("DB_HOST", "localhost"),
            "-U", os.getenv("DB_USER", "mluser"),
            "-d", os.getenv("DB_NAME", "ml_database"),
            "-c", "VACUUM ANALYZE;"
        ]

        result = subprocess.run(optimize_cmd, capture_output=True, text=True)

        if result.returncode == 0:
            return {"status": "completed", "message": "Database optimized"}
        else:
            return {"status": "failed", "error": result.stderr}

    except Exception as e:
        return {"status": "failed", "error": str(e)}

def health_check():
    """Perform comprehensive health check"""
    health_status = {
        "status": "healthy",
        "checks": {}
    }

    # Check database connectivity
    try:
        # Database health check logic
        health_status["checks"]["database"] = "healthy"
    except Exception as e:
        health_status["checks"]["database"] = f"unhealthy: {e}"
        health_status["status"] = "unhealthy"

    # Check model loading
    try:
        # Model health check logic
        health_status["checks"]["models"] = "healthy"
    except Exception as e:
        health_status["checks"]["models"] = f"unhealthy: {e}"
        health_status["status"] = "unhealthy"

    # Check external dependencies
    try:
        # External service health checks
        health_status["checks"]["external_services"] = "healthy"
    except Exception as e:
        health_status["checks"]["external_services"] = f"unhealthy: {e}"
        health_status["status"] = "unhealthy"

    return health_status

# Setup maintenance scheduler
maintenance_scheduler = MaintenanceScheduler()

# Add maintenance tasks
maintenance_scheduler.add_task(
    "log_cleanup", cleanup_old_logs, "daily", maintenance_only=True
)
maintenance_scheduler.add_task(
    "cache_update", update_model_cache, "hourly"
)
maintenance_scheduler.add_task(
    "database_backup", backup_database, "daily", maintenance_only=True
)
maintenance_scheduler.add_task(
    "database_optimize", optimize_database, "weekly", maintenance_only=True
)
maintenance_scheduler.add_task(
    "health_check", health_check, "every 10 minutes"
)

# Schedule tasks
schedule.every().day.at("02:00").do(lambda: maintenance_scheduler.run_task(
    next(task for task in maintenance_scheduler.tasks if task['name'] == 'log_cleanup')
))
schedule.every().hour.do(lambda: maintenance_scheduler.run_task(
    next(task for task in maintenance_scheduler.tasks if task['name'] == 'cache_update')
))
schedule.every().day.at("03:00").do(lambda: maintenance_scheduler.run_task(
    next(task for task in maintenance_scheduler.tasks if task['name'] == 'database_backup')
))
schedule.every().week.do(lambda: maintenance_scheduler.run_task(
    next(task for task in maintenance_scheduler.tasks if task['name'] == 'database_optimize')
))
schedule.every(10).minutes.do(lambda: maintenance_scheduler.run_task(
    next(task for task in maintenance_scheduler.tasks if task['name'] == 'health_check')
))

def run_maintenance():
    """Run maintenance scheduler"""
    logger.info("Starting maintenance scheduler...")

    while True:
        schedule.run_pending()
        time.sleep(60)

if __name__ == "__main__":
    run_maintenance()
```

This comprehensive optimization and maintenance section provides the foundation for maintaining high-performance, reliable ML systems in production environments.
group = "mluser"
tmp_upload_dir = None

# SSL (if needed)
# keyfile = "/path/to/ssl/private.key"
# certfile = "/path/to/ssl/certificate.crt"
```

#### Model Inference Optimization

**ONNX Runtime Optimization:**
```python
# onnx_optimization.py
import onnxruntime as ort
import numpy as np
from sklearn.ensemble import RandomForestClassifier
import onnx
from skl2onnx import convert_sklearn
from onnxmltools import convert_sklearn as convert_sklearn_onnx
from onnxruntime.transformers import optimizer
import time

class OptimizedInference:
    def __init__(self, model_path: str = None, sklearn_model=None):
        self.model_path = model_path
        self.sklearn_model = sklearn_model
        
        if model_path:
            # Load optimized ONNX model
            self.session = ort.InferenceSession(
                model_path,
                providers=['CUDAExecutionProvider', 'CPUExecutionProvider']
            )
        else:
            # Convert sklearn model to ONNX
            self._convert_to_onnx()
    
    def _convert_to_onnx(self):
        """Convert sklearn model to ONNX with optimizations"""
        # Convert to ONNX
        initial_type = [('float_input', 'float32', (None, self.sklearn_model.n_features_))]
        onnx_model = convert_sklearn_onnx(self.sklearn_model, initial_types=initial_type)
        
        # Optimize ONNX model
        optimized_model = optimizer.optimize_model(
            onnx_model,
            model_type='bert',  # Use appropriate model type
            num_heads=0,  # For non-transformer models
            hidden_size=0
        )
        
        # Save optimized model
        onnx.save(optimized_model, 'optimized_model.onnx')
        
        # Create session
        self.session = ort.InferenceSession(
            'optimized_model.onnx',
            providers=['CUDAExecutionProvider', 'CPUExecutionProvider']
        )
    
    def predict(self, X: np.ndarray) -> np.ndarray:
        """Optimized prediction"""
        # Ensure input is float32
        X = X.astype(np.float32)
        
        # Get input name
        input_name = self.session.get_inputs()[0].name
        
        # Run inference
        outputs = self.session.run(None, {input_name: X})
        
        return outputs[0]
    
    def predict_proba(self, X: np.ndarray) -> np.ndarray:
        """Optimized probability prediction"""
        X = X.astype(np.float32)
        input_name = self.session.get_inputs()[0].name
        
        # Run inference
        outputs = self.session.run(None, {input_name: X})
        
        # Apply softmax if needed
        if len(outputs) > 1:
            return self._softmax(outputs)
        else:
            # Binary classification
            probs = outputs[0]
            return np.column_stack([1 - probs, probs])
    
    def _softmax(self, x):
        """Compute softmax"""
        e_x = np.exp(x - np.max(x, axis=1, keepdims=True))
        return e_x / e_x.sum(axis=1, keepdims=True)
    
    def benchmark_inference(self, X: np.ndarray, n_runs: int = 100):
        """Benchmark inference performance"""
        times = []
        
        for _ in range(n_runs):
            start = time.time()
            _ = self.predict(X)
            times.append(time.time() - start)
        
        avg_time = np.mean(times)
        p95_time = np.percentile(times, 95)
        throughput = len(X) / avg_time
        
        print(f"Average inference time: {avg_time:.4f}s")
        print(f"95th percentile time: {p95_time:.4f}s")
        print(f"Throughput: {throughput:.2f} predictions/second")
        
        return {
            'avg_time': avg_time,
            'p95_time': p95_time,
            'throughput': throughput
        }

# Usage
# Convert sklearn model
sklearn_model = RandomForestClassifier(n_estimators=100)
# Assume model is trained...

# Create optimized inference
optimizer = OptimizedInference(sklearn_model=sklearn_model)

# Benchmark
X_test = np.random.randn(1000, 20)  # 1000 samples, 20 features
results = optimizer.benchmark_inference(X_test)
```

**TensorRT Optimization for GPU Inference:**
```python
# tensorrt_optimization.py
import tensorrt as trt
import pycuda.driver as cuda
import pycuda.autoinit
import numpy as np
import time

class TensorRTOptimizer:
    def __init__(self, onnx_path: str):
        self.onnx_path = onnx_path
        self.engine = None
        self.context = None
        
        # Initialize TensorRT
        self.logger = trt.Logger(trt.Logger.WARNING)
        self._build_engine()
    
    def _build_engine(self):
        """Build TensorRT engine from ONNX model"""
        with trt.Builder(self.logger) as builder, \
             builder.create_network(1 << int(trt.NetworkDefinitionCreationFlag.EXPLICIT_BATCH)) as network, \
             trt.OnnxParser(network, self.logger) as parser:
            
            # Parse ONNX model
            with open(self.onnx_path, 'rb') as model:
                if not parser.parse(model.read()):
                    for error in range(parser.num_errors):
                        print(parser.get_error(error))
                    raise ValueError("Failed to parse ONNX model")
            
            # Create builder config
            config = builder.create_builder_config()
            config.max_workspace_size = 1 << 30  # 1GB
            
            # Enable FP16 if supported
            if builder.platform_has_fast_fp16:
                config.set_flag(trt.BuilderFlag.FP16)
            
            # Build engine
            self.engine = builder.build_engine(network, config)
            
            # Create execution context
            self.context = self.engine.create_execution_context()
    
    def predict(self, input_data: np.ndarray) -> np.ndarray:
        """Run inference with TensorRT"""
        # Allocate device memory
        input_shape = input_data.shape
        output_shape = (input_shape[0], self.engine.get_binding_shape(1)[1])
        
        # Allocate host and device buffers
        d_input = cuda.mem_alloc(input_data.nbytes)
        d_output = cuda.mem_alloc(output_shape[0] * output_shape[1] * 4)  # float32
        
        # Create stream
        stream = cuda.Stream()
        
        # Transfer input data to device
        cuda.memcpy_htod_async(d_input, input_data, stream)
        
        # Run inference
        self.context.execute_async_v2(
            bindings=[int(d_input), int(d_output)],
            stream_handle=stream.handle
        )
        
        # Transfer predictions back
        output = np.empty(output_shape, dtype=np.float32)
        cuda.memcpy_dtoh_async(output, d_output, stream)
        
        # Synchronize
        stream.synchronize()
        
        return output
    
    def benchmark(self, input_data: np.ndarray, n_runs: int = 100):
        """Benchmark TensorRT performance"""
        times = []
        
        # Warm up
        for _ in range(10):
            _ = self.predict(input_data)
        
        for _ in range(n_runs):
            start = time.time()
            _ = self.predict(input_data)
            times.append(time.time() - start)
        
        avg_time = np.mean(times)
        p95_time = np.percentile(times, 95)
        throughput = len(input_data) / avg_time
        
        print(f"TensorRT - Average inference time: {avg_time:.4f}s")
        print(f"TensorRT - 95th percentile time: {p95_time:.4f}s")
        print(f"TensorRT - Throughput: {throughput:.2f} predictions/second")
        
        return {
            'avg_time': avg_time,
            'p95_time': p95_time,
            'throughput': throughput
        }

# Usage
# trt_optimizer = TensorRTOptimizer("model.onnx")
# results = trt_optimizer.benchmark(X_test)
```

#### Database Query Optimization

**Connection Pooling and Query Optimization:**
```python
# database_optimization.py
from sqlalchemy import create_engine, text
from sqlalchemy.pool import QueuePool
from sqlalchemy.orm import sessionmaker, scoped_session
import time
import psycopg2.pool

class DatabaseOptimizer:
    def __init__(self, db_url: str):
        # SQLAlchemy engine with optimized settings
        self.engine = create_engine(
            db_url,
            poolclass=QueuePool,
            pool_size=10,
            max_overflow=20,
            pool_timeout=30,
            pool_recycle=3600,
            echo=False
        )
        
        # Create session factory
        self.Session = scoped_session(sessionmaker(bind=self.engine))
        
        # Psycopg2 connection pool for raw queries
        self.psycopg_pool = psycopg2.pool.SimpleConnectionPool(
            minconn=5,
            maxconn=20,
            host="your-host",
            database="your-db",
            user="your-user",
            password="your-password"
        )
    
    def get_optimized_session(self):
        """Get optimized database session"""
        return self.Session()
    
    def execute_optimized_query(self, query: str, params: dict = None):
        """Execute query with optimizations"""
        with self.engine.connect() as conn:
            # Use server-side cursors for large result sets
            if "SELECT" in query.upper() and "LIMIT" not in query.upper():
                conn = conn.execution_options(stream_results=True)
            
            result = conn.execute(text(query), params or {})
            return result
    
    def batch_insert(self, table: str, data: list):
        """Optimized batch insert"""
        with self.engine.connect() as conn:
            # Use executemany for batch inserts
            if data:
                columns = list(data[0].keys())
                values = [tuple(row.values()) for row in data]
                
                placeholders = ','.join([':' + col for col in columns])
                query = f"INSERT INTO {table} ({','.join(columns)}) VALUES ({placeholders})"
                
                conn.execute(text(query), values)
                conn.commit()
    
    def create_indexes(self):
        """Create optimized indexes for ML workloads"""
        with self.engine.connect() as conn:
            # Index for time-series data
            conn.execute(text("""
                CREATE INDEX CONCURRENTLY IF NOT EXISTS idx_predictions_timestamp 
                ON predictions (created_at DESC);
            """))
            
            # Index for user-based queries
            conn.execute(text("""
                CREATE INDEX CONCURRENTLY IF NOT EXISTS idx_predictions_user_id 
                ON predictions (user_id, created_at DESC);
            """))
            
            # Partial index for recent data
            conn.execute(text("""
                CREATE INDEX CONCURRENTLY IF NOT EXISTS idx_recent_predictions 
                ON predictions (created_at DESC) 
                WHERE created_at > NOW() - INTERVAL '30 days';
            """))
            
            conn.commit()
    
    def optimize_table(self, table_name: str):
        """Run table optimization commands"""
        with self.engine.connect() as conn:
            # Vacuum analyze for PostgreSQL
            conn.execute(text(f"VACUUM ANALYZE {table_name};"))
            
            # Reindex if needed
            conn.execute(text(f"REINDEX TABLE CONCURRENTLY {table_name};"))
            
            conn.commit()
    
    def get_query_performance(self, query: str, params: dict = None):
        """Analyze query performance"""
        with self.engine.connect() as conn:
            # Enable timing
            conn.execute(text("SET timing = on;"))
            
            start_time = time.time()
            result = conn.execute(text(f"EXPLAIN ANALYZE {query}"), params or {})
            end_time = time.time()
            
            execution_time = end_time - start_time
            explain_plan = result.fetchall()
            
            return {
                'execution_time': execution_time,
                'explain_plan': [row[0] for row in explain_plan]
            }

# Usage
db_optimizer = DatabaseOptimizer("postgresql://user:pass@host:5432/db")

# Create optimized indexes
db_optimizer.create_indexes()

# Analyze query performance
performance = db_optimizer.get_query_performance("""
    SELECT user_id, AVG(prediction_score) as avg_score, COUNT(*) as prediction_count
    FROM predictions 
    WHERE created_at > NOW() - INTERVAL '7 days'
    GROUP BY user_id 
    ORDER BY avg_score DESC 
    LIMIT 100
""")

print(f"Query execution time: {performance['execution_time']:.4f}s")
```

### 8.2 Cost Optimization

Managing cloud costs for ML workloads requires intelligent resource allocation and monitoring.

#### Right-sizing Infrastructure

**Auto-scaling Configuration:**
```yaml
# auto-scaling.yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: ml-api-hpa
  namespace: ml-production
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: ml-api
  minReplicas: 2
  maxReplicas: 20
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80
  - type: Pods
    pods:
      metric:
        name: http_requests_per_second
      target:
        type: AverageValue
        averageValue: 100
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 300
      policies:
      - type: Percent
        value: 50
        periodSeconds: 60
      - type: Pods
        value: 2
        periodSeconds: 60
      selectPolicy: Min
    scaleUp:
      stabilizationWindowSeconds: 60
      policies:
      - type: Percent
        value: 100
        periodSeconds: 60
      - type: Pods
        value: 4
        periodSeconds: 60
      selectPolicy: Max

---
apiVersion: autoscaling/v2
kind: VerticalPodAutoscaler
metadata:
  name: ml-api-vpa
  namespace: ml-production
spec:
  targetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: ml-api
  updatePolicy:
    updateMode: "Auto"
  resourcePolicy:
    containerPolicies:
    - containerName: ml-api
      minAllowed:
        cpu: 100m
        memory: 256Mi
      maxAllowed:
        cpu: 2000m
        memory: 4Gi
```

**Spot Instance Configuration:**
```yaml
# spot-instance-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-training-spot
  namespace: ml-production
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ml-training
  template:
    metadata:
      labels:
        app: ml-training
    spec:
      affinity:
        nodeAffinity:
          preferredDuringSchedulingIgnoredDuringExecution:
          - weight: 100
            preference:
              matchExpressions:
              - key: instance-type
                operator: In
                values:
                - spot
                - preemptible
      tolerations:
      - key: spot-instance
        operator: Equal
        value: "true"
        effect: NoSchedule
      containers:
      - name: ml-training
        image: your-registry/ml-training:v1.0.0
        resources:
          requests:
            memory: "4Gi"
            cpu: "2"
          limits:
            memory: "8Gi"
            cpu: "4"
        env:
        - name: TRAINING_DATA_PATH
          value: "/data/training"
        volumeMounts:
        - name: training-data
          mountPath: /data
      volumes:
      - name: training-data
        persistentVolumeClaim:
          claimName: training-data-pvc
      restartPolicy: OnFailure
```

#### Cost Monitoring and Alerting

**Cloud Cost Monitoring:**
```python
# cost_monitoring.py
import boto3
from datetime import datetime, timedelta
import pandas as pd
import matplotlib.pyplot as plt
from prometheus_client import Gauge, push_to_gateway
import os

class CloudCostMonitor:
    def __init__(self, cloud_provider: str = "aws"):
        self.cloud_provider = cloud_provider
        
        if cloud_provider == "aws":
            self.client = boto3.client('ce', region_name='us-east-1')
        elif cloud_provider == "gcp":
            # GCP cost monitoring setup
            pass
        elif cloud_provider == "azure":
            # Azure cost monitoring setup
            pass
    
    def get_cost_data(self, days: int = 30):
        """Get cost data for the specified period"""
        end_date = datetime.now()
        start_date = end_date - timedelta(days=days)
        
        if self.cloud_provider == "aws":
            return self._get_aws_costs(start_date, end_date)
        elif self.cloud_provider == "gcp":
            return self._get_gcp_costs(start_date, end_date)
        else:
            return self._get_azure_costs(start_date, end_date)
    
    def _get_aws_costs(self, start_date, end_date):
        """Get AWS cost data"""
        response = self.client.get_cost_and_usage(
            TimePeriod={
                'Start': start_date.strftime('%Y-%m-%d'),
                'End': end_date.strftime('%Y-%m-%d')
            },
            Granularity='DAILY',
            Metrics=['BlendedCost'],
            GroupBy=[
                {
                    'Type': 'DIMENSION',
                    'Key': 'SERVICE'
                },
                {
                    'Type': 'DIMENSION',
                    'Key': 'AZ'
                }
            ]
        )
        
        costs = []
        for result in response['ResultsByTime']:
            date = result['TimePeriod']['Start']
            for group in result['Groups']:
                service = group['Keys'][0]
                az = group['Keys'][1]
                amount = float(group['Metrics']['BlendedCost']['Amount'])
                
                costs.append({
                    'date': date,
                    'service': service,
                    'availability_zone': az,
                    'cost': amount
                })
        
        return pd.DataFrame(costs)
    
    def analyze_cost_trends(self, cost_df):
        """Analyze cost trends and identify anomalies"""
        # Daily cost trend
        daily_costs = cost_df.groupby('date')['cost'].sum().reset_index()
        
        # Service-wise cost breakdown
        service_costs = cost_df.groupby('service')['cost'].sum().sort_values(ascending=False)
        
        # Cost by availability zone
        az_costs = cost_df.groupby('availability_zone')['cost'].sum()
        
        # Identify cost anomalies (simple threshold-based)
        mean_daily_cost = daily_costs['cost'].mean()
        std_daily_cost = daily_costs['cost'].std()
        threshold = mean_daily_cost + 2 * std_daily_cost
        
        anomalies = daily_costs[daily_costs['cost'] > threshold]
        
        return {
            'daily_trends': daily_costs,
            'service_breakdown': service_costs,
            'az_breakdown': az_costs,
            'anomalies': anomalies,
            'threshold': threshold
        }
    
    def create_cost_dashboard(self, cost_df):
        """Create cost visualization dashboard"""
        analysis = self.analyze_cost_trends(cost_df)
        
        # Create subplots
        fig, ((ax1, ax2), (ax3, ax4)) = plt.subplots(2, 2, figsize=(15, 10))
        
        # Daily cost trend
        ax1.plot(analysis['daily_trends']['date'], analysis['daily_trends']['cost'])
        ax1.set_title('Daily Cost Trend')
        ax1.set_xlabel('Date')
        ax1.set_ylabel('Cost ($)')
        ax1.tick_params(axis='x', rotation=45)
        
        # Service breakdown
        analysis['service_breakdown'].head(10).plot(kind='bar', ax=ax2)
        ax2.set_title('Top 10 Services by Cost')
        ax2.set_ylabel('Cost ($)')
        ax2.tick_params(axis='x', rotation=45)
        
        # Availability zone breakdown
        analysis['az_breakdown'].plot(kind='pie', ax=ax3, autopct='%1.1f%%')
        ax3.set_title('Cost by Availability Zone')
        
        # Anomalies
        ax4.bar(range(len(analysis['anomalies'])), analysis['anomalies']['cost'])
        ax4.set_title('Cost Anomalies')
        ax4.set_xlabel('Anomaly Index')
        ax4.set_ylabel('Cost ($)')
        
        plt.tight_layout()
        plt.savefig('cost_analysis_dashboard.png', dpi=300, bbox_inches='tight')
        
        return fig
    
    def export_cost_metrics(self, cost_df):
        """Export cost metrics to Prometheus"""
        analysis = self.analyze_cost_trends(cost_df)
        
        # Create Prometheus metrics
        total_cost = Gauge('cloud_total_cost', 'Total cloud cost')
        service_cost = Gauge('cloud_service_cost', 'Cost by service', ['service'])
        anomaly_count = Gauge('cloud_cost_anomalies', 'Number of cost anomalies')
        
        # Set metrics
        total_cost.set(cost_df['cost'].sum())
        
        for service, cost in analysis['service_breakdown'].items():
            service_cost.labels(service=service).set(cost)
        
        anomaly_count.set(len(analysis['anomalies']))
        
        # Push to Prometheus pushgateway
        pushgateway_url = os.getenv('PROMETHEUS_PUSHGATEWAY', 'localhost:9091')
        push_to_gateway(pushgateway_url, job='cost_monitoring', registry=None)
    
    def generate_cost_report(self, cost_df):
        """Generate detailed cost report"""
        analysis = self.analyze_cost_trends(cost_df)
        
        report = f"""
# Cloud Cost Report - {datetime.now().strftime('%Y-%m-%d')}

## Summary
- Total Cost: ${cost_df['cost'].sum():.2f}
- Average Daily Cost: ${analysis['daily_trends']['cost'].mean():.2f}
- Cost Anomalies Detected: {len(analysis['anomalies'])}

## Top Cost Services
{analysis['service_breakdown'].head(5).to_string()}

## Recommendations
"""
        
        # Generate recommendations
        if len(analysis['anomalies']) > 0:
            report += f"- Investigate {len(analysis['anomalies'])} cost anomalies\n"
        
        # Check for high-cost services
        high_cost_services = analysis['service_breakdown'][analysis['service_breakdown'] > analysis['service_breakdown'].quantile(0.95)]
        if len(high_cost_services) > 0:
            report += f"- Review high-cost services: {', '.join(high_cost_services.index)}\n"
        
        # Check for uneven AZ distribution
        az_variance = analysis['az_breakdown'].std() / analysis['az_breakdown'].mean()
        if az_variance > 0.5:
            report += "- Consider optimizing resource distribution across availability zones\n"
        
        return report

# Usage
cost_monitor = CloudCostMonitor("aws")
cost_data = cost_monitor.get_cost_data(days=30)
analysis = cost_monitor.analyze_cost_trends(cost_data)

# Create dashboard
cost_monitor.create_cost_dashboard(cost_data)

# Export metrics
cost_monitor.export_cost_metrics(cost_data)

# Generate report
report = cost_monitor.generate_cost_report(cost_data)
print(report)
```

### 8.3 Backup and Disaster Recovery

Implementing robust backup and disaster recovery strategies ensures business continuity.

#### Data Backup Strategies

**Automated Backup Configuration:**
```yaml
# backup-cronjob.yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: ml-data-backup
  namespace: ml-production
spec:
  schedule: "0 2 * * *"  # Daily at 2 AM
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: backup
            image: your-registry/backup-tools:v1.0.0
            command:
            - /bin/bash
            - -c
            - |
              # Database backup
              pg_dump -h postgres -U mluser -d ml_database > /backup/db_backup_$(date +%Y%m%d_%H%M%S).sql
              
              # Model artifacts backup
              tar -czf /backup/models_backup_$(date +%Y%m%d_%H%M%S).tar.gz /models/
              
              # Upload to cloud storage
              aws s3 cp /backup/ s3://ml-backups/$(date +%Y-%m-%d)/ --recursive
              
              # Cleanup old backups (keep last 30 days)
              find /backup -name "*.sql" -mtime +30 -delete
              find /backup -name "*.tar.gz" -mtime +30 -delete
            volumeMounts:
            - name: backup-volume
              mountPath: /backup
            - name: model-volume
              mountPath: /models
            env:
            - name: AWS_ACCESS_KEY_ID
              valueFrom:
                secretKeyRef:
                  name: aws-credentials
                  key: access-key
            - name: AWS_SECRET_ACCESS_KEY
              valueFrom:
                secretKeyRef:
                  name: aws-credentials
                  key: secret-key
          volumes:
          - name: backup-volume
            persistentVolumeClaim:
              claimName: backup-pvc
          - name: model-volume
            persistentVolumeClaim:
              claimName: model-pvc
          restartPolicy: OnFailure
```

**Point-in-Time Recovery:**
```python
# pitr_backup.py
import boto3
import psycopg2
from datetime import datetime, timedelta
import subprocess
import os

class PointInTimeRecovery:
    def __init__(self, db_config: dict, s3_bucket: str):
        self.db_config = db_config
        self.s3_bucket = s3_bucket
        self.s3_client = boto3.client('s3')
    
    def create_backup(self, backup_type: str = "full"):
        """Create database backup"""
        timestamp = datetime.now().strftime('%Y%m%d_%H%M%S')
        
        if backup_type == "full":
            self._create_full_backup(timestamp)
        elif backup_type == "incremental":
            self._create_incremental_backup(timestamp)
        
        # Upload to S3
        backup_file = f"backup_{timestamp}.sql"
        self.s3_client.upload_file(
            backup_file,
            self.s3_bucket,
            f"backups/{timestamp}/{backup_file}"
        )
        
        # Clean up local file
        os.remove(backup_file)
        
        return f"backups/{timestamp}/{backup_file}"
    
    def _create_full_backup(self, timestamp: str):
        """Create full database backup"""
        cmd = [
            'pg_dump',
            '-h', self.db_config['host'],
            '-U', self.db_config['user'],
            '-d', self.db_config['database'],
            '-f', f'backup_{timestamp}.sql',
            '--no-password',
            '--format=custom',
            '--compress=9'
        ]
        
        env = os.environ.copy()
        env['PGPASSWORD'] = self.db_config['password']
        
        subprocess.run(cmd, env=env, check=True)
    
    def _create_incremental_backup(self, timestamp: str):
        """Create incremental backup using WAL files"""
        # This would implement WAL-based incremental backup
        # Requires PostgreSQL WAL archiving setup
        pass
    
    def restore_to_point_in_time(self, target_time: datetime, target_db: str = None):
        """Restore database to specific point in time"""
        if target_db is None:
            target_db = f"{self.db_config['database']}_restored"
        
        # Find appropriate backup
        backup_path = self._find_backup_for_time(target_time)
        
        if not backup_path:
            raise ValueError(f"No suitable backup found for {target_time}")
        
        # Download backup
        local_backup = f"restore_backup.sql"
        self.s3_client.download_file(
            self.s3_bucket,
            backup_path,
            local_backup
        )
        
        try:
            # Create new database
            self._create_database(target_db)
            
            # Restore backup
            self._restore_backup(local_backup, target_db)
            
            # Apply WAL logs up to target time
            self._apply_wal_logs(target_db, target_time)
            
            return target_db
            
        finally:
            # Clean up
            if os.path.exists(local_backup):
                os.remove(local_backup)
    
    def _find_backup_for_time(self, target_time: datetime):
        """Find the most recent backup before target time"""
        # List backup objects in S3
        response = self.s3_client.list_objects_v2(
            Bucket=self.s3_bucket,
            Prefix='backups/'
        )
        
        if 'Contents' not in response:
            return None
        
        # Find most recent backup before target time
        backups = []
        for obj in response['Contents']:
            if obj['Key'].endswith('.sql'):
                # Extract timestamp from key
                timestamp_str = obj['Key'].split('/')[-2]  # Format: YYYYMMDD_HHMMSS
                backup_time = datetime.strptime(timestamp_str, '%Y%m%d_%H%M%S')
                
                if backup_time <= target_time:
                    backups.append((backup_time, obj['Key']))
        
        if not backups:
            return None
        
        # Return most recent backup
        backups.sort(key=lambda x: x[0], reverse=True)
        return backups[0][1]
    
    def _create_database(self, db_name: str):
        """Create new database for restoration"""
        conn = psycopg2.connect(
            host=self.db_config['host'],
            user=self.db_config['user'],
            password=self.db_config['password'],
            database='postgres'
        )
        
        conn.autocommit = True
        with conn.cursor() as cursor:
            cursor.execute(f"DROP DATABASE IF EXISTS {db_name}")
            cursor.execute(f"CREATE DATABASE {db_name}")
        
        conn.close()
    
    def _restore_backup(self, backup_file: str, target_db: str):
        """Restore backup to target database"""
        cmd = [
            'pg_restore',
            '-h', self.db_config['host'],
            '-U', self.db_config['user'],
            '-d', target_db,
            '--no-password',
            backup_file
        ]
        
        env = os.environ.copy()
        env['PGPASSWORD'] = self.db_config['password']
        
        subprocess.run(cmd, env=env, check=True)
    
    def _apply_wal_logs(self, target_db: str, target_time: datetime):
        """Apply WAL logs up to target time"""
        # This would implement WAL replay logic
        # Requires access to archived WAL files
        pass

# Usage
db_config = {
    'host': 'localhost',
    'user': 'mluser',
    'password': 'password',
    'database': 'ml_database'
}

pitr = PointInTimeRecovery(db_config, 'ml-backups-bucket')

# Create backup
backup_path = pitr.create_backup("full")

# Restore to specific point in time
target_time = datetime.now() - timedelta(hours=1)
restored_db = pitr.restore_to_point_in_time(target_time)
```

#### Disaster Recovery Planning

**Multi-Region Deployment:**
```yaml
# multi-region-deployment.yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: ml-api-multi-region
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/your-org/ml-infrastructure
    path: k8s
    targetRevision: HEAD
  destination:
    server: https://kubernetes.default.svc
    namespace: ml-production
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
  revisionHistoryLimit: 10

---
# Cross-region replication
apiVersion: v1
kind: ConfigMap
metadata:
  name: cross-region-config
  namespace: ml-production
data:
  primary-region: "us-east-1"
  secondary-region: "us-west-2"
  failover-threshold: "300"  # seconds
  health-check-interval: "30"

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api-global
  namespace: ml-production
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ml-api
      region: global
  template:
    metadata:
      labels:
        app: ml-api
        region: global
    spec:
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchLabels:
                app: ml-api
            topologyKey: kubernetes.io/hostname
      containers:
      - name: ml-api
        image: your-registry/ml-api:v1.0.0
        ports:
        - containerPort: 8000
        env:
        - name: PRIMARY_REGION
          valueFrom:
            configMapKeyRef:
              name: cross-region-config
              key: primary-region
        - name: SECONDARY_REGION
          valueFrom:
            configMapKeyRef:
              name: cross-region-config
              key: secondary-region
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
        resources:
          requests:
            memory: "512Mi"
            cpu: "500m"
          limits:
            memory: "1Gi"
            cpu: "1000m"
```

**Automated Failover System:**
```python
# failover_system.py
import boto3
import time
from datetime import datetime, timedelta
import requests
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

class DisasterRecoveryManager:
    def __init__(self, primary_region: str, secondary_region: str):
        self.primary_region = primary_region
        self.secondary_region = secondary_region
        
        self.route53 = boto3.client('route53')
        self.elb_primary = boto3.client('elbv2', region_name=primary_region)
        self.elb_secondary = boto3.client('elbv2', region_name=secondary_region)
        
        self.failover_threshold = 300  # 5 minutes
        self.health_check_interval = 30  # seconds
    
    def monitor_health(self):
        """Continuously monitor system health and trigger failover if needed"""
        while True:
            try:
                primary_healthy = self._check_region_health(self.primary_region)
                
                if not primary_healthy:
                    logger.warning("Primary region unhealthy, checking duration...")
                    
                    # Check if unhealthy for threshold duration
                    unhealthy_start = self._get_unhealthy_start_time()
                    if unhealthy_start:
                        duration = (datetime.now() - unhealthy_start).total_seconds()
                        
                        if duration >= self.failover_threshold:
                            logger.error("Primary region unhealthy for too long, initiating failover")
                            self._initiate_failover()
                        else:
                            logger.info(f"Primary region unhealthy for {duration:.0f}s, waiting...")
                    else:
                        self._set_unhealthy_start_time()
                else:
                    # Reset unhealthy state
                    self._clear_unhealthy_start_time()
                    logger.info("Primary region healthy")
                
            except Exception as e:
                logger.error(f"Health monitoring error: {e}")
            
            time.sleep(self.health_check_interval)
    
    def _check_region_health(self, region: str) -> bool:
        """Check health of a specific region"""
        try:
            # Check load balancer health
            if region == self.primary_region:
                elb_client = self.elb_primary
            else:
                elb_client = self.elb_secondary
            
            # Get target group health
            response = elb_client.describe_target_health(
                TargetGroupArn=self._get_target_group_arn(region)
            )
            
            healthy_count = sum(1 for target in response['TargetHealthDescriptions'] 
                              if target['TargetHealth']['State'] == 'healthy')
            
            total_count = len(response['TargetHealthDescriptions'])
            
            # Consider healthy if > 50% targets are healthy
            return healthy_count / total_count > 0.5 if total_count > 0 else False
            
        except Exception as e:
            logger.error(f"Health check failed for {region}: {e}")
            return False
    
    def _initiate_failover(self):
        """Initiate failover to secondary region"""
        try:
            logger.info("Starting failover process...")
            
            # Update Route 53 to point to secondary region
            self._update_dns_weights(primary_weight=0, secondary_weight=100)
            
            # Scale up secondary region
            self._scale_region(self.secondary_region, target_replicas=6)
            
            # Notify stakeholders
            self._send_failover_notification()
            
            # Start recovery process for primary region
            self._start_primary_recovery()
            
            logger.info("Failover completed successfully")
            
        except Exception as e:
            logger.error(f"Failover failed: {e}")
            raise
    
    def _update_dns_weights(self, primary_weight: int, secondary_weight: int):
        """Update Route 53 weighted routing"""
        # This would update Route 53 record sets
        pass
    
    def _scale_region(self, region: str, target_replicas: int):
        """Scale deployment in specified region"""
        # This would use Kubernetes API to scale deployments
        pass
    
    def _send_failover_notification(self):
        """Send notifications about failover"""
        # Send alerts via email, Slack, etc.
        pass
    
    def _start_primary_recovery(self):
        """Start recovery process for primary region"""
        # Automated recovery logic
        pass
    
    def _get_unhealthy_start_time(self) -> datetime:
        """Get when primary region became unhealthy"""
        # Implementation to track unhealthy state
        pass
    
    def _set_unhealthy_start_time(self):
        """Mark primary region as unhealthy"""
        # Implementation to store unhealthy timestamp
        pass
    
    def _clear_unhealthy_start_time(self):
        """Clear unhealthy state"""
        # Implementation to reset unhealthy tracking
        pass
    
    def _get_target_group_arn(self, region: str) -> str:
        """Get target group ARN for region"""
        # Implementation to retrieve target group ARN
        pass

# Usage
dr_manager = DisasterRecoveryManager("us-east-1", "us-west-2")

# Start health monitoring (would run in background)
# dr_manager.monitor_health()

# Manual failover test
# dr_manager._initiate_failover()
```

This comprehensive optimization and maintenance framework ensures that ML systems remain performant, cost-effective, and resilient in production environments. The combination of performance tuning, cost monitoring, and disaster recovery strategies provides a robust foundation for long-term ML operations.

## 9. Troubleshooting Guide

### 9.1 Common Operational Issues

#### What is Troubleshooting in MLOps?

**Troubleshooting** is the systematic process of diagnosing, identifying, and resolving issues in ML production systems. It involves methodical investigation using monitoring data, logs, and diagnostic tools to pinpoint root causes and implement effective solutions.

**Troubleshooting Methodology**:
- **Gather Information**: Collect relevant logs, metrics, and system state
- **Reproduce the Issue**: Create conditions that trigger the problem
- **Isolate Components**: Determine which system components are affected
- **Identify Root Cause**: Find the underlying cause rather than symptoms
- **Implement Fix**: Apply the appropriate solution
- **Verify Resolution**: Confirm the issue is resolved and monitor for recurrence
- **Document Solution**: Record the problem and solution for future reference

**Why Effective Troubleshooting Matters**:
- **Minimize Downtime**: Quick resolution reduces service unavailability
- **Cost Reduction**: Prevents prolonged outages and resource waste
- **Learning Opportunity**: Each issue provides insights for system improvement
- **Team Efficiency**: Well-documented solutions speed up future resolutions
- **User Trust**: Reliable systems maintain user confidence

#### Container Startup Failures

**Debugging Container Issues:**
```bash
# Check container status and recent events
kubectl get pods -n ml-production -o wide
kubectl get events -n ml-production --sort-by=.metadata.creationTimestamp | tail -20

# Get detailed pod information including events
kubectl describe pod <pod-name> -n ml-production

# Check container logs (current and previous)
kubectl logs <pod-name> -n ml-production -c <container-name> --tail=100
kubectl logs <pod-name> -n ml-production -c <container-name> --previous

# Check if pod is scheduled on a node
kubectl get pod <pod-name> -n ml-production -o jsonpath='{.spec.nodeName}'
kubectl describe node <node-name>

# Debug with ephemeral container for investigation
kubectl debug <pod-name> -n ml-production --image=busybox --target=<container-name> -- sh

# Check resource usage and limits
kubectl top pods -n ml-production
kubectl get pod <pod-name> -n ml-production -o jsonpath='{.spec.containers[*].resources}'

# Validate container image locally
docker run --rm -it --entrypoint /bin/bash your-registry/ml-api:latest

# Check image layers and size
docker history your-registry/ml-api:latest
docker inspect your-registry/ml-api:latest | jq '.Size'
```

**Common Container Issues and Solutions:**

**Issue: Image Pull Errors**
```bash
# Diagnose image pull issues
kubectl describe pod <pod-name> | grep -A 10 "Containers.*Container ID"
kubectl get pod <pod-name> -o yaml | grep -A 5 image

# Check image exists in registry
docker pull your-registry/ml-api:latest

# Verify registry credentials
kubectl get secrets -n ml-production
kubectl describe secret regcred -n ml-production

# Check image pull policy
kubectl get deployment ml-api -o yaml | grep imagePullPolicy

# Solutions:

# 1. Update image pull secret
kubectl create secret docker-registry regcred \
  --docker-server=your-registry.com \
  --docker-username=<username> \
  --docker-password=<password> \
  --docker-email=<email> -n ml-production

# 2. Update deployment to use the secret
kubectl patch serviceaccount default -p '{"imagePullSecrets": [{"name": "regcred"}]}' -n ml-production

# 3. Force image pull
kubectl patch deployment ml-api -p '{"spec":{"template":{"spec":{"containers":[{"name":"ml-api","imagePullPolicy":"Always"}]}}}}' -n ml-production

# 4. Check registry connectivity
kubectl run test-registry --image=busybox --rm -it --restart=Never -- wget -qO- https://your-registry.com/v2/
```

**Issue: Resource Constraints**
```bash
# Diagnose resource issues
kubectl describe pod <pod-name> | grep -A 20 "Containers"
kubectl get pod <pod-name> -o jsonpath='{.status.containerStatuses[*].lastState.terminated.reason}'

# Check current resource requests/limits
kubectl get pod <pod-name> -o jsonpath='{.spec.containers[*].resources}' | jq .

# Check node capacity and allocation
kubectl describe nodes | grep -A 10 "Allocated resources"
kubectl get nodes --show-labels

# Solutions:

# 1. Update resource limits
kubectl patch deployment ml-api -n ml-production --type='json' -p='[
  {"op": "replace", "path": "/spec/template/spec/containers/0/resources/requests/memory", "value": "1Gi"},
  {"op": "replace", "path": "/spec/template/spec/containers/0/resources/limits/memory", "value": "2Gi"},
  {"op": "replace", "path": "/spec/template/spec/containers/0/resources/requests/cpu", "value": "500m"},
  {"op": "replace", "path": "/spec/template/spec/containers/0/resources/limits/cpu", "value": "1000m"}
]'

# 2. Add resource quota to namespace
kubectl apply -f - <<EOF
apiVersion: v1
kind: ResourceQuota
metadata:
  name: ml-resource-quota
  namespace: ml-production
spec:
  hard:
    requests.cpu: "4"
    requests.memory: 8Gi
    limits.cpu: "8"
    limits.memory: 16Gi
EOF

# 3. Check for OOM kills
kubectl get events -n ml-production | grep -i "oom\|memory"
dmesg | grep -i "oom\|kill"

# 4. Add memory monitoring
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: memory-debugger
  namespace: ml-production
spec:
  containers:
  - name: debugger
    image: busybox
    command: ['sh', '-c', 'while true; do echo "$(date): $(ps aux | grep python | grep -v grep)"; sleep 30; done']
EOF
```

**Issue: Health Check Failures**
```bash
# Diagnose health check issues
kubectl describe pod <pod-name> | grep -A 10 "Readiness\|Liveness"
kubectl get pod <pod-name> -o jsonpath='{.status.conditions}'

# Test health endpoint manually
kubectl exec <pod-name> -n ml-production -c ml-api -- curl -f http://localhost:8000/health

# Check application logs during health check
kubectl logs <pod-name> -n ml-production -c ml-api --previous | grep -i health

# Debug health check script inside container
kubectl exec <pod-name> -n ml-production -c ml-api -- /bin/bash
# Inside container:
curl -v http://localhost:8000/health
python -c "import requests; print(requests.get('http://localhost:8000/health').status_code)"
ps aux | grep python
netstat -tlnp | grep 8000

# Solutions:

# 1. Fix health check endpoint
# In your application code, ensure health endpoint is accessible
@app.get("/health")
async def health_check():
    return {"status": "healthy", "timestamp": time.time()}

# 2. Update health check configuration
kubectl patch deployment ml-api --type='json' -p='[
  {"op": "replace", "path": "/spec/template/spec/containers/0/readinessProbe/httpGet/path", "value": "/health"},
  {"op": "replace", "path": "/spec/template/spec/containers/0/readinessProbe/initialDelaySeconds", "value": "30"},
  {"op": "replace", "path": "/spec/template/spec/containers/0/readinessProbe/periodSeconds", "value": "10"}
]'

# 3. Add startup probe for slow-starting apps
kubectl patch deployment ml-api --type='json' -p='[
  {"op": "add", "path": "/spec/template/spec/containers/0/startupProbe", "value": {
    "httpGet": {"path": "/health", "port": 8000},
    "initialDelaySeconds": 5,
    "periodSeconds": 10,
    "timeoutSeconds": 5,
    "successThreshold": 1,
    "failureThreshold": 30
  }}
]'

# 4. Check for port conflicts
kubectl get services -n ml-production
kubectl exec <pod-name> -n ml-production -- netstat -tlnp
```

#### Network Connectivity Problems

**Diagnosing Network Issues:**
```bash
# Check service discovery
kubectl get services -n ml-production -o wide
kubectl get endpoints -n ml-production -o wide

# Test service connectivity from within cluster
kubectl run test-pod --image=busybox --rm -it --restart=Never -- sh
# Inside test pod:
wget -qO- http://ml-api.ml-production.svc.cluster.local:8000/health
nslookup ml-api.ml-production.svc.cluster.local
curl -v http://ml-api:8000/health

# Check network policies
kubectl get networkpolicies -n ml-production
kubectl describe networkpolicy <policy-name> -n ml-production

# Test external connectivity
kubectl run test-external --image=busybox --rm -it --restart=Never -- sh
# Inside test pod:
wget -qO- https://httpbin.org/get

# Check DNS resolution
kubectl exec <pod-name> -n ml-production -- nslookup kubernetes.default.svc.cluster.local
kubectl logs -n kube-system -l k8s-app=kube-dns

# Solutions:

# 1. Fix service configuration
kubectl apply -f - <<EOF
apiVersion: v1
kind: Service
metadata:
  name: ml-api
  namespace: ml-production
spec:
  selector:
    app: ml-api
  ports:
  - port: 80
    targetPort: 8000
    protocol: TCP
  type: ClusterIP
EOF

# 2. Update network policies
kubectl apply -f - <<EOF
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: ml-api-network
  namespace: ml-production
spec:
  podSelector:
    matchLabels:
      app: ml-api
  policyTypes:
  - Ingress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: ingress-nginx
    ports:
    - protocol: TCP
      port: 8000
EOF

# 3. Check ingress configuration
kubectl get ingress -n ml-production
kubectl describe ingress ml-api-ingress -n ml-production
kubectl logs -n ingress-nginx deployment/ingress-nginx-controller

# 4. Debug DNS issues
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: dns-debug
  namespace: ml-production
spec:
  containers:
  - name: debug
    image: busybox
    command: ['sh', '-c', 'while true; do nslookup ml-api.ml-production.svc.cluster.local; sleep 30; done']
EOF
```

#### Model Performance Issues

**Diagnosing Model Problems:**
```bash
# Check model loading and inference
kubectl exec <pod-name> -n ml-production -c ml-api -- python -c "
import sys
sys.path.append('/app')
try:
    from model_loader import load_model
    model = load_model()
    print('Model loaded successfully')
    # Test inference
    import numpy as np
    test_input = np.random.rand(1, 10)
    result = model.predict(test_input)
    print(f'Inference successful: {result.shape}')
except Exception as e:
    print(f'Error: {e}')
"

# Check model file integrity
kubectl exec <pod-name> -n ml-production -c ml-api -- ls -la /app/models/
kubectl exec <pod-name> -n ml-production -c ml-api -- sha256sum /app/models/model.pkl

# Monitor prediction latency
kubectl logs <pod-name> -n ml-production -c ml-api | grep "prediction_time\|latency"

# Check for model drift
kubectl exec <pod-name> -n ml-production -c ml-api -- python -c "
# Check model metrics
import requests
response = requests.get('http://localhost:8000/metrics')
print(response.text)
"

# Solutions:

# 1. Model reloading issue
kubectl rollout restart deployment/ml-api -n ml-production

# 2. Memory issues with large models
# Increase memory limits
kubectl patch deployment ml-api -p '{"spec":{"template":{"spec":{"containers":[{"name":"ml-api","resources":{"limits":{"memory":"4Gi"}}}]}}}}' -n ml-production

# 3. Model corruption
# Redeploy with fresh model
kubectl set image deployment/ml-api ml-api=your-registry/ml-api:v1.1.0 -n ml-production

# 4. Performance degradation
# Check for memory leaks
kubectl exec <pod-name> -n ml-production -c ml-api -- python -c "
import psutil
import os
process = psutil.Process(os.getpid())
print(f'Memory usage: {process.memory_info().rss / 1024 / 1024:.2f} MB')
"
```

#### Database Connectivity Issues

**Diagnosing Database Problems:**
```bash
# Check database pod status
kubectl get pods -n ml-production -l app=postgres
kubectl describe pod postgres-0 -n ml-production

# Test database connectivity
kubectl exec <pod-name> -n ml-production -c ml-api -- python -c "
import psycopg2
import os
try:
    conn = psycopg2.connect(
        host=os.getenv('DB_HOST'),
        database=os.getenv('DB_NAME'),
        user=os.getenv('DB_USER'),
        password=os.getenv('DB_PASSWORD')
    )
    print('Database connection successful')
    conn.close()
except Exception as e:
    print(f'Database connection failed: {e}')
"

# Check database logs
kubectl logs postgres-0 -n ml-production

# Check connection pool
kubectl exec <pod-name> -n ml-production -c ml-api -- python -c "
# Check connection pool status
import os
print('DB Pool config:')
for key in ['DB_POOL_MIN', 'DB_POOL_MAX']:
    print(f'{key}: {os.getenv(key)}')
"

# Solutions:

# 1. Database connection timeout
# Update connection settings
kubectl set env deployment/ml-api DB_CONNECT_TIMEOUT=30 -n ml-production

# 2. Connection pool exhaustion
# Increase pool size
kubectl set env deployment/ml-api DB_POOL_MAX=20 -n ml-production

# 3. Database migration issues
# Run migrations manually
kubectl exec postgres-0 -n ml-production -- psql -U mluser -d ml_database -c "SELECT * FROM schema_migrations;"

# 4. Database backup/restore
# Create backup
kubectl exec postgres-0 -n ml-production -- pg_dump -U mluser ml_database > backup.sql

# Restore backup
kubectl exec -i postgres-0 -n ml-production -- psql -U mluser ml_database < backup.sql
```

#### Automated Troubleshooting

**Troubleshooting Automation:**
```python
# automated_troubleshooting.py
import logging
import time
from typing import Dict, List, Callable
from dataclasses import dataclass
from datetime import datetime
import subprocess
import json

logger = logging.getLogger(__name__)

@dataclass
class Issue:
    name: str
    description: str
    severity: str
    diagnostic_commands: List[str]
    solutions: List[str]
    automated_fix: Callable = None

class AutomatedTroubleshooter:
    """Automated troubleshooting system for ML operations"""

    def __init__(self):
        self.issues = self._define_issues()
        self.diagnostic_history = []

    def _define_issues(self) -> Dict[str, Issue]:
        """Define common issues and their diagnostics/solutions"""
        return {
            "container_crash": Issue(
                name="Container Crash",
                description="ML API container is crashing repeatedly",
                severity="HIGH",
                diagnostic_commands=[
                    "kubectl get pods -n ml-production -l app=ml-api",
                    "kubectl logs --previous -n ml-production -l app=ml-api | tail -50",
                    "kubectl describe pod -n ml-production -l app=ml-api"
                ],
                solutions=[
                    "Check application logs for error messages",
                    "Verify resource limits and requests",
                    "Check health check configuration",
                    "Validate environment variables"
                ]
            ),

            "high_latency": Issue(
                name="High Prediction Latency",
                description="ML predictions are taking too long",
                severity="MEDIUM",
                diagnostic_commands=[
                    "kubectl logs -n ml-production -l app=ml-api | grep prediction_time",
                    "kubectl top pods -n ml-production",
                    "kubectl exec -n ml-production -l app=ml-api -- python -c 'import psutil; print(psutil.virtual_memory())'"
                ],
                solutions=[
                    "Check model size and memory usage",
                    "Optimize model inference code",
                    "Consider model quantization",
                    "Scale up container resources"
                ]
            ),

            "database_connection": Issue(
                name="Database Connection Issues",
                description="ML API cannot connect to database",
                severity="HIGH",
                diagnostic_commands=[
                    "kubectl get pods -n ml-production -l app=postgres",
                    "kubectl logs -n ml-production -l app=postgres | tail -20",
                    "kubectl exec -n ml-production -l app=ml-api -- nc -zv postgres 5432"
                ],
                solutions=[
                    "Check database pod status",
                    "Verify database credentials",
                    "Check network policies",
                    "Validate connection string"
                ]
            ),

            "memory_leak": Issue(
                name="Memory Leak",
                description="Container memory usage is continuously increasing",
                severity="HIGH",
                diagnostic_commands=[
                    "kubectl top pods -n ml-production",
                    "kubectl logs -n ml-production -l app=ml-api | grep memory",
                    "kubectl exec -n ml-production -l app=ml-api -- python -c 'import gc; print(f\"Objects: {len(gc.get_objects())}\")'"
                ],
                solutions=[
                    "Profile application memory usage",
                    "Fix memory leaks in code",
                    "Implement proper garbage collection",
                    "Consider container restart policies"
                ]
            )
        }

    def diagnose_issue(self, issue_type: str) -> Dict:
        """Diagnose a specific issue type"""
        if issue_type not in self.issues:
            return {"error": f"Unknown issue type: {issue_type}"}

        issue = self.issues[issue_type]
        diagnosis = {
            "issue": issue.name,
            "description": issue.description,
            "severity": issue.severity,
            "timestamp": datetime.now().isoformat(),
            "diagnostics": {},
            "recommendations": issue.solutions
        }

        # Run diagnostic commands
        for cmd in issue.diagnostic_commands:
            try:
                result = subprocess.run(cmd, shell=True, capture_output=True, text=True, timeout=30)
                diagnosis["diagnostics"][cmd] = {
                    "success": result.returncode == 0,
                    "output": result.stdout,
                    "error": result.stderr
                }
            except subprocess.TimeoutExpired:
                diagnosis["diagnostics"][cmd] = {"error": "Command timed out"}
            except Exception as e:
                diagnosis["diagnostics"][cmd] = {"error": str(e)}

        self.diagnostic_history.append(diagnosis)
        return diagnosis

    def auto_fix_issue(self, issue_type: str) -> Dict:
        """Attempt automated fix for an issue"""
        if issue_type not in self.issues:
            return {"error": f"Unknown issue type: {issue_type}"}

        issue = self.issues[issue_type]

        if not issue.automated_fix:
            return {"error": f"No automated fix available for {issue_type}"}

        try:
            result = issue.automated_fix()
            return {
                "issue": issue.name,
                "fix_attempted": True,
                "result": result,
                "timestamp": datetime.now().isoformat()
            }
        except Exception as e:
            return {
                "issue": issue.name,
                "fix_attempted": True,
                "error": str(e),
                "timestamp": datetime.now().isoformat()
            }

    def get_diagnostic_history(self) -> List[Dict]:
        """Get history of all diagnostics performed"""
        return self.diagnostic_history

    def generate_troubleshooting_report(self) -> Dict:
        """Generate comprehensive troubleshooting report"""
        report = {
            "generated_at": datetime.now().isoformat(),
            "total_diagnostics": len(self.diagnostic_history),
            "issues_by_severity": {},
            "recent_issues": self.diagnostic_history[-10:]  # Last 10 diagnostics
        }

        # Count issues by severity
        for diagnosis in self.diagnostic_history:
            severity = diagnosis.get("severity", "UNKNOWN")
            report["issues_by_severity"][severity] = report["issues_by_severity"].get(severity, 0) + 1

        return report

# Global troubleshooter instance
troubleshooter = AutomatedTroubleshooter()

def restart_ml_deployment():
    """Automated fix: Restart ML deployment"""
    cmd = "kubectl rollout restart deployment/ml-api -n ml-production"
    result = subprocess.run(cmd, shell=True, capture_output=True, text=True)
    return {
        "command": cmd,
        "success": result.returncode == 0,
        "output": result.stdout,
        "error": result.stderr
    }

def scale_ml_deployment():
    """Automated fix: Scale ML deployment"""
    cmd = "kubectl scale deployment ml-api --replicas=3 -n ml-production"
    result = subprocess.run(cmd, shell=True, capture_output=True, text=True)
    return {
        "command": cmd,
        "success": result.returncode == 0,
        "output": result.stdout,
        "error": result.stderr
    }

# Add automated fixes to issues
troubleshooter.issues["container_crash"].automated_fix = restart_ml_deployment
troubleshooter.issues["high_latency"].automated_fix = scale_ml_deployment
```

This comprehensive troubleshooting guide provides systematic approaches to diagnosing and resolving common operational issues in ML production systems.

# Check network policies
kubectl get networkpolicies -n ml-production

# Test DNS resolution
kubectl exec <pod-name> -n ml-production -- nslookup ml-api.ml-production.svc.cluster.local

# Check ingress
kubectl get ingress -n ml-production
kubectl describe ingress ml-api-ingress -n ml-production
```

**Network Troubleshooting Tools:**
```bash
# Install network debugging tools
kubectl apply -f https://raw.githubusercontent.com/Praqma/Network-MultiTool/master/yaml/network-multitool.yaml

# Run network diagnostics
kubectl run net-debug --image=praqma/network-multitool --rm -it --restart=Never

# Inside debug container:
# Test connectivity
curl -v http://ml-api.ml-production.svc.cluster.local:8000/health

# Check DNS
nslookup ml-api.ml-production.svc.cluster.local

# Test external connectivity
curl -v https://api.example.com/health

# Packet capture
tcpdump -i eth0 port 8000
```

#### Resource Exhaustion Scenarios

**Memory Issues:**
```bash
# Check memory usage
kubectl top pods --containers -n ml-production

# Get memory dump (if enabled)
kubectl exec <pod-name> -n ml-production -- gcore -o /tmp/core $(pidof python)

# Check for memory leaks
kubectl exec <pod-name> -n ml-production -- python -c "
import psutil
import os
process = psutil.Process(os.getpid())
print(f'Memory usage: {process.memory_info().rss / 1024 / 1024:.2f} MB')
"

# Enable memory profiling
# In your application:
from memory_profiler import profile

@profile
def predict_function(data):
    # Your prediction logic
    pass
```

**CPU Issues:**
```bash
# Check CPU usage
kubectl top pods -n ml-production

# Profile CPU usage
kubectl exec <pod-name> -n ml-production -- python -c "
import cProfile
import pstats
from io import StringIO

pr = cProfile.Profile()
pr.enable()

# Your code to profile
import time
time.sleep(1)

pr.disable()
s = StringIO()
ps = pstats.Stats(pr, stream=s).sort_stats('cumulative')
ps.print_stats()
print(s.getvalue())
"

# Check for CPU-intensive threads
kubectl exec <pod-name> -n ml-production -- top -H -p $(pidof python)
```

### 9.2 Debugging Strategies

Systematic approaches to debugging complex ML system issues.

#### Log Analysis Techniques

**Centralized Log Analysis:**
```bash
# Search logs across pods
kubectl logs -l app=ml-api -n ml-production --tail=100 | grep ERROR

# Follow logs in real-time
kubectl logs -f <pod-name> -n ml-production

# Search logs with timestamps
kubectl logs <pod-name> -n ml-production --since=1h | grep "prediction"

# Export logs for analysis
kubectl logs <pod-name> -n ml-production > pod_logs.txt

# Analyze logs with jq (for JSON logs)
kubectl logs <pod-name> -n ml-production | jq '. | select(.level == "ERROR")'
```

**Log Pattern Analysis:**
```python
# log_analyzer.py
import re
from collections import defaultdict, Counter
import pandas as pd
from datetime import datetime

class LogAnalyzer:
    def __init__(self, log_file: str):
        self.log_file = log_file
        self.patterns = {
            'error': re.compile(r'ERROR|error|Error'),
            'warning': re.compile(r'WARNING|warning|Warning'),
            'prediction': re.compile(r'prediction.*score'),
            'latency': re.compile(r'latency.*(\d+\.?\d*)'),
            'memory': re.compile(r'memory.*(\d+)'),
            'cpu': re.compile(r'cpu.*(\d+\.?\d*)')
        }
    
    def analyze_logs(self):
        """Analyze log file for patterns and anomalies"""
        errors = []
        warnings = []
        predictions = []
        latencies = []
        memory_usage = []
        cpu_usage = []
        
        with open(self.log_file, 'r') as f:
            for line_num, line in enumerate(f, 1):
                # Check for errors
                if self.patterns['error'].search(line):
                    errors.append((line_num, line.strip()))
                
                # Check for warnings
                if self.patterns['warning'].search(line):
                    warnings.append((line_num, line.strip()))
                
                # Extract predictions
                pred_match = self.patterns['prediction'].search(line)
                if pred_match:
                    predictions.append((line_num, pred_match.group()))
                
                # Extract latency
                lat_match = self.patterns['latency'].search(line)
                if lat_match:
                    latencies.append(float(lat_match.group(1)))
                
                # Extract memory usage
                mem_match = self.patterns['memory'].search(line)
                if mem_match:
                    memory_usage.append(int(mem_match.group(1)))
                
                # Extract CPU usage
                cpu_match = self.patterns['cpu'].search(line)
                if cpu_match:
                    cpu_usage.append(float(cpu_match.group(1)))
        
        return {
            'errors': errors,
            'warnings': warnings,
            'predictions': predictions,
            'avg_latency': sum(latencies) / len(latencies) if latencies else 0,
            'max_latency': max(latencies) if latencies else 0,
            'avg_memory': sum(memory_usage) / len(memory_usage) if memory_usage else 0,
            'avg_cpu': sum(cpu_usage) / len(cpu_usage) if cpu_usage else 0,
            'error_count': len(errors),
            'warning_count': len(warnings)
        }
    
    def find_anomalies(self, analysis_results):
        """Find anomalous patterns in logs"""
        anomalies = []
        
        # Check for error spikes
        if analysis_results['error_count'] > 10:
            anomalies.append(f"High error count: {analysis_results['error_count']}")
        
        # Check for high latency
        if analysis_results['avg_latency'] > 1000:  # > 1 second
            anomalies.append(f"High average latency: {analysis_results['avg_latency']:.2f}ms")
        
        # Check for memory issues
        if analysis_results['avg_memory'] > 1024:  # > 1GB
            anomalies.append(f"High memory usage: {analysis_results['avg_memory']:.2f}MB")
        
        return anomalies
    
    def generate_report(self):
        """Generate comprehensive log analysis report"""
        analysis = self.analyze_logs()
        anomalies = self.find_anomalies(analysis)
        
        report = f"""
# Log Analysis Report

## Summary
- Total Errors: {analysis['error_count']}
- Total Warnings: {analysis['warning_count']}
- Average Latency: {analysis['avg_latency']:.2f}ms
- Maximum Latency: {analysis['max_latency']:.2f}ms
- Average Memory Usage: {analysis['avg_memory']:.2f}MB
- Average CPU Usage: {analysis['avg_cpu']:.2f}%

## Anomalies Detected
"""
        
        for anomaly in anomalies:
            report += f"- {anomaly}\n"
        
        if not anomalies:
            report += "No significant anomalies detected.\n"
        
        report += f"""
## Recent Errors
"""
        for line_num, error in analysis['errors'][-5:]:  # Last 5 errors
            report += f"Line {line_num}: {error[:100]}...\n"
        
        return report

# Usage
analyzer = LogAnalyzer("pod_logs.txt")
report = analyzer.generate_report()
print(report)
```

#### Performance Profiling Tools

**Application Performance Profiling:**
```python
# performance_profiler.py
import cProfile
import pstats
import io
import time
from functools import wraps
import memory_profiler
import psutil
import threading
from typing import Dict, List

class PerformanceProfiler:
    def __init__(self):
        self.profiles = {}
        self.metrics = {}
        
    def profile_function(self, func_name: str = None):
        """Decorator for function profiling"""
        def decorator(func):
            name = func_name or func.__name__
            
            @wraps(func)
            def wrapper(*args, **kwargs):
                pr = cProfile.Profile()
                pr.enable()
                
                start_time = time.time()
                start_memory = psutil.Process().memory_info().rss / 1024 / 1024  # MB
                
                try:
                    result = func(*args, **kwargs)
                    return result
                finally:
                    end_time = time.time()
                    end_memory = psutil.Process().memory_info().rss / 1024 / 1024
                    
                    pr.disable()
                    
                    # Store metrics
                    self.metrics[name] = {
                        'execution_time': end_time - start_time,
                        'memory_delta': end_memory - start_memory,
                        'cpu_percent': psutil.cpu_percent(interval=0.1)
                    }
                    
                    # Store profile
                    s = io.StringIO()
                    ps = pstats.Stats(pr, stream=s).sort_stats('cumulative')
                    ps.print_stats(10)  # Top 10 functions
                    self.profiles[name] = s.getvalue()
            
            return wrapper
        return decorator
    
    def profile_memory(self, func_name: str = None):
        """Decorator for memory profiling"""
        def decorator(func):
            name = func_name or func.__name__
            
            @wraps(func)
            @memory_profiler.profile
            def wrapper(*args, **kwargs):
                return func(*args, **kwargs)
            
            return wrapper
        return decorator
    
    def start_system_monitoring(self, interval: float = 1.0):
        """Start background system monitoring"""
        self.monitoring = True
        self.system_metrics = []
        
        def monitor():
            while self.monitoring:
                metrics = {
                    'timestamp': time.time(),
                    'cpu_percent': psutil.cpu_percent(interval=None),
                    'memory_percent': psutil.virtual_memory().percent,
                    'disk_io': psutil.disk_io_counters().read_bytes + psutil.disk_io_counters().write_bytes,
                    'network_io': psutil.net_io_counters().bytes_sent + psutil.net_io_counters().bytes_recv
                }
                self.system_metrics.append(metrics)
                time.sleep(interval)
        
        self.monitor_thread = threading.Thread(target=monitor, daemon=True)
        self.monitor_thread.start()
    
    def stop_system_monitoring(self):
        """Stop system monitoring"""
        self.monitoring = False
        if hasattr(self, 'monitor_thread'):
            self.monitor_thread.join(timeout=1)
    
    def analyze_performance(self) -> Dict:
        """Analyze collected performance data"""
        analysis = {
            'function_metrics': self.metrics,
            'system_metrics': self.system_metrics,
            'bottlenecks': []
        }
        
        # Identify bottlenecks
        for func_name, metrics in self.metrics.items():
            if metrics['execution_time'] > 1.0:  # > 1 second
                analysis['bottlenecks'].append(f"{func_name}: slow execution ({metrics['execution_time']:.2f}s)")
            
            if metrics['memory_delta'] > 100:  # > 100MB increase
                analysis['bottlenecks'].append(f"{func_name}: high memory usage ({metrics['memory_delta']:.2f}MB)")
        
        # Analyze system metrics trends
        if self.system_metrics:
            cpu_trend = [m['cpu_percent'] for m in self.system_metrics[-10:]]  # Last 10 readings
            memory_trend = [m['memory_percent'] for m in self.system_metrics[-10:]]
            
            if sum(cpu_trend) / len(cpu_trend) > 80:
                analysis['bottlenecks'].append("High average CPU usage")
            
            if sum(memory_trend) / len(memory_trend) > 85:
                analysis['bottlenecks'].append("High average memory usage")
        
        return analysis
    
    def generate_report(self) -> str:
        """Generate performance analysis report"""
        analysis = self.analyze_performance()
        
        report = "# Performance Analysis Report\n\n"
        
        report += "## Function Performance\n"
        for func_name, metrics in analysis['function_metrics'].items():
            report += f"### {func_name}\n"
            report += f"- Execution Time: {metrics['execution_time']:.4f}s\n"
            report += f"- Memory Delta: {metrics['memory_delta']:.2f}MB\n"
            report += f"- CPU Usage: {metrics['cpu_percent']:.1f}%\n\n"
        
        report += "## System Metrics\n"
        if analysis['system_metrics']:
            latest = analysis['system_metrics'][-1]
            report += f"- CPU Usage: {latest['cpu_percent']:.1f}%\n"
            report += f"- Memory Usage: {latest['memory_percent']:.1f}%\n"
            report += f"- Disk I/O: {latest['disk_io'] / 1024 / 1024:.2f}MB\n"
            report += f"- Network I/O: {latest['network_io'] / 1024 / 1024:.2f}MB\n\n"
        
        report += "## Identified Bottlenecks\n"
        for bottleneck in analysis['bottlenecks']:
            report += f"- {bottleneck}\n"
        
        if not analysis['bottlenecks']:
            report += "No significant bottlenecks detected.\n"
        
        return report

# Usage example
profiler = PerformanceProfiler()

@profiler.profile_function()
def slow_prediction_function(data):
    """Simulate a slow prediction function"""
    time.sleep(0.5)  # Simulate processing time
    return {"prediction": 1, "confidence": 0.85}

@profiler.profile_memory()
def memory_intensive_function():
    """Simulate memory-intensive operation"""
    large_list = [i for i in range(1000000)]  # Create large list
    return sum(large_list)

# Start system monitoring
profiler.start_system_monitoring()

# Run profiled functions
result1 = slow_prediction_function({"input": "test"})
result2 = memory_intensive_function()

# Stop monitoring
profiler.stop_system_monitoring()

# Generate report
report = profiler.generate_report()
print(report)
```

#### Root Cause Analysis Methods

**5-Why Analysis Framework:**
```python
# root_cause_analyzer.py
from typing import List, Dict, Optional
import json
from datetime import datetime

class RootCauseAnalyzer:
    def __init__(self):
        self.incidents = []
    
    def analyze_incident(self, incident_description: str, symptoms: List[str], 
                        timeline: List[Dict], logs: List[str]) -> Dict:
        """Perform root cause analysis using 5-Why method"""
        
        analysis = {
            'incident': incident_description,
            'symptoms': symptoms,
            'timeline': timeline,
            'five_whys': self._perform_five_whys(incident_description),
            'contributing_factors': self._identify_contributing_factors(logs),
            'preventive_actions': [],
            'detected_at': datetime.now().isoformat()
        }
        
        # Generate preventive actions based on root cause
        analysis['preventive_actions'] = self._generate_preventive_actions(analysis['five_whys'])
        
        return analysis
    
    def _perform_five_whys(self, problem: str) -> List[str]:
        """Perform 5-Why root cause analysis"""
        whys = [problem]
        
        # Predefined cause-effect relationships (would be expanded in practice)
        cause_map = {
            "Model predictions are slow": "High inference latency",
            "High inference latency": "Inefficient model implementation",
            "Inefficient model implementation": "No model optimization",
            "No model optimization": "Missing performance requirements",
            "Missing performance requirements": "Incomplete requirements gathering",
            
            "Application crashes": "Memory exhaustion",
            "Memory exhaustion": "Memory leak in prediction code",
            "Memory leak in prediction code": "Improper resource management",
            "Improper resource management": "Lack of code review",
            "Lack of code review": "Insufficient development processes",
            
            "Database connection failures": "Connection pool exhausted",
            "Connection pool exhausted": "High concurrent requests",
            "High concurrent requests": "Traffic spike",
            "Traffic spike": "No auto-scaling configured",
            "No auto-scaling configured": "Missing scalability planning"
        }
        
        current_problem = problem
        for _ in range(4):  # 4 more whys to make 5 total
            if current_problem in cause_map:
                next_cause = cause_map[current_problem]
                whys.append(next_cause)
                current_problem = next_cause
            else:
                # If no predefined cause, ask for manual input or use generic
                whys.append(f"Underlying cause for: {current_problem}")
                break
        
        return whys
    
    def _identify_contributing_factors(self, logs: List[str]) -> List[str]:
        """Identify contributing factors from logs"""
        factors = []
        
        error_patterns = [
            ('timeout', 'Timeout errors indicate performance issues'),
            ('memory', 'Memory-related errors suggest resource constraints'),
            ('connection', 'Connection errors indicate network or database issues'),
            ('permission', 'Permission errors suggest security or configuration issues'),
            ('validation', 'Validation errors indicate data quality issues')
        ]
        
        log_text = ' '.join(logs).lower()
        
        for pattern, description in error_patterns:
            if pattern in log_text:
                factors.append(description)
        
        return factors
    
    def _generate_preventive_actions(self, five_whys: List[str]) -> List[str]:
        """Generate preventive actions based on 5-Why analysis"""
        actions = []
        
        root_cause = five_whys[-1] if five_whys else ""
        
        # Action mapping based on root causes
        action_map = {
            "Incomplete requirements gathering": [
                "Implement comprehensive requirements gathering process",
                "Add performance benchmarks to requirements",
                "Include scalability requirements in planning"
            ],
            "Insufficient development processes": [
                "Implement mandatory code reviews",
                "Add automated testing for resource usage",
                "Establish performance testing in CI/CD"
            ],
            "Missing scalability planning": [
                "Implement auto-scaling policies",
                "Add load testing to deployment process",
                "Monitor resource usage trends"
            ]
        }
        
        if root_cause in action_map:
            actions.extend(action_map[root_cause])
        
        # Add general preventive actions
        actions.extend([
            "Implement comprehensive monitoring and alerting",
            "Establish regular performance reviews",
            "Create incident response playbooks",
            "Implement automated testing and validation"
        ])
        
        return actions
    
    def create_incident_report(self, analysis: Dict) -> str:
        """Create formatted incident report"""
        report = f"""
# Incident Analysis Report

## Incident Summary
**Description:** {analysis['incident']}

**Detected:** {analysis['detected_at']}

## Symptoms Observed
"""
        
        for symptom in analysis['symptoms']:
            report += f"- {symptom}\n"
        
        report += "\n## Timeline\n"
        for event in analysis['timeline']:
            report += f"- {event.get('timestamp', 'Unknown')}: {event.get('description', 'Unknown event')}\n"
        
        report += "\n## 5-Why Root Cause Analysis\n"
        for i, why in enumerate(analysis['five_whys'], 1):
            report += f"{i}. {why}\n"
        
        report += "\n## Contributing Factors\n"
        for factor in analysis['contributing_factors']:
            report += f"- {factor}\n"
        
        report += "\n## Preventive Actions\n"
        for action in analysis['preventive_actions']:
            report += f"- {action}\n"
        
        return report

# Usage example
analyzer = RootCauseAnalyzer()

incident_analysis = analyzer.analyze_incident(
    incident_description="Model predictions are slow",
    symptoms=[
        "Response time > 5 seconds",
        "CPU usage at 95%",
        "Memory usage increasing over time"
    ],
    timeline=[
        {"timestamp": "2024-01-01 10:00:00", "description": "Traffic spike detected"},
        {"timestamp": "2024-01-01 10:05:00", "description": "Response times increased"},
        {"timestamp": "2024-01-01 10:10:00", "description": "Application became unresponsive"}
    ],
    logs=[
        "ERROR: Timeout occurred during prediction",
        "WARNING: High memory usage detected",
        "INFO: CPU usage at 95%"
    ]
)

report = analyzer.create_incident_report(incident_analysis)
print(report)
```

### 9.3 Incident Response

Structured approaches to handling and recovering from system incidents.

#### Incident Response Procedures

**Incident Response Plan:**
```yaml
# incident_response_plan.yaml
incident_response:
  version: "1.0"
  last_updated: "2024-01-01"
  
  # Incident severity levels
  severity_levels:
    critical:
      description: "System completely unavailable, affecting all users"
      response_time: "15 minutes"
      communication: "Immediate notification to all stakeholders"
    
    high:
      description: "Major functionality impaired, affecting many users"
      response_time: "1 hour"
      communication: "Notification to engineering team and management"
    
    medium:
      description: "Some functionality impaired, affecting subset of users"
      response_time: "4 hours"
      communication: "Notification to engineering team"
    
    low:
      description: "Minor issues, minimal user impact"
      response_time: "24 hours"
      communication: "Internal tracking only"

  # Response phases
  phases:
    1_identify:
      name: "Identify"
      actions:
        - "Detect and acknowledge the incident"
        - "Assess severity and impact"
        - "Notify appropriate personnel"
        - "Create incident ticket"
    
    2_assess:
      name: "Assess"
      actions:
        - "Gather information about the incident"
        - "Determine scope and affected systems"
        - "Assess customer impact"
        - "Update severity if needed"
    
    3_contain:
      name: "Contain"
      actions:
        - "Stop the incident from spreading"
        - "Implement temporary workarounds"
        - "Scale back affected services if needed"
        - "Communicate status to stakeholders"
    
    4_resolve:
      name: "Resolve"
      actions:
        - "Identify root cause"
        - "Implement permanent fix"
        - "Test the fix"
        - "Deploy the fix"
    
    5_learn:
      name: "Learn"
      actions:
        - "Document the incident and resolution"
        - "Identify preventive measures"
        - "Update incident response procedures"
        - "Share learnings with team"

  # Communication templates
  communication_templates:
    initial_notification: |
      Subject: Incident Detected - {severity} Severity
      
      An incident has been detected affecting {affected_system}.
      
      Severity: {severity}
      Impact: {impact_description}
      Status: Investigating
      
      Incident Response Team has been notified and is working on resolution.
      
      Updates will be provided as available.
    
    status_update: |
      Subject: Incident Update - {incident_id}
      
      Current Status: {status}
      Timeline: {timeline_summary}
      ETA: {estimated_resolution}
      
      Next Update: {next_update_time}
    
    resolution_notification: |
      Subject: Incident Resolved - {incident_id}
      
      The incident has been resolved.
      
      Root Cause: {root_cause}
      Resolution: {resolution_summary}
      Duration: {incident_duration}
      
      Post-incident review will be conducted to prevent future occurrences.

  # Escalation procedures
  escalation:
    level_1: "On-call engineer"
    level_2: "Engineering manager (after 30 minutes)"
    level_3: "VP Engineering (after 2 hours)"
    level_4: "Executive team (after 4 hours)"

  # Contact information
  contacts:
    incident_response_team: "incident-response@company.com"
    engineering_manager: "eng-manager@company.com"
    communications: "communications@company.com"
    customers: "support@company.com"
```

**Automated Incident Response:**
```python
# incident_response_system.py
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
import json
import time
from datetime import datetime, timedelta
from typing import Dict, List, Optional
import threading
import logging

logging.basicConfig(level=logging.INFO)
logger = logging.getLogger(__name__)

class IncidentResponseSystem:
    def __init__(self, config_file: str = "incident_response_plan.yaml"):
        self.config = self._load_config(config_file)
        self.active_incidents = {}
        self.escalation_timers = {}
        
    def _load_config(self, config_file: str) -> Dict:
        """Load incident response configuration"""
        import yaml
        with open(config_file, 'r') as f:
            return yaml.safe_load(f)
    
    def create_incident(self, title: str, description: str, severity: str, 
                       affected_system: str, reporter: str) -> str:
        """Create a new incident"""
        
        incident_id = f"INC-{int(time.time())}"
        
        incident = {
            'id': incident_id,
            'title': title,
            'description': description,
            'severity': severity,
            'affected_system': affected_system,
            'reporter': reporter,
            'status': 'investigating',
            'created_at': datetime.now(),
            'updated_at': datetime.now(),
            'timeline': [{
                'timestamp': datetime.now(),
                'action': 'Incident created',
                'details': f'Created by {reporter}'
            }],
            'assigned_to': None,
            'escalation_level': 1
        }
        
        self.active_incidents[incident_id] = incident
        
        # Send initial notification
        self._send_initial_notification(incident)
        
        # Start escalation timer
        self._start_escalation_timer(incident_id)
        
        logger.info(f"Incident {incident_id} created: {title}")
        
        return incident_id
    
    def update_incident(self, incident_id: str, status: str = None, 
                       assigned_to: str = None, notes: str = None):
        """Update incident status"""
        
        if incident_id not in self.active_incidents:
            raise ValueError(f"Incident {incident_id} not found")
        
        incident = self.active_incidents[incident_id]
        incident['updated_at'] = datetime.now()
        
        if status:
            old_status = incident['status']
            incident['status'] = status
            self._add_timeline_entry(incident_id, f"Status changed from {old_status} to {status}")
        
        if assigned_to:
            incident['assigned_to'] = assigned_to
            self._add_timeline_entry(incident_id, f"Assigned to {assigned_to}")
        
        if notes:
            self._add_timeline_entry(incident_id, f"Notes: {notes}")
        
        # Send status update if resolved
        if status == 'resolved':
            self._send_resolution_notification(incident)
            self._stop_escalation_timer(incident_id)
    
    def _add_timeline_entry(self, incident_id: str, action: str, details: str = ""):
        """Add entry to incident timeline"""
        incident = self.active_incidents[incident_id]
        entry = {
            'timestamp': datetime.now(),
            'action': action,
            'details': details
        }
        incident['timeline'].append(entry)
    
    def _start_escalation_timer(self, incident_id: str):
        """Start escalation timer for incident"""
        incident = self.active_incidents[incident_id]
        severity = incident['severity']
        
        # Get escalation delays from config
        escalation_delays = {
            'critical': [30, 120, 240],  # minutes
            'high': [60, 240, 480],
            'medium': [240, 480, 1440],
            'low': [1440, 2880, 4320]
        }
        
        delays = escalation_delays.get(severity, [1440])
        
        def escalate_level(level: int):
            if incident_id in self.active_incidents:
                incident = self.active_incidents[incident_id]
                if incident['status'] != 'resolved':
                    incident['escalation_level'] = level
                    self._escalate_incident(incident_id, level)
                    
                    # Schedule next escalation if not at max level
                    if level < len(delays):
                        timer = threading.Timer(delays[level] * 60, escalate_level, args=[level + 1])
                        self.escalation_timers[incident_id] = timer
                        timer.start()
        
        # Start first escalation
        timer = threading.Timer(delays[0] * 60, escalate_level, args=[2])
        self.escalation_timers[incident_id] = timer
        timer.start()
    
    def _stop_escalation_timer(self, incident_id: str):
        """Stop escalation timer for resolved incident"""
        if incident_id in self.escalation_timers:
            self.escalation_timers[incident_id].cancel()
            del self.escalation_timers[incident_id]
    
    def _escalate_incident(self, incident_id: str, level: int):
        """Escalate incident to next level"""
        incident = self.active_incidents[incident_id]
        
        escalation_contacts = self.config['escalation']
        contact = escalation_contacts.get(f'level_{level}', 'incident-response@company.com')
        
        subject = f"INCIDENT ESCALATION - Level {level} - {incident['title']}"
        message = f"""
Incident {incident_id} has been escalated to level {level}.

Title: {incident['title']}
Severity: {incident['severity']}
Status: {incident['status']}
Assigned to: {incident.get('assigned_to', 'Unassigned')}

Please take immediate action.
"""
        
        self._send_email(contact, subject, message)
        logger.warning(f"Incident {incident_id} escalated to level {level}")
    
    def _send_initial_notification(self, incident: Dict):
        """Send initial incident notification"""
        template = self.config['communication_templates']['initial_notification']
        
        message = template.format(
            severity=incident['severity'].upper(),
            affected_system=incident['affected_system'],
            impact_description=incident['description']
        )
        
        # Send to incident response team
        self._send_email(
            self.config['contacts']['incident_response_team'],
            f"Incident Detected - {incident['severity'].upper()} Severity",
            message
        )
    
    def _send_resolution_notification(self, incident: Dict):
        """Send incident resolution notification"""
        template = self.config['communication_templates']['resolution_notification']
        
        duration = datetime.now() - incident['created_at']
        
        message = template.format(
            incident_id=incident['id'],
            root_cause="To be determined in post-incident review",
            resolution_summary="Incident has been resolved",
            incident_duration=str(duration)
        )
        
        # Send to stakeholders
        stakeholders = [
            self.config['contacts']['incident_response_team'],
            self.config['contacts']['engineering_manager']
        ]
        
        for stakeholder in stakeholders:
            self._send_email(stakeholder, f"Incident Resolved - {incident['id']}", message)
    
    def _send_email(self, to: str, subject: str, message: str):
        """Send email notification"""
        # Email configuration would be loaded from environment/config
        # This is a placeholder implementation
        
        logger.info(f"Email sent to {to}: {subject}")
        print(f"Would send email: {subject}")
        print(message)
    
    def get_incident_status(self, incident_id: str) -> Optional[Dict]:
        """Get current incident status"""
        return self.active_incidents.get(incident_id)
    
    def list_active_incidents(self) -> List[Dict]:
        """List all active incidents"""
        return list(self.active_incidents.values())

# Usage example
irs = IncidentResponseSystem()

# Create incident
incident_id = irs.create_incident(
    title="ML API High Latency",
    description="ML API response times > 5 seconds",
    severity="high",
    affected_system="ml-api",
    reporter="monitoring_system"
)

# Update incident
irs.update_incident(
    incident_id,
    status="investigating",
    assigned_to="john.doe@company.com",
    notes="Investigating database connection pool exhaustion"
)

# Later, resolve incident
irs.update_incident(
    incident_id,
    status="resolved",
    notes="Increased database connection pool size from 10 to 50"
)

# Check status
status = irs.get_incident_status(incident_id)
print(f"Incident {incident_id} status: {status['status']}")
```

#### Post-Incident Reviews

**Post-Incident Review Template:**
```markdown
# Post-Incident Review Report

## Incident Summary
- **Incident ID:** {incident_id}
- **Title:** {incident_title}
- **Date/Time:** {incident_datetime}
- **Duration:** {incident_duration}
- **Severity:** {severity_level}
- **Affected Systems:** {affected_systems}

## Impact Assessment
- **User Impact:** {user_impact_description}
- **Business Impact:** {business_impact_description}
- **Data Loss:** {data_loss_description}

## Timeline
1. {timestamp} - Incident detected by {detection_method}
2. {timestamp} - Initial assessment completed
3. {timestamp} - Containment measures implemented
4. {timestamp} - Root cause identified
5. {timestamp} - Resolution implemented
6. {timestamp} - Service fully restored

## Root Cause Analysis
### What happened?
{detailed_description_of_what_happened}

### Why did it happen?
1. {primary_root_cause}
2. {contributing_factor_1}
3. {contributing_factor_2}
4. {contributing_factor_3}

### What was the impact?
{impact_details}

## Response Assessment
### What went well?
- {positive_aspect_1}
- {positive_aspect_2}

### What could be improved?
- {improvement_area_1}
- {improvement_area_2}

## Action Items
### Immediate Actions (Complete within 24 hours)
- [ ] {immediate_action_1}
- [ ] {immediate_action_2}

### Short-term Actions (Complete within 1 week)
- [ ] {short_term_action_1}
- [ ] {short_term_action_2}

### Long-term Actions (Complete within 1 month)
- [ ] {long_term_action_1}
- [ ] {long_term_action_2}

## Prevention Measures
### Technical Measures
- {technical_prevention_1}
- {technical_prevention_2}

### Process Measures
- {process_improvement_1}
- {process_improvement_2}

### Monitoring Measures
- {monitoring_enhancement_1}
- {monitoring_enhancement_2}

## Lessons Learned
1. {lesson_1}
2. {lesson_2}
3. {lesson_3}

## Follow-up
- **Review Date:** {follow_up_date}
- **Responsible Party:** {responsible_person}
- **Success Criteria:** {success_criteria}

---
*This report was generated on {report_generation_date}*
```

This comprehensive troubleshooting guide provides systematic approaches to diagnosing issues, implementing fixes, and learning from incidents to improve system reliability and performance.

## 10. Resources and Best Practices

### 10.1 Official Documentation

#### What are MLOps Resources and Best Practices?

**MLOps Resources** encompass the comprehensive collection of documentation, tools, frameworks, and learning materials that support the implementation and maintenance of machine learning operations. These resources provide authoritative guidance, best practices, and practical implementations for building production-ready ML systems.

**Best Practices** are proven approaches and methodologies that have been validated through real-world implementation. They represent the collective wisdom of the MLOps community and provide standardized approaches to common challenges.

**Why Resources and Best Practices Matter**:
- **Accelerated Learning**: Access to expert knowledge and proven solutions
- **Consistency**: Standardized approaches across teams and projects
- **Quality Assurance**: Validated methods reduce errors and improve outcomes
- **Continuous Improvement**: Community-driven evolution of practices
- **Risk Mitigation**: Proven approaches minimize operational risks
- **Scalability**: Best practices enable systems that grow effectively

#### Cloud Platform Documentation

**AWS MLOps Resources:**
- **[AWS SageMaker Documentation](https://docs.aws.amazon.com/sagemaker/)**
  - Complete guide for ML model development, training, and deployment
  - Includes SageMaker Pipelines for CI/CD, Model Registry for versioning, and Endpoint management for serving
  - Covers AutoML, distributed training, and cost optimization
- **[AWS DevOps for ML](https://aws.amazon.com/devops/ml/)**
  - Best practices for CI/CD with ML workloads using CodePipeline, CodeBuild, and CodeDeploy
  - Integration patterns for ML model deployment and monitoring
  - Security and compliance considerations for ML systems
- **[Amazon EKS Documentation](https://docs.aws.amazon.com/eks/)**
  - Container orchestration for ML applications with advanced networking and security
  - Auto-scaling groups, GPU support, and hybrid cloud deployments
  - Integration with SageMaker for end-to-end ML workflows

**Google Cloud ML Resources:**
- **[Google Cloud AI Platform](https://cloud.google.com/ai-platform/docs)**
  - Unified platform for ML workflow management from Vertex AI
  - End-to-end ML operations including data labeling, training, and deployment
  - MLOps templates and reference architectures
- **[Kubernetes Engine (GKE) ML](https://cloud.google.com/kubernetes-engine/docs/concepts/ml)**
  - Running ML workloads on GKE with GPU support and auto-scaling
  - AI Platform integration and model serving optimizations
  - Security and networking best practices for ML applications
- **[Cloud Build for ML](https://cloud.google.com/cloud-build/docs/building/build-ml)**
  - CI/CD pipelines specifically designed for ML projects
  - Container building, testing, and deployment automation
  - Integration with GitHub, Cloud Source Repositories, and Artifact Registry

**Azure ML Documentation:**
- **[Azure Machine Learning](https://docs.microsoft.com/en-us/azure/machine-learning/)**
  - Complete ML platform with designer interface, automated ML, and pipelines
  - Model management, deployment, and monitoring capabilities
  - Integration with Azure DevOps and GitHub Actions
- **[Azure DevOps for AI](https://docs.microsoft.com/en-us/azure/devops/pipelines/targets/azure-machine-learning)**
  - CI/CD integration with Azure ML using YAML pipelines
  - Model training, testing, and deployment automation
  - Security scanning and compliance integration
- **[Azure Kubernetes Service](https://docs.microsoft.com/en-us/azure/aks/)**
  - Container orchestration for ML workloads with advanced scheduling
  - GPU support, auto-scaling, and integration with Azure ML
  - Security, networking, and cost optimization features

#### Kubernetes and Container Resources

**Official Kubernetes Documentation:**
- **[Kubernetes Concepts](https://kubernetes.io/docs/concepts/)**
  - Comprehensive guide to workloads (Pods, Deployments, StatefulSets)
  - Services, networking, and ingress management
  - Storage options, configuration management, and security policies
- **[kubectl Reference](https://kubernetes.io/docs/reference/kubectl/)**
  - Complete command-line tool reference with examples
  - Advanced operations, debugging commands, and automation scripts
  - Plugin ecosystem and customization options
- **[Kubernetes API](https://kubernetes.io/docs/reference/kubernetes-api/)**
  - REST API reference for programmatic access and automation
  - Custom resource definitions and operator development
  - Client library documentation for multiple languages

**Docker Resources:**
- **[Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)**
  - Container optimization techniques and image size reduction
  - Multi-stage builds, layer caching, and security hardening
  - Dockerfile patterns and anti-patterns
- **[Docker Compose](https://docs.docker.com/compose/)**
  - Multi-container application management and orchestration
  - Environment-specific configurations and secrets management
  - Integration with Docker Swarm and Kubernetes
- **[Docker Security](https://docs.docker.com/engine/security/)**
  - Container security best practices and threat mitigation
  - Image scanning, runtime security, and access controls
  - Compliance frameworks and security tools integration

#### ML-Specific Tools Documentation

**MLflow Documentation:**
- **[MLflow Tracking](https://mlflow.org/docs/latest/tracking.html)**
  - Experiment tracking, parameter logging, and metrics recording
  - Model artifact storage and experiment comparison
  - Integration with popular ML frameworks
- **[MLflow Models](https://mlflow.org/docs/latest/models.html)**
  - Model packaging formats and serving options
  - Custom model flavors and deployment targets
  - Model signature and input validation
- **[MLflow Registry](https://mlflow.org/docs/latest/registry.html)**
  - Model versioning, staging, and lifecycle management
  - Model approval workflows and access controls
  - Integration with CI/CD pipelines and deployment systems

**DVC (Data Version Control):**
- **[DVC Documentation](https://dvc.org/doc)**
  - Data and model versioning with Git-compatible workflows
  - Large file storage and efficient data transfer
  - Data pipeline management and reproducibility
- **[DVC Pipelines](https://dvc.org/doc/user-guide/pipelines)**
  - Reproducible ML pipelines with dependency tracking
  - Pipeline execution, caching, and parallel processing
  - Integration with CI/CD systems and cloud storage

**Kubeflow Documentation:**
- **[Kubeflow Pipelines](https://www.kubeflow.org/docs/components/pipelines/)**
  - ML workflow orchestration with visual pipeline designer
  - Component reusability and parameter passing
  - Integration with Kubernetes and cloud platforms
- **[Kubeflow Training](https://www.kubeflow.org/docs/components/training/)**
  - Distributed training operators for TensorFlow, PyTorch, and MPI
  - GPU resource management and job scheduling
  - Hyperparameter tuning and experiment tracking

### 10.2 Learning Resources

#### Online Courses and Certifications

**Coursera Specializations:**
- **[Machine Learning Engineering for Production (MLOps) Specialization](https://www.coursera.org/specializations/machine-learning-engineering-for-production-mlops)**
  - Comprehensive MLOps curriculum by Andrew Ng and Google Cloud
  - Covers deployment, monitoring, and scaling of ML systems
  - Includes hands-on projects with real-world scenarios
- **[MLOps Zoomcamp](https://github.com/DataTalksClub/mlops-zoomcamp)**
  - Free, practical MLOps course with code examples
  - Covers experiment tracking, model deployment, and monitoring
  - Community-driven with active Discord support

**Udacity Nanodegrees:**
- **[Machine Learning DevOps Engineer](https://www.udacity.com/course/machine-learning-devops-engineer-nanodegree--nd0821)**
  - End-to-end ML pipeline development and deployment
  - Focus on CI/CD, containerization, and cloud platforms
  - Real projects with industry partners

**edX Courses:**
- **[MLOps for Beginners](https://www.edx.org/learn/machine-learning/microsoft-mlops-for-beginners)**
  - Microsoft Learn collection covering MLOps fundamentals
  - Free courses with practical Azure ML examples
  - Certification preparation materials

#### Books and Publications

**Essential MLOps Books:**
- **"Building Machine Learning Pipelines" by Hannes Hapke and Catherine Nelson**
  - Comprehensive guide to ML pipeline construction
  - Covers data processing, model training, and deployment
  - Practical examples with open-source tools

- **"Machine Learning Engineering" by Andriy Burkov**
  - Focus on production ML system design
  - Covers scalability, reliability, and maintenance
  - Real-world case studies and best practices

- **"Designing Machine Learning Systems" by Chip Huyen**
  - System design principles for ML applications
  - Covers requirements, data, modeling, and deployment
  - Industry examples from leading companies

**Research Papers and White Papers:**
- **[MLflow: A Platform for the Machine Learning Lifecycle](https://www.databricks.com/blog/2018/06/05/introducing-mlflow-an-open-source-machine-learning-platform.html)**
  - Original MLflow paper introducing the platform
  - Architecture and design decisions
- **[TFX: A TensorFlow-Based Production-Scale Machine Learning Platform](https://arxiv.org/abs/2010.02013)**
  - Google's production ML platform architecture
  - Lessons learned from large-scale ML deployment
- **[Continuous Integration for Machine Learning](https://www.microsoft.com/en-us/research/uploads/prod/2019/03/Continuous-Integration-for-Machine-Learning-CI4ML.pdf)**
  - Microsoft's approach to ML CI/CD
  - Challenges and solutions for ML testing

#### Community Resources

**Online Communities:**
- **[MLOps Community Slack](https://mlops-community.slack.com/)**
  - Active community for MLOps discussions and support
  - Special interest channels for tools and platforms
  - Job postings and networking opportunities

- **[Kaggle MLOps Discussions](https://www.kaggle.com/discussions)**
  - Practical MLOps questions and solutions
  - Competition-winning approaches and techniques
  - Code sharing and collaboration

- **[Reddit r/MLOps](https://www.reddit.com/r/MLOps/)**
  - Community-driven discussions and news
  - Tool comparisons and career advice
  - Industry trends and job opportunities

**Conferences and Meetups:**
- **[MLOps World](https://www.mlops.world/)**
  - Annual conference focused on MLOps practices
  - Keynotes from industry leaders and practitioners
  - Workshops and networking opportunities

- **[Data Engineering Summit](https://www.dataengineeringsummit.com/)**
  - Focus on data platforms and ML infrastructure
  - Technical deep-dives and case studies

- **Local Meetups:**
  - [Meetup.com MLOps groups](https://www.meetup.com/topics/mlops/)
  - Local chapters for hands-on learning
  - Speaker sessions and hackathons

### 10.3 Best Practices Summary

#### Development Best Practices

**Code Quality and Testing:**
```python
# Comprehensive testing strategy
def test_ml_pipeline():
    """Test ML pipeline components"""
    # Unit tests for data processing
    def test_data_preprocessing():
        raw_data = load_test_data()
        processed_data = preprocess_data(raw_data)

        assert processed_data.shape[0] > 0
        assert 'target' in processed_data.columns
        assert processed_data.isnull().sum().sum() == 0

    # Integration tests for model training
    def test_model_training():
        X_train, X_test, y_train, y_test = prepare_data()

        model = train_model(X_train, y_train)
        predictions = model.predict(X_test)

        accuracy = accuracy_score(y_test, predictions)
        assert accuracy > 0.8  # Minimum acceptable accuracy

    # End-to-end pipeline tests
    def test_full_pipeline():
        # Test complete ML workflow
        pipeline = create_ml_pipeline()
        results = pipeline.run()

        assert 'model' in results
        assert 'metrics' in results
        assert results['metrics']['accuracy'] > 0.8
```

**Version Control for ML:**
```yaml
# .dvc/config for data versioning
core:
    analytics: false
    check_update: true
    machine: your-machine-name
    no_scm: false

states:
    cache:
        dir: .dvc/cache
    remote:
        origin:
            url: s3://ml-bucket/data
            region: us-east-1

# MLflow experiment tracking
import mlflow

def track_experiment():
    with mlflow.start_run():
        # Log parameters
        mlflow.log_param("model_type", "random_forest")
        mlflow.log_param("n_estimators", 100)

        # Log metrics
        mlflow.log_metric("accuracy", 0.85)
        mlflow.log_metric("precision", 0.82)

        # Log model
        mlflow.sklearn.log_model(model, "model")
```

#### Production Best Practices

**Security First Approach:**
```yaml
# Security checklist for ML deployment
security_checklist = {
    "container_security": [
        "Use minimal base images",
        "Scan images for vulnerabilities",
        "Run containers as non-root user",
        "Implement least privilege access"
    ],
    "data_protection": [
        "Encrypt data at rest and in transit",
        "Implement data access controls",
        "Regular security audits",
        "GDPR/CCPA compliance"
    ],
    "model_security": [
        "Validate model inputs",
        "Monitor for adversarial attacks",
        "Regular model updates",
        "Secure model storage"
    ]
}
```

**Monitoring and Alerting:**
```python
# Comprehensive monitoring setup
monitoring_config = {
    "metrics": [
        "prediction_latency",
        "model_accuracy",
        "data_drift_score",
        "system_resources"
    ],
    "alerts": [
        {
            "name": "High Latency Alert",
            "condition": "prediction_latency > 500ms for 5m",
            "severity": "warning"
        },
        {
            "name": "Model Drift Alert",
            "condition": "data_drift_score > 0.3",
            "severity": "critical"
        }
    ],
    "dashboards": [
        "System Performance",
        "Model Metrics",
        "Business KPIs"
    ]
}
```

**Disaster Recovery:**
```yaml
# Disaster recovery plan
dr_plan = {
    "backup_strategy": {
        "data_backup": "Daily incremental, weekly full",
        "model_backup": "Every model version",
        "config_backup": "Git-based configuration"
    },
    "recovery_procedures": {
        "data_recovery": "Point-in-time recovery within 1 hour",
        "service_recovery": "Automated failover within 5 minutes",
        "rto_rpo": {
            "recovery_time_objective": "4 hours",
            "recovery_point_objective": "1 hour"
        }
    },
    "testing": {
        "frequency": "Quarterly DR drills",
        "scope": "Full system failover testing"
    }
}
```

#### Team Collaboration Best Practices

**Documentation Standards:**
```markdown
# ML Project Documentation Template

## Overview
- Project purpose and objectives
- Key stakeholders and team members
- Success metrics and KPIs

## Architecture
- System architecture diagram
- Data flow and pipeline overview
- Technology stack and dependencies

## Development
- Development environment setup
- Code standards and conventions
- Testing strategy and coverage

## Deployment
- Deployment pipeline and process
- Environment configurations
- Rollback procedures

## Monitoring
- Key metrics and alerts
- Dashboard locations
- Incident response procedures

## Maintenance
- Update schedules and procedures
- Performance optimization plans
- Security maintenance tasks
```

**Knowledge Sharing:**
```python
# Team knowledge base structure
knowledge_base = {
    "runbooks": {
        "deployment": "deployment_runbook.md",
        "troubleshooting": "troubleshooting_guide.md",
        "incident_response": "incident_response.md"
    },
    "playbooks": {
        "model_update": "model_update_playbook.md",
        "scaling": "scaling_playbook.md",
        "security_incident": "security_incident_playbook.md"
    },
    "training": {
        "onboarding": "new_team_member_guide.md",
        "tool_training": "tool_training_materials/",
        "best_practices": "mlops_best_practices.md"
    }
}
```

This comprehensive resources and best practices section provides the foundation for continuous learning and improvement in MLOps implementation.

Curated learning paths and educational content for MLOps.

#### Online Courses and Certifications

**Coursera Specializations:**
- [MLOps Zoomcamp](https://github.com/DataTalksClub/mlops-zoomcamp)
  - Free, practical MLOps course
  - Covers deployment, monitoring, and scaling
- [Machine Learning Engineering for Production (MLOps)](https://www.coursera.org/specializations/machine-learning-engineering-for-production-mlops)
  - Comprehensive MLOps specialization
  - Google Cloud Platform focus

**Udacity Nanodegrees:**
- [Cloud DevOps using Microsoft Azure](https://www.udacity.com/course/cloud-devops-using-microsoft-azure-nanodegree--nd082)
  - DevOps practices with Azure
- [AWS Machine Learning Engineer](https://www.udacity.com/course/aws-machine-learning-engineer-nanodegree--nd189)
  - ML engineering on AWS

**edX Courses:**
- [DevOps and MLOps](https://www.edx.org/learn/devops)
  - Various DevOps and MLOps courses
- [Kubernetes for Developers](https://www.edx.org/learn/kubernetes)
  - Container orchestration skills

#### Books and Guides

**Essential MLOps Books:**
- "Building Machine Learning Pipelines" by Hannes Hapke and Catherine Nelson
  - Practical guide to ML pipeline construction
- "Machine Learning Engineering" by Andriy Burkov
  - End-to-end ML system design
- "Designing Data-Intensive Applications" by Martin Kleppmann
  - System design for data applications

**DevOps and Infrastructure Books:**
- "The DevOps Handbook" by Gene Kim, Jez Humble, Patrick Debois, and John Willis
  - Comprehensive DevOps practices
- "Kubernetes in Action" by Marko Luksa
  - Practical Kubernetes guide
- "Infrastructure as Code" by Kief Morris
  - IaC principles and practices

#### Community Resources

**GitHub Repositories:**
- [Awesome MLOps](https://github.com/visenger/awesome-mlops)
  - Curated list of MLOps tools and resources
- [ML Engineering](https://github.com/stanfordmlgroup/ml-engineering)
  - Stanford's ML engineering resources
- [Made With ML](https://github.com/GokuMohandas/MadeWithML)
  - MLOps examples and tutorials

**Blogs and Newsletters:**
- [Towards Data Science - MLOps](https://towardsdatascience.com/tagged/mlops)
  - Community articles on MLOps
- [Chip Huyen's Blog](https://huyenchip.com/)
  - ML engineering insights
- [MLOps Newsletter](https://mlops.news/)
  - Weekly MLOps updates

### 10.3 Best Practices Summary

Consolidated best practices for successful MLOps implementation.

#### Development Best Practices

**Code Quality and Testing:**
```python
# Example: Comprehensive testing strategy
import pytest
import unittest
from unittest.mock import Mock, patch
import numpy as np

class TestMLPipeline(unittest.TestCase):
    def setUp(self):
        """Set up test fixtures"""
        self.sample_data = np.random.randn(100, 10)
        self.sample_labels = np.random.randint(0, 2, 100)
    
    def test_data_validation(self):
        """Test data validation functions"""
        from your_pipeline import validate_data
        
        # Test valid data
        self.assertTrue(validate_data(self.sample_data, self.sample_labels))
        
        # Test invalid data shapes
        with self.assertRaises(ValueError):
            validate_data(np.random.randn(10, 5), self.sample_labels)
    
    @patch('your_pipeline.load_model')
    def test_model_loading(self, mock_load):
        """Test model loading with mocking"""
        mock_model = Mock()
        mock_load.return_value = mock_model
        
        from your_pipeline import get_model
        model = get_model('test_model')
        
        mock_load.assert_called_once_with('test_model')
        self.assertEqual(model, mock_model)
    
    def test_prediction_consistency(self):
        """Test prediction consistency"""
        from your_pipeline import predict
        
        # Make multiple predictions with same input
        pred1 = predict(self.sample_data[:10])
        pred2 = predict(self.sample_data[:10])
        
        np.testing.assert_array_equal(pred1, pred2)

# Integration tests
class TestIntegration(unittest.TestCase):
    def test_full_pipeline(self):
        """Test complete ML pipeline"""
        from your_pipeline import run_pipeline
        
        result = run_pipeline('test_config.yaml')
        
        self.assertIn('accuracy', result)
        self.assertIn('predictions', result)
        self.assertGreater(result['accuracy'], 0.5)

if __name__ == '__main__':
    # Run tests with coverage
    pytest.main(['-v', '--cov=your_pipeline', '--cov-report=html'])
```

**Version Control Practices:**
- Use semantic versioning (MAJOR.MINOR.PATCH)
- Maintain separate branches for features, releases, and hotfixes
- Implement pre-commit hooks for code quality checks
- Use conventional commits for clear change history

#### Operational Best Practices

**Monitoring and Alerting:**
```yaml
# Example: Comprehensive monitoring configuration
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

rule_files:
  - "alert_rules.yml"

alerting:
  alertmanagers:
    - static_configs:
        - targets:
          - alertmanager:9093

scrape_configs:
  - job_name: 'ml-api'
    static_configs:
      - targets: ['ml-api:8000']
    metrics_path: '/metrics'
    scrape_interval: 5s

  - job_name: 'ml-training'
    static_configs:
      - targets: ['ml-training:8000']
    metrics_path: '/metrics'

  - job_name: 'kubernetes-pods'
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

# alert_rules.yml
groups:
  - name: ml.alerts
    rules:
      - alert: HighPredictionLatency
        expr: histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m])) > 2
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High prediction latency detected"
          description: "95th percentile latency is {{ $value }}s"

      - alert: ModelAccuracyDrop
        expr: ml_model_accuracy < 0.8
        for: 10m
        labels:
          severity: critical
        annotations:
          summary: "Model accuracy dropped significantly"
          description: "Model accuracy is {{ $value }}"

      - alert: HighErrorRate
        expr: rate(http_requests_total{status=~"5.."}[5m]) / rate(http_requests_total[5m]) > 0.05
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: "High error rate detected"
          description: "Error rate is {{ $value | humanizePercentage }}"
```

**Security Best Practices:**
- Implement least privilege access (RBAC, IAM)
- Use secrets management (Vault, AWS Secrets Manager)
- Enable audit logging for all access
- Regular security scanning and vulnerability assessments
- Encrypt data at rest and in transit

#### Performance Optimization

**Resource Optimization:**
```python
# Example: Resource optimization utilities
import psutil
import GPUtil
from typing import Dict, Any
import threading
import time

class ResourceOptimizer:
    def __init__(self):
        self.monitoring = False
        self.metrics = []
        
    def start_resource_monitoring(self):
        """Start background resource monitoring"""
        self.monitoring = True
        
        def monitor():
            while self.monitoring:
                cpu = psutil.cpu_percent(interval=1)
                memory = psutil.virtual_memory()
                disk = psutil.disk_usage('/')
                
                gpu_info = []
                try:
                    gpus = GPUtil.getGPUs()
                    gpu_info = [{
                        'id': gpu.id,
                        'utilization': gpu.load * 100,
                        'memory_used': gpu.memoryUsed,
                        'memory_total': gpu.memoryTotal
                    } for gpu in gpus]
                except:
                    gpu_info = []
                
                self.metrics.append({
                    'timestamp': time.time(),
                    'cpu_percent': cpu,
                    'memory_percent': memory.percent,
                    'memory_used_gb': memory.used / (1024**3),
                    'disk_percent': disk.percent,
                    'gpu_info': gpu_info
                })
                
                time.sleep(5)  # Monitor every 5 seconds
        
        self.monitor_thread = threading.Thread(target=monitor, daemon=True)
        self.monitor_thread.start()
    
    def stop_resource_monitoring(self):
        """Stop resource monitoring"""
        self.monitoring = False
        if hasattr(self, 'monitor_thread'):
            self.monitor_thread.join(timeout=1)
    
    def get_resource_recommendations(self) -> Dict[str, Any]:
        """Generate resource optimization recommendations"""
        if not self.metrics:
            return {}
        
        # Analyze recent metrics (last 10 readings)
        recent = self.metrics[-10:] if len(self.metrics) >= 10 else self.metrics
        
        avg_cpu = sum(m['cpu_percent'] for m in recent) / len(recent)
        avg_memory = sum(m['memory_percent'] for m in recent) / len(recent)
        peak_memory = max(m['memory_used_gb'] for m in recent)
        
        recommendations = {
            'cpu_scaling': self._cpu_recommendation(avg_cpu),
            'memory_scaling': self._memory_recommendation(avg_memory, peak_memory),
            'gpu_optimization': self._gpu_recommendation(recent),
            'cost_optimization': self._cost_recommendation(avg_cpu, avg_memory)
        }
        
        return recommendations
    
    def _cpu_recommendation(self, avg_cpu: float) -> str:
        """Generate CPU scaling recommendation"""
        if avg_cpu > 80:
            return "Consider increasing CPU allocation or implementing horizontal scaling"
        elif avg_cpu < 30:
            return "CPU utilization is low; consider reducing allocation for cost optimization"
        else:
            return "CPU utilization is optimal"
    
    def _memory_recommendation(self, avg_memory: float, peak_memory: float) -> str:
        """Generate memory scaling recommendation"""
        if avg_memory > 85:
            return f"High memory usage ({avg_memory:.1f}%); increase memory allocation"
        elif peak_memory > 8:  # GB
            return f"High peak memory usage ({peak_memory:.1f}GB); consider memory optimization"
        elif avg_memory < 40:
            return "Memory utilization is low; consider reducing allocation"
        else:
            return "Memory utilization is optimal"
    
    def _gpu_recommendation(self, metrics: list) -> str:
        """Generate GPU optimization recommendation"""
        gpu_utils = []
        for metric in metrics:
            for gpu in metric.get('gpu_info', []):
                gpu_utils.append(gpu['utilization'])
        
        if gpu_utils:
            avg_gpu = sum(gpu_utils) / len(gpu_utils)
            if avg_gpu > 80:
                return "High GPU utilization; consider GPU optimization or additional GPUs"
            elif avg_gpu < 30:
                return "Low GPU utilization; consider using smaller GPU instances"
            else:
                return "GPU utilization is optimal"
        else:
            return "No GPU usage detected"
    
    def _cost_recommendation(self, avg_cpu: float, avg_memory: float) -> str:
        """Generate cost optimization recommendation"""
        if avg_cpu < 30 and avg_memory < 40:
            return "Low resource utilization; consider using smaller instance types"
        elif avg_cpu > 70 or avg_memory > 80:
            return "High resource utilization; consider larger instance types or auto-scaling"
        else:
            return "Resource utilization is balanced for current instance type"

# Usage
optimizer = ResourceOptimizer()
optimizer.start_resource_monitoring()

# Run your workload
time.sleep(60)  # Simulate 1 minute of work

optimizer.stop_resource_monitoring()
recommendations = optimizer.get_resource_recommendations()

for category, recommendation in recommendations.items():
    print(f"{category}: {recommendation}")
```

#### Deployment Best Practices

**Zero-Downtime Deployment:**
```yaml
# Example: Blue-green deployment with Kubernetes
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ml-api-blue
  namespace: ml-production
spec:
  replicas: 3
  selector:
    matchLabels:
      app: ml-api
      version: blue
  template:
    metadata:
      labels:
        app: ml-api
        version: blue
    spec:
      containers:
      - name: ml-api
        image: your-registry/ml-api:v2.0.0
        ports:
        - containerPort: 8000
        readinessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 5
          periodSeconds: 5
        livenessProbe:
          httpGet:
            path: /health
            port: 8000
          initialDelaySeconds: 30
          periodSeconds: 10

---
apiVersion: v1
kind: Service
metadata:
  name: ml-api-service
  namespace: ml-production
spec:
  selector:
    app: ml-api
    version: blue  # Point to blue deployment
  ports:
  - port: 80
    targetPort: 8000
  type: LoadBalancer

---
# Deployment script for blue-green deployment
# deploy.sh
#!/bin/bash

set -e

NEW_VERSION=$1
CURRENT_COLOR=$(kubectl get service ml-api-service -o jsonpath='{.spec.selector.version}')

if [ "$CURRENT_COLOR" = "blue" ]; then
    NEW_COLOR="green"
else
    NEW_COLOR="blue"
fi

echo "Deploying to $NEW_COLOR environment..."

# Deploy new version
kubectl set image deployment/ml-api-$NEW_COLOR ml-api=your-registry/ml-api:$NEW_VERSION

# Wait for rollout to complete
kubectl rollout status deployment/ml-api-$NEW_COLOR

# Run smoke tests
echo "Running smoke tests..."
kubectl run smoke-test --image=your-registry/smoke-test --rm -it --restart=Never -- \
  curl -f http://ml-api-$NEW_COLOR:8000/health

# Switch traffic
kubectl patch service ml-api-service -p "{\"spec\":{\"selector\":{\"app\":\"ml-api\",\"version\":\"$NEW_COLOR\"}}}"

echo "Traffic switched to $NEW_COLOR environment"

# Keep old deployment for rollback
echo "Keeping $CURRENT_COLOR environment for rollback capability"
```

**Rollback Strategies:**
- Implement automated rollback triggers
- Maintain multiple deployment versions
- Use feature flags for gradual rollouts
- Implement circuit breakers for automatic rollback

### 10.4 Tools and Frameworks Comparison

Comparative analysis of popular MLOps tools and frameworks.

#### Experiment Tracking Tools

| Tool | Features | Pros | Cons | Best For |
|------|----------|------|------|----------|
| MLflow | Tracking, Registry, UI | Open-source, language agnostic | Limited collaboration features | Small to medium teams |
| Weights & Biases | Advanced visualization, collaboration | Rich UI, team features | Commercial pricing | Research and collaboration |
| Comet.ml | Model monitoring, production tracking | End-to-end ML lifecycle | Complex setup | Enterprise deployments |
| ClearML | Automation, pipelines | Open-source core | Steep learning curve | CI/CD integration |

#### Model Serving Frameworks

| Framework | Features | Pros | Cons | Best For |
|-----------|----------|------|------|----------|
| FastAPI | Async, auto-docs, validation | Fast development, Python-native | Python-only | REST API serving |
| TensorFlow Serving | Optimized for TF models | High performance, scalable | TF ecosystem only | TensorFlow models |
| TorchServe | PyTorch model serving | Production-ready, multi-model | PyTorch-only | PyTorch models |
| BentoML | Multi-framework support | Flexible, cloud-native | Newer project | Multi-framework serving |
| Seldon Core | Kubernetes-native | Enterprise features | Complex setup | Kubernetes deployments |

#### Pipeline Orchestration

| Tool | Features | Pros | Cons | Best For |
|------|----------|------|------|----------|
| Kubeflow Pipelines | Kubernetes-native, UI | Scalable, portable | Complex setup | Kubernetes environments |
| Apache Airflow | Flexible scheduling, UI | Mature, extensible | Resource intensive | Complex workflows |
| Prefect | Python-native, hybrid execution | Easy to use, modern | Newer ecosystem | Python teams |
| Dagster | Software-defined assets | Type safety, testing | Steep learning curve | Data engineering |

#### Infrastructure as Code

| Tool | Features | Pros | Cons | Best For |
|------|----------|------|------|----------|
| Terraform | Multi-cloud, state management | Declarative, mature | Complex syntax | Multi-cloud deployments |
| AWS CDK | Programming languages | Familiar syntax, AWS optimized | AWS-only | AWS-focused teams |
| Pulumi | Multi-language, component resources | Programming languages | Newer project | Developer experience |
| CloudFormation | AWS native, integrated | AWS integrated | AWS-only, verbose | AWS-only deployments |

### 10.5 Career Development

Resources for advancing your MLOps career.

#### Skill Development Roadmap

**Beginner Level:**
- Learn Python programming fundamentals
- Understand basic ML concepts (scikit-learn, pandas)
- Introduction to Docker and containerization
- Basic Git and version control

**Intermediate Level:**
- Advanced Python (async programming, testing)
- Cloud platforms (AWS/GCP/Azure basics)
- Kubernetes fundamentals
- CI/CD with GitHub Actions
- Basic monitoring with Prometheus

**Advanced Level:**
- Distributed systems design
- Infrastructure as Code (Terraform)
- Advanced Kubernetes (operators, service mesh)
- ML pipeline orchestration (Kubeflow)
- Security and compliance
- Performance optimization

#### Certifications

**Cloud Certifications:**
- AWS Certified Machine Learning - Specialty
- Google Cloud Professional Cloud Architect
- Microsoft Azure AI Engineer Associate
- Certified Kubernetes Administrator (CKA)

**DevOps Certifications:**
- AWS DevOps Engineer Professional
- Google Cloud DevOps Engineer
- Docker Certified Associate
- HashiCorp Terraform Associate

#### Community Involvement

**Contribute to Open Source:**
- MLflow, Kubeflow, DVC contributions
- Write technical blog posts
- Speak at conferences (PyData, KubeCon)
- Create educational content

**Professional Networks:**
- LinkedIn MLOps groups
- Reddit (r/MLOps, r/DevOps)
- Slack communities (Kubeflow, MLflow)
- Local meetups and conferences

This comprehensive MLOps guide provides everything needed to implement, operate, and optimize machine learning systems in production. From development environment setup through advanced optimization techniques, it covers the complete operational lifecycle with practical examples, best practices, and extensive resources for continuous learning and improvement.

## 1. Core Building Blocks

### 1.1 Data Management
- [1.1.a Data Collection and Storage](#111-data-collection-and-storage)
- [1.1.b Data Versioning](#112-data-versioning)
- [1.1.c Data Quality and Validation](#113-data-quality-and-validation)

### 1.2 Model Development
- [1.2.a Experiment Tracking](#121-experiment-tracking)
- [1.2.b Model Training Pipelines](#122-model-training-pipelines)
- [1.2.c Hyperparameter Tuning](#123-hyperparameter-tuning)

### 1.3 Model Deployment
- [1.3.a Containerization](#131-containerization)
- [1.3.b Model Serving](#132-model-serving)
- [1.3.c API Development](#133-api-development)

### 1.4 Monitoring and Maintenance
- [1.4.a Performance Monitoring](#141-performance-monitoring)
- [1.4.b Drift Detection](#142-drift-detection)
- [1.4.c Automated Retraining](#143-automated-retraining)

## 2. MLOps Tools and Frameworks

### 2.1 MLflow
### 2.2 Kubeflow
### 2.3 DVC (Data Version Control)
### 2.4 Weights & Biases

## 3. Development Workflow

### 3.1 Data Engineering for ML
- [ETL Pipelines](#etl-pipelines)
- [Feature Engineering](#feature-engineering)
- [Data Pipeline Orchestration](#data-pipeline-orchestration)
- [Data Quality Monitoring](#data-quality-monitoring)

### 3.2 Model Training and Validation
- [Cross-Validation Techniques](#cross-validation-techniques)
- [Model Evaluation Metrics](#model-evaluation-metrics)
- [A/B Testing](#ab-testing)
- [Model Validation Strategies](#model-validation-strategies)

### 3.3 CI/CD for Machine Learning
- [Automated Testing](#automated-testing)
- [Continuous Integration](#continuous-integration)
- [Continuous Deployment](#continuous-deployment)

## 4. Production Deployment

### 4.1 Deployment Strategies
- [Blue-Green Deployment](#blue-green-deployment)
- [Canary Deployment](#canary-deployment)
- [Shadow Deployment](#shadow-deployment)
- [Multi-Model Serving](#multi-model-serving)

### 4.2 Containerization and Orchestration
- [Docker - Containerization](#docker---containerization)
- [Kubernetes - Orchestration](#kubernetes---orchestration)
- [Serverless ML](#serverless-ml)

### 4.3 Scaling and Performance
- [Horizontal Scaling](#horizontal-scaling)
- [Load Balancing](#load-balancing)
- [Cost Optimization](#cost-optimization)

## 5. Monitoring and Observability

### 5.1 Model Performance Monitoring
- [Accuracy Metrics](#accuracy-metrics)
- [Latency Monitoring](#latency-monitoring)
- [Throughput Tracking](#throughput-tracking)

### 5.2 System Health Monitoring
- [Infrastructure Monitoring](#infrastructure-monitoring)
- [Resource Utilization](#resource-utilization)
- [Error Rate Tracking](#error-rate-tracking)

### 5.3 Logging and Alerting
- [Logging Best Practices](#logging-best-practices)
- [Alerting Systems](#alerting-systems)
- [Incident Response](#incident-response)

## 6. Advanced MLOps Topics

### 6.1 AutoML
### 6.2 Federated Learning
### 6.3 Edge ML Deployment
### 6.4 MLOps for Large Language Models

## 7. Business Use Cases and Examples

### 7.1 Industry Applications
- [Fraud Detection](#fraud-detection)
- [Recommendation Systems](#recommendation-systems)
- [Predictive Maintenance](#predictive-maintenance)
- [Customer Churn Prediction](#customer-churn-prediction)

### 7.2 Real-World Examples
- [End-to-End ML Pipeline](#end-to-end-ml-pipeline)
- [Model A/B Testing System](#model-ab-testing-system)
- [Automated Retraining Pipeline](#automated-retraining-pipeline)
- [Multi-Cloud ML Deployment](#multi-cloud-ml-deployment)

## 8. Best Practices and Security

### 8.1 Security and Privacy
- [Data Encryption](#data-encryption)
- [Model Security](#model-security)
- [Access Control](#access-control)
- [GDPR Compliance](#gdpr-compliance)

### 8.2 Compliance Considerations
- [Data Privacy](#data-privacy)
- [Model Fairness](#model-fairness)
- [Ethical AI](#ethical-ai)

### 8.3 Performance Optimization
- [Model Compression](#model-compression)
- [Inference Optimization](#inference-optimization)
- [Caching Strategies](#caching-strategies)

### 8.4 Testing and Documentation
- [Unit Testing](#unit-testing)
- [Integration Testing](#integration-testing)
- [Model Documentation](#model-documentation)

## 9. Troubleshooting

### 9.1 Common Issues
- [Data Pipeline Failures](#data-pipeline-failures)
- [Model Serving Issues](#model-serving-issues)
- [Performance Bottlenecks](#performance-bottlenecks)
- [Integration Problems](#integration-problems)

### 9.2 Debugging Strategies
- [Root Cause Analysis](#root-cause-analysis)
- [Performance Profiling](#performance-profiling)
- [Log Analysis](#log-analysis)

## 10. Resources and Further Reading

### 10.1 Official Documentation
### 10.2 Learning Resources
### 10.3 Community and Events

### 📘 Learning Path Overview

1. **Core building blocks**
   - [Data Management](#11-data-management): Establish robust data pipelines and quality controls
   - [Model Development](#12-model-development): Build reproducible training workflows
   - [Model Deployment](#13-model-deployment): Deploy models reliably at scale
   - [Monitoring and Maintenance](#14-monitoring-and-maintenance): Keep models performing in production

2. **Tools and frameworks**
   - Choose appropriate tools for your use case (MLflow, Kubeflow, DVC, etc.)

3. **Production readiness**
   - Containerization, orchestration, monitoring, and security

4. **Advanced topics**
   - AutoML, federated learning, edge deployment, and specialized MLOps for LLMs

### 🔄 MLOps Lifecycle

```
Data Collection → Data Processing → Model Training → Model Validation → Deployment → Monitoring → Retraining
      ↑                                                                                      ↓
      └───────────────────────────────────────────────────────────────────────────────────────┘
```

### 🛠️ Key MLOps Components

- **Data Versioning**: Track changes in datasets and features
- **Experiment Tracking**: Log parameters, metrics, and artifacts
- **Model Registry**: Store and version trained models
- **CI/CD Pipelines**: Automate testing and deployment
- **Model Serving**: Deploy models as APIs or services
- **Monitoring**: Track performance and detect issues
- **Retraining**: Automatically update models with new data

### 📊 Essential Skills

- Python programming and data science libraries
- Containerization (Docker) and orchestration (Kubernetes)
- Cloud platforms (AWS, GCP, Azure)
- Version control (Git) and data versioning (DVC)
- Monitoring and logging tools
- DevOps practices adapted for ML

### 🚀 Getting Started

1. Learn Python and basic ML concepts
2. Set up a simple ML pipeline with experiment tracking
3. Containerize and deploy a model
4. Implement monitoring and automated retraining
5. Scale to production with proper infrastructure

### 📈 Career Path

- ML Engineer → MLOps Engineer → ML Platform Engineer
- Focus on automation, scalability, and reliability
- Bridge between data science and engineering teams