# CI/CD Pipeline for Node.js Application with Docker and Kubernetes

This repository contains a Node.js application configured with a full CI/CD pipeline using GitHub Actions. The pipeline includes testing, linting, building, containerizing the app with Docker, scanning for vulnerabilities, and deploying to a Kubernetes cluster.

## 📦 Features

- ✅ Automated unit testing using `npm test`
- 🧹 Static code analysis with ESLint
- 🔧 Build process using `npm run build`
- 🐳 Docker image creation and push to GitHub Container Registry (GHCR)
- 🔍 Security scanning using Trivy
- ☸️ Auto-update Kubernetes deployment with the new Docker image
- 🛠️ Smart skip for `kubernetes/deployment.yml` changes to avoid CI loops

## 🚀 CI/CD Pipeline Overview

### Triggers
- On `push` to the `main` branch (except changes to `kubernetes/deployment.yml`)
- On pull request to the `main` branch

### Workflow Stages

1. **Unit Testing**
   - Runs `npm test` to ensure code correctness.

2. **Linting**
   - Runs `npm run lint` for static code analysis.

3. **Build**
   - Executes `npm run build` and uploads the output as artifacts.

4. **Docker Build & Scan**
   - Builds a Docker image using Buildx.
   - Scans the image using Trivy for vulnerabilities (fails on CRITICAL/HIGH issues).
   - Pushes the image to [GitHub Container Registry](https://ghcr.io/).

5. **Kubernetes Deployment Update**
   - Updates the image tag in `kubernetes/deployment.yml` to the new image.
   - Commits and pushes the updated manifest (skips CI using `[skip ci]`).

## 🐳 Docker Image

Images are pushed to:  
`ghcr.io/<owner>/<repo>:<tag>`

Tags include:
- Short SHA
- Branch name
- `latest`

## ⚙️ Secrets Required

Ensure the following secret is configured in your GitHub repository:

- `TOKEN`: A GitHub Personal Access Token with `write:packages`, `repo`, and `workflow` scopes.

## 🧪 Commands

To run locally:

```bash
npm ci           # Install dependencies
npm run lint     # Lint the code
npm test         # Run tests
npm run build    # Build the project
