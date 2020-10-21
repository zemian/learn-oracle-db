## Docker for mac

1. Install Docker Engine for Mac
2. https://docs.docker.com/get-started/

	docker --version
	docker run hello-world

	docker run -it alpine

	# List of images you have downloaded
	docker image ls


## Docker image sizes

	zedeng-mac:~ zedeng$ docker images
	REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
	archlinux           latest              c24fe13d37b9        3 days ago          412MB
	postgres            latest              0f10374e5170        2 weeks ago         314MB
	oraclelinux         latest              48a0b88bcf77        5 days ago          235MB
	nginx               latest              602e111c06b6        2 weeks ago         127MB
	debian              latest              3de0e2c97e5c        2 weeks ago         114MB
	ubuntu              latest              1d622ef86b13        2 weeks ago         73.9MB
	alpine              latest              f70734b6a266        2 weeks ago         5.61MB
	hello-world         latest              fce289e99eb9        16 months ago       1.84kB

NOTE: Both postgres and nginx are based on debian image.


## Docker postgres server

	docker run -it -p 5432:5432 -e POSTGRES_PASSWORD=Postgres1 postgres

	# On another terminal, run
	psql -h localhost -U postgres


## Docker nginx server

Engine X HTTP server

	cd $HOME
	echo 'hello' > index.html
	docker run -v $HOME:/usr/share/nginx/html -p 8080:80 nginx

	# NOTE The above command will not output anything! You need to open a browser to test.
	open http://localhost:8080


## Running Docker as background process

	docker run -it -d alpine


To attach to the bg process:

	docker container attach <name>

To detach without exiting the container:

	CTRL+p, CTRL+q


## Docker Network

Look for "Containers" in for IP address:

	docker run -it -d -name alpine1 alpine
	docker run -it -d -name alpine2 alpine
	docker network inspect bridge

We cannot use container name as hostname to resolve to IP address when using defualt 'bridge' network.

To learn more about user custom-network:

https://docs.docker.com/network/network-tutorial-standalone/#use-the-default-bridge-network

	docker network create --driver bridge alpine-net
	docker network connect bridge alpine4
	docker network connect alpine-net alpine4

We can use container name as hostname to resolve to IP address when using user custom network.

But for container that connected to multiple network, you need to use IP address again.


## Remove unused containers

	docker container stop alpine1 alpine2
	docker container rm alpine1 alpine2
	docker container prune


## Docker Storage and Disk Volumes

https://docs.docker.com/storage/volumes/

Use -v or --mount options. (The -v is more compact syntax, while --mount is verbose.)

	
	docker run --mount source=nginx-vol,destination=/usr/share/nginx/html,readonly nginx:latest

 	docker run -v nginx-vol:/usr/share/nginx/html:ro nginx:latest


## Docker Service

Docker Swarm orchestrator - managing multiple nodes to run multiple containers.

https://docs.docker.com/engine/reference/commandline/service/


## Docker Compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. 

https://docs.docker.com/compose/

