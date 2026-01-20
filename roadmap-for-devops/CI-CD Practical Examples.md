Advanced CI/CD for Node.js — Enterprise Deep Dive

Topics Covered:

	Dockerized Node.js CI/CD
	Kubernetes Deployment Pipelines
	Blue-Green & Canary Deployments
	Monorepo Node.js Pipelines
	CI/CD Security Deep Dive

1. Dockerized Node.js CI/CD
	1.1 Why Docker in CI/CD?
		Docker solves environment drift.
		“It works on my machine” is eliminated.
	
	Benefits
		Immutable builds
		Same runtime across CI, staging, production
		Faster deployments
		Horizontal scalability
	
	1.2 Dockerized Node.js Architecture
		Developer
		   ↓
		Git Commit
		   ↓
		CI Pipeline
		   ↓
		Docker Build
		   ↓
		Docker Image
		   ↓
		Container Registry
		   ↓
		Server / Kubernetes
	
	1.3 Production-Grade Dockerfile (Node.js)
		
		FROM node:18-alpine AS base
		WORKDIR /app
		COPY package*.json ./
		RUN npm ci --only=production
		COPY . .
		EXPOSE 3000
		CMD ["node", "server.js"]
		Best Practices Used
		Alpine image (smaller attack surface)
		npm ci for deterministic installs
		No dev dependencies
		Single responsibility container
	
	1.4 GitHub Actions – Dockerized Pipeline
		name: Docker CI/CD
		
		on:
		  push:
		    branches: [ main ]
	
	jobs:
	  docker:
	    
	    runs-on: ubuntu-latest
	    steps:
	      - uses: actions/checkout@v4
	
	      - name: Build Docker image
	        run: docker build -t myorg/node-app:${{ github.sha }} .
	
	      - name: Push to registry
	        run: |
	          docker tag myorg/node-app:${{ github.sha }} 
	          myorg/node-app:latest
	          docker push myorg/node-app:latest
	
	1.5 Mental Model
		Source Code → Docker Image → Deployment
		You deploy images, not source code.

2. Kubernetes Deployment Pipelines
	2.1 Why Kubernetes?
		Kubernetes provides:
		Auto-healing
		Auto-scaling
		Rolling updates
		Zero-downtime deployments
	
	2.2 Kubernetes CI/CD Flow
		CI Pipeline
		   ↓
		Build Image
		   ↓
		Push to Registry
		   ↓
		kubectl / Helm
		   ↓
		Kubernetes Cluster
	
	2.3 Kubernetes Deployment YAML (Node.js)
		apiVersion: apps/v1
		kind: Deployment
		metadata:
		  name: node-app
		spec:
		  replicas: 3
		  selector:
		    matchLabels:
		      app: node-app
		  template:
		    metadata:
		      labels:
		        app: node-app
		    spec:
		      containers:
		        - name: node-app
		          image: myorg/node-app:latest
		          ports:
		            - containerPort: 3000
		
		2.4 Kubernetes Service
			apiVersion: v1
			kind: Service
			metadata:
			  name: node-app-service
			spec:
			  selector:
			    app: node-app
			  ports:
			    - port: 80
			      targetPort: 3000
		
		2.5 Rolling Update Flow (Graph)
			Old Pod v1 ──┐
			Old Pod v1 ──┼─→ Traffic
			New Pod v2 ──┼─→ Traffic
			New Pod v2 ──┘
		
		No downtime. Traffic shifts gradually.

2. Blue-Green & Canary Deployments

	3.1 Blue-Green Deployment
	
	Concept
		Two identical environments:
		Blue → current production
		Green → new version
	
	Blue-Green Flow
		Users
		  |
		  v
		Load Balancer
		  |
		  ├── Blue (v1)  ← ACTIVE
		  └── Green (v2) ← IDLE
	
	After validation:
	Load Balancer
	  |
	  ├── Blue (v1)  ← IDLE
	  └── Green (v2) ← ACTIVE
	
	Advantages
		Instant rollback
		Zero downtime
		Clean releases
		Drawback
		Double infrastructure cost
	
	3.2 Canary Deployment
		Concept
		Release to small subset of users first.
		
		Canary Flow
		100% Traffic
		   |
		   ├── 90% → v1
		   └── 10% → v2 (Canary)

If stable:
	100% → v2
	Canary Metrics
	Error rate
	Latency
	CPU usage

Business KPIs
	Kubernetes Canary Example
	Deployment v1: replicas=9
	Deployment v2: replicas=1

4. Monorepo Node.js Pipelines
	4.1 What Is a Monorepo?
	- A single repository containing multiple services.

		repo/
		├── services/
		│   ├── auth/
		│   ├── payments/
		│   └── users/
		├── package.json

	4.2 Challenges
		Long pipelines
		Unnecessary builds
		Dependency coupling
	
	4.3 Smart Monorepo CI Strategy
		Change Detection
		Git Diff
		  ↓
		Identify Changed Service
		  ↓
		Build Only That Service

	GitHub Actions Monorepo Example
	jobs:
	  detect:
	    runs-on: ubuntu-latest
	    outputs:
	      service: ${{ steps.filter.outputs.service }}
	    steps:
	      - uses: actions/checkout@v4
	      - uses: dorny/paths-filter@v3
	        id: filter
	        with:
	          filters: |
	            auth:
	              - 'services/auth/**'

	4.4 Monorepo Graph
		Commit
		  |
		  ├── auth changed → build auth
		  ├── payments unchanged → skip
		  └── users unchanged → skip

5. CI/CD Security Deep Dive (DevSecOps)
	5.1 Why CI/CD Security Matters
		Pipelines have access to:
		Source code
		Secrets
		Production credentials
		A compromised pipeline = total breach.
	
	5.2 CI/CD Threat Model
		Developer → CI → Registry → Prod
		     ↑         ↑        ↑
		  Code     Secrets   Image
	
	5.3 Security Layers (Defense in Depth)
		Layer 1: Source Code
		Layer 2: Dependencies
		Layer 3: Build Environment
		Layer 4: Artifacts
		Layer 5: Runtime
	
	5.4 Security Controls with Examples
	1. SAST (Static Analysis)
		`$ npm audit`

Detects vulnerable dependencies.

2. Dependency Locking
	package-lock.json
	Prevents supply-chain attacks.

3. Secrets Scanning
	TruffleHog
	GitHub Secret Scanning

4. Image Scanning
	trivy image myorg/node-app

5. Least Privilege

	CI tokens scoped
	
	No long-lived secrets
	
	Short-lived cloud credentials

	5.5 Secure CI/CD Pipeline Flow
		Commit
		  ↓
		SAST
		  ↓
		Dependency Scan
		  ↓
		Docker Scan
		  ↓
		Deploy
		
		Fail early, fail safely.

6. Final Unified Mental Model
	Code
	 ↓
	CI (Build + Test + Scan)
	 ↓
	Artifact (Docker Image)
	 ↓
	CD (Deploy Strategy)
	 ↓
	Kubernetes
	 ↓
	Observability + Rollback

7. Summary Table
	Area	Key Focus
	Docker CI/CD	Immutable builds
	Kubernetes	Orchestration
	Blue-Green	Zero downtime
	Canary	Risk reduction
	Monorepo	Selective pipelines
	Security	Trust & control
	
8. What I Can Provide Next
	
	Full Helm-based pipelines
	
	GitOps (ArgoCD / Flux) workflows
	
	Advanced Canary with Istio
	
	AWS / GCP / Azure CI/CD

End-to-end DevSecOps reference architecture