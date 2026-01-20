#### Step-1: Learn YAML
	- see the link for yaml concepts [[YAML Learning Concepts]]
#### Step-2: Learn Docker
##### Docker Supports
- Portable : sharing between different machines
- Lightweight: less overhead container(contains app + dependencies)
- Compatible: has disadvantage(docker image are linux based) where VM is compatible with any OS

##### Docker Concepts Theoretical
	1. What is virtualization?
	2. VM vs Docker - [[Docker vs VM]]
		- VM setups overall os(means separate kernel for each vm's)
		- Docker setup a container(OS independent kernel won't be tocuhed)
	3. Docker Image vs Docker Container
		- Docker Image: an executable file helps to create containers
		- Docker Container: an instance of a Docker Image
	4. Docker Commands - [[Docker Commands Learning]]
	5. Docker Compose - [[Docker Compose]]
	6. Docker Network - [[Docker Network]]
	7. Docker Volume - [[Docker Volume]]
	8. Docker Publication
		- Dockerfile: [[Docker Publishing Concepts]] 
		- Dockerhub or AWS ECR [[Docker Image Deployment]]
		- Github Container Registry
	9. Docker Swarm
	10. Docker Best Practices
		1. use specific image tags(version)
		2. combine run command with &&(stacked commands)
		3. using multi-stage builds
		4. do not run as root(instead use groups and users)
		5. scan images for vulnerabilities(docker scout)
	11. Docker Microservices: Container Orchestration
		1. Kubernetes
#### Step-3: Learn Kubernetes
#### Step-4: Learn Github Action
