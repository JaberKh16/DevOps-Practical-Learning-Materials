-  compose is a tool for defining and running multi-container applications
-  a file - .yml is created to handle all necessary information for docker container to 
	-setup a multi-container management in docker

File: compose.yml
version: "3.8"
services:
	mongo:
		image: mongo
		ports:
		- 27017:27017
		environment:
			MONGO_INITDB_ROOT_USERNAME: admin
			MONGO_INITDB_ROOT_PASSWORD: password
	mongo-express:
		image: mongo-express
		ports:
		-8080:8081
		environment:
			ME_CONFIG_MONGODB_ADMINUSERNAME: admin
			ME_CONFIG_MONGODB_ADMINPASSWORD: password
			ME_CONFIG_MONGODB_URL: mongodb://username:password@image_name:port 
			# mongodb://mongodb:password@mongo:27017


##### Setup A DB Image
1.  create an isolated network
	$ docker network create mongo-network
2. check the network
	$ docker network ls
3. setup the image and pull: mongo
	$ docker run -d \
	> -p 27017:27017 \
	> --name mongo \
	> --network mongo-network \
	> -e MONGO_INITDB_ROOT_USERNAME=admin \
	> -e MONGO_INITDB_ROOT_PASSWORD=password \
	> mongo

4. setup the image and pull: mongo-express
	$ docker run -d \
	> -p 8081:8081
	> --name mongo-express
	> --network mongo-network
	> -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
	> -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
	> -e ME_CONFIG_MONGODB_URL="mongodb://admin:password@mongo:27017" \
	> mongo-express 