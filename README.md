# Achat DevOps Project

## Pipeline Stages

### Git Checkout
- Checkout the code from the git repository

### Compile and Build 
- Compile the code
- Build Maven package

### SonarQube Scan
- Run SonarQube scan on the code

### Build Docker Image
- Build Docker image
- Push Docker image to Docker Hub

### Deploy to Nexus
Nexus is used as a repository manager where we can store our build artifacts. It is used to share artifacts between development teams and also to deploy artifacts. It is also used to manage the dependencies of various build artifacts.

### Prometheus & Grafana
- 