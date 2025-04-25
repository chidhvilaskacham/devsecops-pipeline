# GitHub Actions CI/CD Pipeline 

This document outlines a robust CI/CD pipeline tailored for TypeScript Applications, leveraging GitHub Actions to automate the complete software delivery lifecycle. This pipeline emphasizes best practices for continuous integration and continuous deployment, ensuring high-quality, reliable, and efficient deployments.

## Table of Contents

* [Overview](#overview)
* [Workflow](#workflow)
* [Jobs](#jobs)
    * [Test](#test)
    * [Lint](#lint)
    * [Build](#build)
    * [Docker](#docker)
    * [Update Kubernetes Deployment](#update-kubernetes-deployment)
* [Triggers](#triggers)
* [Usage](#usage)

## Overview

This pipeline automates the testing, linting, building, and deployment of Node.js applications.  It employs a modular design, where jobs are executed sequentially or in parallel based on their dependencies.  The pipeline is initiated by `push` events to the `main` branch (excluding changes to `kubernetes/deployment.yaml`) and `pull_request` events targeting the `main` branch, facilitating both continuous integration and deployment workflows.

## Workflow

The workflow, defined in `.github/workflows/main.yml`, comprises the following jobs:

1.  **Test**: Executes unit tests.
2.  **Lint**: Performs static code analysis.
3.  **Build**: Builds the Node.js project.
4.  **Docker**: Builds a container image, performs vulnerability scanning, and pushes the image to the GitHub Container Registry.
5.  **Update Kubernetes Deployment**: Updates the Kubernetes deployment manifest with the new container image tag.

## Jobs

### Test

* **Name**: Unit Testing
* **Description**:  This job performs unit tests to ensure code functionality and prevent regressions.

### Lint

* **Name**: Static Code Analysis
* **Description**: This job performs static analysis of the codebase to identify potential errors and enforce code style guidelines.

### Build

* **Name**: Build
* **Description**: This job compiles and prepares the Node.js project for deployment.

### Docker

* **Name**: Docker Build and Push
* **Description**: This job builds a Docker image, performs vulnerability scanning, and pushes the image to the GitHub Container Registry.

### Update Kubernetes Deployment

* **Name**: Update Kubernetes Deployment
* **Description**: This job updates the Kubernetes deployment manifest with the new Docker image tag to trigger a deployment.

## Triggers

The workflow is triggered by the following events:

* `push` events to the `main` branch, excluding changes to the `kubernetes/deployment.yaml` file.
* `pull_request` events targeting the `main` branch.

## Usage

1.  **Set up GitHub Secrets**:
    * Create a personal access token with `write:packages` and `repo` permissions.
    * Add this token to your GitHub repository's secrets with the name `TOKEN`.
2.  **Configure Kubernetes Deployment Manifest**:
    * Ensure the `kubernetes/deployment.yaml` file in your repository contains the correct Docker image name and a tag placeholder. The workflow will automatically update the tag during the deployment process.
3.  **Define Build Artifacts**:
    * The Node.js build process must output the build artifacts to the `dist/` directory. This directory is then used to create the Docker image.
4.  **Define npm Scripts**:
    * The `package.json` file should contain the following npm scripts:
        * `test`:  Execute unit tests.
        * `lint`:  Run the code linter.
        * `build`:  Build the project.
