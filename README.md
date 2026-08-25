# CI/CD React Application Deployment to AWS EC2

## Application
- React + Vite frontend application
- Displays CI/CD deployment status

## Architecture
- **GitHub**: Source code repository
- **GitHub Actions**: CI/CD pipeline
- **Docker**: Containerization
- **Amazon ECR**: Docker image registry
- **Amazon EC2**: Application hosting

## Continuous Integration (CI)
- Checkout code
- Install dependencies (`npm ci`)
- Run linting (`npm run lint`)
- Build application (`npm run build`)

## Continuous Deployment (CD)
- Build Docker image
- Push to Amazon ECR
- SSH to EC2
- Pull new image
- Stop old container
- Run new container

## Dockerfile
- **Stage 1**: Node.js 22 Alpine - Build React app
- **Stage 2**: Nginx Alpine - Serve built files

## GitHub Secrets
- AWS_ACCESS_KEY_ID
- AWS_SECRET_ACCESS_KEY
- AWS_SESSION_TOKEN
- EC2_HOST
- EC2_SSH_PRIVATE_KEY

## Problems Encountered
### Problem 1: Dockerfile not found in GitHub Actions
- **Error**: `open Dockerfile: no such file or directory`
- **Cause**: Dockerfile not pushed to GitHub
- **Solution**: Added Dockerfile and .dockerignore, pushed to GitHub

### Problem 2: SSH connection timeout
- **Error**: `ssh: connect to host port 22: Operation timed out`
- **Cause**: EC2 Public IP changed after reboot
- **Solution**: Updated EC2_HOST secret with new IP

### Problem 3: Configure SSH step failed in GitHub Actions
- **Error**: `mkdir -p ~/.ssh` exit code 1
- **Cause**: Permission issue in GitHub runner
- **Solution**: Used official `webfactory/ssh-agent` action

## Live URL
http://54.161.139.52