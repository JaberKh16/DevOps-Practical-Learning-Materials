Real-World CI/CD Setup for a Node.js Application

Tools: GitHub Actions, Jenkins  
App Type: Node.js REST API (Express-style)

1.  Reference Application Assumptions

To keep the example realistic, we assume:

Node.js version: 18 LTS

Package manager: npm

App entry: server.js

Tests: npm test

Build step (optional): npm run build

Deployment target:

VM / server with Node.js installed

App managed via PM2

Repository structure:

.  
├── server.js  
├── package.json  
├── package-lock.json  
├── test/  
├── .env.example  
├── ecosystem.config.js  PM2 config  
└── ci/

2.  GitHub Actions — Real-Life CI/CD Setup  
    2.1 Workflow Goals

This pipeline will:

Trigger on push to main

Install dependencies

Run tests

Build application

Deploy to production server via SSH

2.2 Required GitHub Secrets

Configured in Repo → Settings → Secrets → Actions:

Secret Name Purpose  
SSH\HOST Server IP / hostname  
SSH\USER SSH user  
SSH\KEY Private SSH key  
APP\PATH Remote app directory  
2.3 GitHub Actions Workflow

File:

.github/workflows/nodejs-ci-cd.yml

name: Node.js CI/CD Pipeline

on:  
push:  
branches:  
\- main

jobs:  
build-test-deploy:  
runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@v4
    
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: 18
          cache: 'npm'
    
      - name: Install dependencies
        run: npm ci
    
      - name: Run tests
        run: npm test
    
      - name: Build application
        run: npm run build --if-present
    
      - name: Deploy to production server
        uses: appleboy/ssh-action@v1
        with:
          host: ${{ secrets.SSHHOST }}
          username: ${{ secrets.SSHUSER }}
          key: ${{ secrets.SSHKEY }}
          script: |
            cd ${{ secrets.APPPATH }}
            git pull origin main
            npm ci --production
            pm2 reload ecosystem.config.js --env production
    

2.4 What Happens in Reality

Every push to main triggers deployment

Code is tested before deployment

Production server always runs tested code

No manual intervention required

2.5 Why This Is Production-Grade

Uses npm ci for deterministic installs

Secrets never exposed

Build happens before deploy

Idempotent deployment via PM2

3.  Jenkins — Real-Life CI/CD Setup  
    3.1 Jenkins Infrastructure Setup  
    Required Components

Jenkins server (VM or container)

Node.js installed on agent

Git plugin

NodeJS plugin

SSH credentials configured

3.2 Jenkins Credentials Setup

In Manage Jenkins → Credentials:

ID Type  
prod-ssh SSH Username with Private Key  
github-token GitHub access token  
3.3 Node.js Tool Configuration

Manage Jenkins → Global Tool Configuration

Name: node18

Version: NodeJS 18.x

Auto-install: Enabled

3.4 Jenkins Pipeline (Declarative)

File:

Jenkinsfile

pipeline {  
agent any

    tools {
        nodejs 'node18'
    }
    
    environment {
        APPDIR = '/var/www/node-app'
        NODEENV = 'production'
    }
    
    stages {
    
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'github-token',
                    url: 'https://github.com/your-org/node-app.git'
            }
        }
    
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }
    
        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }
    
        stage('Build') {
            steps {
                sh 'npm run build || true'
            }
        }
    
        stage('Deploy') {
            steps {
                sshagent(credentials: ['prod-ssh']) {
                    sh """
                      ssh user@server-ip '
                        cd ${APPDIR} &&
                        git pull origin main &&
                        npm ci --production &&
                        pm2 reload ecosystem.config.js --env production
                      '
                    """
                }
            }
        }
    }
    
    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Pipeline failed'
        }
    }
    

}

3.5 What Jenkins Does Differently

Persistent workspace

Long-running agents

Centralized orchestration

Greater control over environment

4.  GitHub Actions vs Jenkins — Real Usage Comparison  
    Area GitHub Actions Jenkins  
    Setup Time Minutes Hours  
    Maintenance None High  
    Cost Usage-based Infra cost  
    Flexibility Moderate Very High  
    On-Prem Support Limited Excellent  
    Security Control Managed Full control
5.  Production Hardening (Recommended)

For both systems:

Use environment-specific branches

Add linting stage

Add security scans (npm audit, Snyk)

Add manual approval before production

Store secrets in Vault (enterprise)

Enable pipeline notifications (Slack / Email)

6.  Mental Model (Final)

CI ensures correctness.  
CD ensures repeatability.  
Automation ensures trust.

GitHub Actions is ideal for modern, cloud-native workflows.  
Jenkins excels in enterprise, hybrid, and regulated environments.