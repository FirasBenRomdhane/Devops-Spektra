# Achat-App DevOps Pipeline

This repository contains the Jenkins pipeline for automating the build, test, and deployment processes of the Achat-App Backend using Jenkins, Maven, Docker, SonarQube, Nexus, and Docker Hub.

## Pipeline Overview

### Stage 1: Initialize
- Start Docker containers for SonarQube and Nexus.
- Sleep for 30 seconds to ensure containers are up.

### Stage 2: Checkout Code
- Clone the code from the [GitHub repository](https://github.com/FirasBenRomdhane/Devops-Spektra.git) with the specified branch (`abdessalem_mami`).

### Stage 3: Clean & Compile
- Clean and compile the Maven project.

### Stage 4: SonarQube Analysis
- Run SonarQube Code Analysis on the project.

### Stage 5: Deploy with Nexus
- Deploy the project artifact to the Nexus repository.

### Stage 6: Build Docker Image
- Build a Docker image tagged as `abdessalemmami/achat-app:1.0.0`.

### Stage 7: Push to Docker Hub
- Log in to Docker Hub using credentials from Jenkins credentials.
- Push the Docker image to Docker Hub.

### Stage 8: Run App with Docker Compose
- Start the application using Docker Compose.

### Stage 9-10: Prometheus & Grafana
- Start Prometheus and Grafana containers.

### Post-build Actions
- **Success:**
  - Send a success email notification with the build details.
  
- **Failure:**
  - Send a failure email notification with the build details.

