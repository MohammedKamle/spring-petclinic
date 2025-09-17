# Spring Pet Clinic CI/CD Pipeline

## Overview

This repository demonstrates an end-to-end CI/CD pipeline for the Spring Pet Clinic application. The pipeline automates the process of building, testing, containerizing, and deploying the application using GitHub Actions, Docker, and JFrog Artifactory.

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:

- [Docker](https://www.docker.com/get-started)
- [Git](https://git-scm.com/)
- [Maven](https://maven.apache.org/)
- [Java 11 or higher](https://adoptopenjdk.net/)
- [GitHub CLI](https://cli.github.com/) (optional, for interacting with GitHub from the terminal)

### Clone the Repository

```bash
git clone https://github.com/MohammedKamle/spring-petclinic.git
cd spring-petclinic
```

## 🛠️ Building and Running Locally

### Using Maven

To compile and run the application locally:

```bash
./mvnw spring-boot:run
```

Access the application at `http://localhost:8080`.

### Using Docker

To build and run the application using Docker, this utilizes the `Dockerfile` attched in this repo:

```bash
docker build -t spring-petclinic .
docker run -p 8080:8080 spring-petclinic
```

## 🧪 CI/CD Pipeline with GitHub Actions

The GitHub Actions workflow automates the following steps:

1. **Compile the Code**: Ensures the application builds successfully
2. **Run Tests**: Executes unit and integration tests to validate the application
3. **Build Docker Image**: Creates a Docker image of the application
4. **Publish to JFrog Artifactory**: Pushes the Docker image to JFrog Artifactory
5. **Scan with JFrog XRay**: Scans the Docker image for vulnerabilities

### Workflow Configuration

The workflow is defined in `.github/workflows/ci-pipeline.yml`. Key steps include:

- **Set up JDK 17**: Configures the Java Development Kit
- **Cache Maven Dependencies**: Speeds up the build process by caching dependencies
- **Build and Test**: Compiles the code and runs tests
- **Docker Build and Push**: Builds the Docker image and pushes it to JFrog Artifactory
- **XRay Scan**: Scans the Docker image for vulnerabilities

### JFrog Credentials

Store your JFrog credentials as GitHub Secrets:

- `JFROG_REGISTRY`: Your JFrog Registry URL
- `JFROG_USERNAME`: Your JFrog username
- `JFROG_ACCESS_TOKEN`: Your JFrog access token

## 📦 Dockerfile

The Dockerfile in the root directory defines how the application is containerized. It uses the OpenJDK 17 base image, copies the built JAR file into the container, and sets the entry point to run the application.

## 🔍 JFrog XRay Scan Data

After pushing the Docker image to JFrog Artifactory, scan it using JFrog XRay:

1. Navigate to the JFrog XRay dashboard
2. Locate the scanned Docker image
3. Export the scan results as a JSON file

The exported JSON file contains detailed information about any vulnerabilities found in the image. This repo also has a sample Xray report json in `Xray results`

## 📄 GitHub Actions Workflow File

The GitHub Actions workflow files is located at `.github/workflows/`. It defines the steps for the CI/CD pipeline, including setting up the environment, building the application, running tests, building the Docker image, pushing it to JFrog Artifactory, and scanning it with JFrog XRay.


## 🖥️ Pull and Run Docker Image from JFrog Artifactory

If you wish to pull the Docker image from JFrog Artifactory and run it, use the following commands:

### Pull the Docker Image

```bash
docker pull trialxtslf6.jfrog.io/mdk-docker-local/spring-petclinic:149c720fea6729860573b6ca97c46dfbe321f909
```

### Run the Docker Image

```bash
docker run -p 8080:8080 trialxtslf6.jfrog.io/mdk-docker-local/spring-petclinic:149c720fea6729860573b6ca97c46dfbe321f909
```

This will start the Spring Pet Clinic application, and you can access it at `http://localhost:8080`.
