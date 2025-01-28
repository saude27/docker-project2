# AWS Dockerized Web App Deployment

This project demonstrates the setup and deployment of a dynamic web application on AWS using Docker, Amazon Elastic Container Registry (ECR), and Amazon Elastic Container Service (ECS). The deployment leverages a three-tier architecture for scalability, security, and maintainability.

---

## Project Overview

This project automates the deployment of a web application using AWS and Docker. The app is hosted in an AWS VPC with the following key components:
- **Frontend**: Accessible through an Application Load Balancer.
- **Backend**: Secured with an EC2 Bastion host and an RDS database.
- **Environment Variables**: Stored securely in an S3 bucket.

---

## Features

- Dockerized web app for consistent deployment.
- Secure multi-tier VPC architecture.
- Automated build and push to Amazon ECR.
- Scalable deployment with Amazon ECS.
- HTTPS support via SSL/TLS certificate.

---

## Prerequisites

- AWS account with required permissions.
- [AWS CLI](https://aws.amazon.com/cli/) installed and configured.
- Docker installed on your local machine.
- Git installed for repository management.
- Personal Access Token for GitHub.

---

## Setup and Deployment

### 1. **AWS VPC Configuration**
- **Create a VPC** with private and public subnets.
- Attach an **Internet Gateway** to the public subnets.
- Configure a **Route Table** and associate it with subnets.
- Create a **NAT Gateway** for internet access from private subnets.
- Set up **Security Groups** for controlled access.

### 2. **Database Configuration**
- Launch an Amazon RDS instance.
- Configure the database and security groups for your application.

### 3. **Dockerize the Application**
- Write a `Dockerfile` to define the app environment.
- Use `.gitignore` to prevent sensitive files from being committed.
- Build and test the Docker image locally.

### 4. **Push to Amazon ECR**
- Authenticate Docker with ECR using AWS CLI.
- Tag and push the Docker image to your ECR repository.

### 5. **Set Up ECS**
- Create an ECS cluster.
- Define a task with the ECR image and environment variables.
- Create a service for scaling and management.

### 6. **Application Load Balancer**
- Configure a target group for your ECS tasks.
- Create an Application Load Balancer for public access.

### 7. **Domain and SSL**
- Register your domain and create a Route 53 record set.
- Request and attach an SSL certificate for HTTPS.

---

## Dockerfile Explanation

The `Dockerfile` builds a lightweight environment for the web application:

1. **Base Image**: Amazon Linux 2.
2. **Software Installation**: Apache, PHP, MySQL, and dependencies.
3. **Git Repository Cloning**: The app's code is pulled from GitHub.
4. **Environment Configuration**: `.env` variables for app and database setup.
5. **Ports**: Apache (80) and MySQL (3306) exposed.
6. **Entrypoint**: Apache runs in the foreground.

---

## Environment Configuration

- **APP_ENV**: Application environment (e.g., `production`).
- **APP_URL**: Public URL of the application.
- **DB_HOST**: RDS endpoint.
- **DB_DATABASE**: RDS database name.
- **DB_USERNAME**: RDS master username.
- **DB_PASSWORD**: RDS master password.

Environment variables are updated dynamically in the Docker build process.

---

## AWS Services Used

- **Amazon VPC**: Isolated network for the application.
- **Amazon ECR**: Repository for Docker images.
- **Amazon ECS**: Orchestrates container deployment.
- **Amazon RDS**: Managed database instance.
- **Amazon S3**: Stores environment files securely.
- **Amazon Route 53**: Domain name configuration.
- **AWS Certificate Manager**: SSL/TLS certificates.
- **Amazon EC2**: Bastion host for secure access.

---

## Key Commands

### Docker
```bash
# Build Docker image
docker build -t your-image-name .

# Tag Docker image for ECR
docker tag your-image-name:latest <account_id>.dkr.ecr.<region>.amazonaws.com/<repository_name>:latest

# Push image to ECR
docker push <account_id>.dkr.ecr.<region>.amazonaws.com/<repository_name>:latest

