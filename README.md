# hv-container-orchestration

Container orchestration assignment.

# MERN Stack Kubernetes Deployment with Helm & Jenkins

## Overview

This project contains:

- Dockerfiles for frontend (React) and backend (Node.js/Express)
- A single Helm chart that deploys both services using a loop in templates
- Jenkins pipeline for automated CI/CD
- MongoDB Atlas connection via `ATLAS_URI` env variable

## How It Works

1. **Dockerfiles** build the application images.
2. **Helm chart** deploys both apps with a single `values.yaml`.
3. **Jenkins pipeline** builds images, pushes to Docker Hub, and deploys via Helm.
4. **MongoDB Atlas** is used as the database (no local Mongo in Kubernetes).

## Steps to Deploy

```bash
helm upgrade --install mern-stack ./hv-container-orchestration
/container-orchestration-chart-0.1.0.tgz
```
