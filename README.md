# Spring Boot Application for Kubernetes Deployment

This repository contains a Spring Boot application designed for containerization and deployment on Kubernetes, integrated with Snyk for vulnerability scanning. The project demonstrates a real-world DevOps workflow, including building, securing, and deploying a containerized application with zero-downtime rolling upgrades on Google Kubernetes Engine (GKE).

## Project Overview
- **Application**: A Spring Boot app built with Maven, containerized using Docker, and deployed to a GKE cluster named "Lab3".
- **Security**: Scanned with Snyk, remediating 75 vulnerabilities (23 critical, 24 high, 27 medium, 1 low) by upgrading to Java 17 and updating dependencies.
- **Deployment**: Utilizes Kubernetes for orchestration, with a rolling upgrade from `vinod1089/spring-boot-app:latest` to `vinod1089/spring-boot-app:fix3.4.5`.
- **Build Environment**: Built on an AWS EC2 server with Docker, Maven, and Java 17.

## Key Files
- `pom.xml`: Maven configuration, updated to Java 17 and secure dependencies.
- `Dockerfile`: Defines the Docker image, using Java 17 JRE.
- `spring-boot-deployment.yml`: Kubernetes deployment and service configuration for GKE.
- `src/`: Spring Boot application source code, including `spring-boot-initial-0.0.1-SNAPSHOT.jar`.

## Setup Instructions
1. **Prerequisites**:
   - Install Maven, Docker allcomes with EC2 build and then move the SpringBootKubernetesApp to EC2 instance home directroy to move on to the next steps.
2. **Build the Application**:
   ```bash
   mvn clean package
3. **Set up a GKE cluster and Docker Hub account**:
4. **Setup Snyk accound and integrate with Docker using DocerHub Token**:
Generates spring-boot-initial-0.0.1-SNAPSHOT.jar in the target/ directory.
5. **Build and Push Docker Image**:
 
  docker build -t vinod1089/spring-boot-app:latest .
  docker login
  docker push vinod1089/spring-boot-app:latest

For the fixed version:

docker build -t vinod1089/spring-boot-app:fix3.4.5 .
docker push vinod1089/spring-boot-app:fix3.4.5

Deploy to GKE:
kubectl apply -f spring-boot-deployment.yml
kubectl get svc

Access the app via the service’s external IP in a browser.

Scan with Snyk:
Create a Snyk account and generate a Docker Hub token.
Run scans:
snyk test --docker vinod1089/spring-boot-app:latest
snyk test --docker vinod1089/spring-boot-app:fix3.4.5

Achievements
Eliminated 75 vulnerabilities, achieving 0 issues in the fix3.4.5 branch by updating to Java 17.
Executed a zero-downtime rolling upgrade on GKE, monitored with kubectl get pods and kubectl describe pod.
Visualized security improvements with a chart and workflow diagram (see project report).

Related Repository
EC2 Build Server Setup: AWS EC2 build server configuration.

Learn More
Check out my [project report]([Insert report link]) for detailed documentation, screenshots (e.g., Snyk results, kubectl outputs, Docker Hub), and visualizations.
Author: Vinod Kumar Dhanavath
Portfolio: [Insert portfolio link, if applicable]
LinkedIn: [Insert LinkedIn profile link, if desired]
