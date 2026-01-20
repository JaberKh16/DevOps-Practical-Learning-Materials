#### a. Docker Run and Stop Commands
	1. to start the container
		 $ docker start container_name
	2. to stop the contianer
		$ docker stop container_name # via container_name
		$ docker stop container_id   # via container_id
	 3. to see the stats
		 $ docker stats container_name

#### b. Docker Pull Image and Run
	1. pull the image
		$ docker pull centos  # here centos is the image name
	2. run the container: 
		a. via specifying container and image name
			$ docker run -d -t --name  container_name image_name  
		b. via specifying container id - provides container id
			$ docker run -d image_name   # run image in -d(detached mode)
		c. default run without any container specified
			$ docker run image_name
		d. run with exec mode: -it(interactive mode)
			$ docker run exec -it image_name /bin/bash  
	3. to remove images/container
		a. remove image
			$ docker rmi image_name
		b. remove container
			$ docker rm container_name/container_id
#### c. Docker Container and Image List

	1. to see the running containers
		$ docker ps 
		$ docker ps ls
	2. to see the running images
		$ docker images
	3. to see all running and non-running containers
		$ docker ps -a

#### d. Docker With Port Binding
	- concepts of binding local(host) port with the container port
	- syntax:  -p local_port:host_port

	1. port binding command
		$ docker run -d -p 8080:8081 nginx

#### e. Docker Logs Commands
	1. to check logs 
		$ docker logs container_id

#### f. Docker Network Commands
	1. to check available networks
		$ docker network ls
	2. to remove a network
		$ docker network rm network_name
	3. to create a network
		$ docker network create network_name
	4. to inspect the network
		$ docker network inspect network_name
	5. to connect to network while run image
		$ docker run --network network_name image_name
	6. to connect a container to specific network
		$ docker network connect network_name container_name
	7. to disconnect a container from a specified network
		$ docker network disconnect network_name container_name

#### g. Docker Compose Commands
	1. to up the compose
		$ docker compose -f filename.yml
	2. to down the compose
		$ docker compose -f filename.yml down
	3. to create a specific service included in the docker-compose.yml file
		$ docker compose run service_name
	4. to build the image
		$ docker compose build
	5. to stop and remove the volumns
		$ docker compose down --volumes
	6. to stop and removes all current compose containers and any orphans
		$ docker compose down --remove-orphans
	7. to stop compose, remove volumes and orphans
		$ docker compose down --volumes --remove-orphans
	8. to stop the compose
		$ docker compose stop
	9. to check compose related containers
		$ docker compose ps
		$ docker compose ps -a
		