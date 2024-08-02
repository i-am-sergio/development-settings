# GitHub Actions CI/CD Documentation

## Introduction

GitHub Actions is a powerful feature that allows you to automate workflows directly in your GitHub repositories. This documentation provides a guide to setting up GitHub Actions for Continuous Integration (CI) and Continuous Deployment (CD).

## Prerequisites

1. **GitHub Account:** Ensure you have a GitHub account and access to your repository.
2. **Repository:** Your source code should be hosted in a GitHub repository.

## Setting Up GitHub Actions

### 1. Creating a Workflow File

1. **Navigate to GitHub Repository:**
   - Go to your GitHub repository where you want to set up CI/CD.

2. **Create a `.github` Directory:**
   - In the root of your repository, create a directory named `.github` if it doesn't already exist.

3. **Create a `workflows` Directory:**
   - Inside the `.github` directory, create a directory named `workflows`.

4. **Add a Workflow YAML File:**
   - Inside the `workflows` directory, create a YAML file for your workflow, such as `ci-cd.yml`.

### 2. Defining Your Workflow

A GitHub Actions workflow is defined in a YAML file. Here is an example of a basic CI/CD workflow:

#### Example Workflow: `ci-cd.yml`

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout Code
      uses: actions/checkout@v3
      
    - name: Set up Java
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        
    - name: Build with Maven
      run: mvn clean install

  test:
    runs-on: ubuntu-latest
    needs: build
    
    steps:
    - name: Checkout Code
      uses: actions/checkout@v3
      
    - name: Set up Java
      uses: actions/setup-java@v3
      with:
        java-version: '11'
        
    - name: Run Tests
      run: mvn test

  deploy:
    runs-on: ubuntu-latest
    needs: test
    
    steps:
    - name: Checkout Code
      uses: actions/checkout@v3
      
    - name: Deploy Application
      run: ./deploy.sh
      env:
        DEPLOYMENT_KEY: ${{ secrets.DEPLOYMENT_KEY }}
```

### 3. Workflow Breakdown

- **Triggers:**
  - `on: push`: Triggers the workflow when code is pushed to the `main` branch.
  - `on: pull_request`: Triggers the workflow for pull requests targeting the `main` branch.

- **Jobs:**
  - **Build Job:** Runs on an Ubuntu runner, checks out the code, sets up Java, and builds the application using Maven.
  - **Test Job:** Runs after the build job, checks out the code, sets up Java, and runs tests.
  - **Deploy Job:** Runs after the test job, checks out the code, and executes a deployment script. The deployment key is accessed from GitHub Secrets.

### 4. Configuring Secrets

1. **Add Secrets to Your Repository:**
   - Go to the repository settings.
   - Select "Secrets and variables" > "Actions".
   - Click "New repository secret" and add secrets like `DEPLOYMENT_KEY`.

### 5. Monitoring and Managing Workflows

1. **Monitor Workflow Runs:**
   - Navigate to the "Actions" tab in your GitHub repository to view the status and logs of workflow runs.

2. **Manage Workflow Files:**
   - Update or add new workflow files as needed for different CI/CD tasks.


For more detailed information, refer to the [GitHub Actions documentation](https://docs.github.com/en/actions).
