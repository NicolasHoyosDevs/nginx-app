# CI/CD Pipeline with AWS ECS

This project implements a complete CI/CD pipeline on AWS using:
- **Amazon ECS (Fargate)** - Container orchestration
- **Application Load Balancer (ALB)** - Load balancing for Testing and Production
- **AWS CodePipeline** - CI/CD orchestration
- **AWS CodeBuild** - Docker image building
- **Amazon ECR** - Container registry
- **Terraform** - Infrastructure as Code
- **GitHub** - Source code repository

## Architecture

```
GitHub → CodePipeline → CodeBuild → ECR → ECS (Testing) → ECS (Production)
                           ↓                      ↓              ↓
                        Build Image         Manual Approval  Manual Approval
                                                  ↓              ↓
                                            ALB Testing    ALB Production
```

## Project Structure

```
.
├── app/
│   ├── Dockerfile       # Docker image definition
│   ├── index.html       # Nginx web application
│   └── nginx.conf       # Nginx configuration
├── buildspec.yml        # CodeBuild build instructions
└── README.md            # This file
```

## Environments

- **Testing**: Deployment environment for testing before production
- **Production**: Final production environment

## Pipeline Stages

1. **Source**: Fetch code from GitHub
2. **Build**: Build Docker image and push to ECR
3. **Approval (Testing)**: Manual approval required
4. **Deploy to Testing**: Deploy to Testing environment
5. **Approval (Production)**: Manual approval required
6. **Deploy to Production**: Deploy to Production environment

## Technology Stack

- **Frontend**: Nginx serving static HTML
- **Container**: Docker
- **Orchestration**: AWS ECS Fargate
- **CI/CD**: AWS CodePipeline + CodeBuild
- **Infrastructure**: Terraform
- **Source Control**: GitHub

## Deployment

The pipeline automatically triggers on every push to the `main` branch.

## Health Check

Both environments expose a health check endpoint at `/health` for the ALB to monitor container health.
