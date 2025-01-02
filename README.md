# better
node.js application

# Node.js CI/CD Pipeline with Jenkins, Docker, Kubernetes, and AWS SNS

This repository demonstrates a CI/CD pipeline for a Node.js application using Jenkins. The pipeline automates testing, building, and deployment of the application to a Kubernetes cluster, and includes deployment notifications using AWS SNS.

---

## Features

1. *Automated Testing*: Runs unit tests on every pull request.
2. *Docker Image Creation*: Builds a Docker image and pushes it to a container registry.
3. *Kubernetes Deployment*: Deploys the application to a Kubernetes cluster.
4. *Notifications*: Sends success or failure notifications using AWS SNS.

---

## Prerequisites

### Jenkins Setup
- *Required Plugins*:
  - Git
  - Docker Pipeline
  - Kubernetes CLI (kubectl)
  - Pipeline: AWS Steps
- A Jenkins agent with:
  - Docker installed and configured.
  - kubectl installed and configured to interact with your Kubernetes cluster.
  - AWS CLI installed and configured.

### AWS Setup
- An SNS topic created in AWS.
- AWS access keys for a user with permissions to publish messages to the SNS topic.

### Kubernetes Cluster
- A running Kubernetes cluster.
- Kubernetes manifests for deployment (deployment.yml and service.yml).

### Jenkins Credentials
- *Docker Credentials*:
  - ID: dockerhubcred
  - Username and password for Docker Hub or other container registry.
- *AWS Credentials*:
  - ID: awscreds
  - AWS access key and secret key.
- *Kubernetes Config*:
  - ID: kubeconfig
  - Your kubeconfig file for accessing the Kubernetes cluster.

---

## Folder Structure

.
├── Jenkinsfile             # Defines the CI/CD pipeline
├── k8s/
│   ├── deployment.yaml     # Kubernetes deployment manifest
│   └── service.yaml        # Kubernetes service manifest
├── package.json            # Node.js dependencies and scripts
├── src/                    # Node.js application source code
└── test/                   # Test files

