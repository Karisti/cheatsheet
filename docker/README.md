## Docker<!-- omit in toc -->

## Index<!-- omit in toc -->
- [Installation](#installation)
- [What is Docker?](#what-is-docker)
- [What are containers?](#what-are-containers)
	- [Life cycle of a container](#life-cycle-of-a-container)
- [Dockerfile](#dockerfile)
- [Images](#images)
- [Containers](#containers)
	- [Networking](#networking)
	- [Data](#data)
		- [Bind mount](#bind-mount)
		- [Volumes](#volumes)
		- [tmpfs mount](#tmpfs-mount)
- [Docker compose](#docker-compose)
	- [Docker compose commands](#docker-compose-commands)
- [Other options](#other-options)
- [Resources](#resources)

------------

### Installation
- https://docs.docker.com/get-docker/
- `docker version`
- `docker info`
- Hello world test: `docker run hello-world`

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### What is Docker?
Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and deploy it as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code.

In a way, Docker is a bit like a virtual machine. But unlike a virtual machine, rather than creating a whole virtual operating system, Docker allows applications to use the same Linux kernel as the system that they're running on and only requires applications be shipped with things not already running on the host computer. This gives a significant performance boost and reduces the size of the application.

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### What are containers?
A container runs its processes natively, just like any other process on the host machine, but cannot see processes outside the container. In the same way, you can only access the resources that have been assigned to you, it will not know if the host has more resources. For the file system, you can only see from its root, not above.

First, we need a Dockerfile where we specify all the layers that the image is going to have when we build it. After that, we run the image to create de container.

**Dockerfile --build--> image --run--> container**

#### Life cycle of a container:
Normally as soon as the ubuntu is executed it turns off, unless we are connected in interactive mode. Whenever a container is executed, normally the bash is executed and since it has no command to execute, it ends. We can change the command to execute.

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### Dockerfile
We can specify how we want to be our image in this Dockerfile.
- `FROM <BASE_IMAGE>:<VERSION>` we indicate which base image to use.
- `RUN <COMMAND TO EXECUTE>` to execute commands when building the image.
- `COPY ["<BUILD_CONTEXT_PATH>", "<DEST_PATH>"]` to copy files from the build context to a dest on the image.
- `WORKDIR <DIRECTORY>` change working directory.
- `EXPOSE <PORT>` to expose port.
- `CMD ["<COMMAND>", "<COMMAND>"]` default command that will run if it is not specified.

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### Images
Images in Docker are built with layers. Each layer is one 'difference' with the previus one on the files.
- `docker build -t <TAG_NAME> <PATH_SRCS_FOR_BUILD_TIME>` to build image from Dockerfile. We indicate the tag with -t. The Docker daemon can use the files only from PATH on build time.
- `docker pull <IMAGE_NAME>` or `docker pull <IMAGE_NAME>:<VERSION>` pull image from Docker repository.
- `docker image ls` list images.
- `docker image rm <IMAGE_NAME>` remove image.
- `docker tag <PREVIOUS_TAG> <MY_USER>/<NEW TAG>` to rename image tag, so we can push to our Docker repository.
- `docker push <IMAGE_NAME>` or `docker push <IMAGE_NAME>:<VERSION>` to push image from to Docker repository.
- `docker history <IMAGE_NAME> OR <TAG_NAME>` to see how image was created.
	- `-- no-trunc` to avoid truncating output.
- `dive <IMAGE_NAME>` we can use Dive to see history better (https://github.com/wagoodman/dive).

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### Containers
- `docker run <FLAGS> <IMAGE_NAME>` runs container.
	- `-it` interactive with my shell.
	- `--mount src=<NAME_VOLUME> dst=</PATH/TO/DEST>` to use bind mounts.
	- `-p 8080:80` (publish) bound hosts port '8080' to containers port '80'.
	- `-d` (detach) if this has output, don´t show me.
	- `--name <CONTAINER_NAME>` we run IMAGE_NAME with the name CONTAINER_NAME instead of a random name.
	- `--env <NAME>=<ENVIROMENT_VARIABLE>` assign environment variable.
	- `--rm` deletes container when this ends.
- `docker run <IMAGE_NAME> tail -f /dev/null` it execute the comand that we want, instead of default one. In this case tail -f "/dev/null" to get a infinite loop.
	- `Tail`: returns to standard output the content of a file or directory.
	- `-f`: follow. Return what there is, and stay waiting for changes to keep returning.
	- `/dev/null`: everything that is carried here will disappear.

- `docker ps <FLAGS>` only shows running containers by default.
	- `-a` shows all containers.
	- `-aq` shows also quiet containers.
	- `-fea` view all system processes. By default the "root process" will have PID 1. When this term is the container it will be closed.
- `docker exec -it <CONTAINER_NAME> bash` executes command on running container.
- `docker kill <CONTAINER_NAME>` to stop container.
- `docker rm <CONTAINER_NAME>` to remove container.
	- `docker rm $(docker ps -aq)` and we remove quiet containers.
- `docker logs <CONTAINER_NAME>` to see the output of a container, even if this one is stopped.
- `docker rename <CONTAINER_NAME> <NEW_NAME>` cambiar nombre a un contenedor.
- `docker inspect <CONTAINER_ID or CONTAINER_NAME>` metadata sobre el estado del contenedor.
- `docker inspect -f '{{ json .Config.Env }}' <CONTAINER_ID or CONTAINER_NAME>` filtramos el resultado de inspect para obtener un valor concreto. En este caso el path del contenedor.

#### Networking
If two containers are connected to the same network, they can see each other using the name of the container as hostname.

##### Types of network
Three types of networks by default: bridge, host, none.
- **Bridge**: default network, or bridged network, was used with the 'link' instruction, which allowed to link containers across the network. However this network is deprecated.
- **Host**: Use this interface with caution. Allows the container to use the default network of the host machine. It is sensible that if the container opens any port, this is replicated on the host machine,  generating possible vulnerabilities.
- **None**: it is similar to /dev/null or black hole on unix systems. In this case it allows us to specify that the container has no exit or permission to access or be accessed by network.

##### Commands
- `docker network ls` list networks.
- `docker network create --attachable <NETWORK_NAME>` create network.
	- `--attachable` we allow other containers connection on the future.
- `docker network connect <NETWORK_NAME> <CONTAINER_NAME>` connects container to given network.
- `docker network inspect <NETWORK_NAME>` all the information about the network.

#### Data
Each container with the original image (from 0) when we run it, so if we need data persistence, we have to manage it. We need to mount directory we want from the host on the desired directory of the container.
##### Bind mount
- `-v /Host/directory:Container/directory` makes data persistence between indicated host directory and the directory inside the container. Changes from one side are reflected in the other, so it can be insecure, as external processes can have access.

##### Volumes
Stored place is managed by Docker, so external processes should not have access to this. Containers can create volumens by default.
- `docker volume create <NAME_VOLUME>` creates a volume. We can use it when running, with --mount.
- `docker volume ls` list volumes.
- `docker volume prume` deletes volumes that are not being used by some container.

##### tmpfs mount
Temporal file system. It works on memory, so when it stops its deleted. Very useful for security.

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### Docker compose
Describe declaratively the structure of our application to easily configure the whole image. It uses compose files in yml format. It creates a default network for all the services.

- `docker-compose up` to run.
- `docker-compose down` to clean.
- docker-compose ps` to clean.
- `docker-compose scale <SERVICE>=<NUM>` create 'NUM' containers. It can give problems with ports, we can solve it using a range on ports. For example: 3000-3010 instead of 3000.

docker-compose.yml example:
```
version:"3"

services:
<ONE_NAME>:
  	image: <IMAGE_NAME>
	environment:
		<NAME>:<ENV_VARIABLE>
	depends_on:
		- <DEPENDENCY_NAME>
	ports:
		- "<HOST_PORT>:<CONTAINER_PORT>"
	volumes:
		- <HOST_PATH>:<CONTAINER_PATH>
		- <DONT_TOUCH_HOST_PATH>
	
<DEPENDENCY_NAME>:
    image: <IMAGE_NAME>
```
#### Docker compose commands
Are similar to the other docker commands:
- `docker-compose up -d`
- `docker-compose ps`
- `docker-compose logs <SERVICE_NAME>`
- `docker-compose exec <SERVICE_NAME> <COMMAND>`

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### Other options
- Like on Git, also exists an `.dockerignore` file, to specify files and directories that we don't want to build.
- Docker also has multi-stage builds. You can use Docker to have a development build and a production build, run tests before putting it into production, etc.
- We can use 'Docker in Docker' concept to run a Docker inside another Docker, for continuous integration for example. You can have a container that has the Docker client, and that speaks to the docker daemon of the host machine, but they won't be able to touch the rest of the machine.

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>

### Resources
- [Docker Hub](https://hub.docker.com/)
- [Docker For The Absolute Beginner](https://www.kodekloud.com/p/docker-for-the-absolute-beginner-hands-on)
- [Learn Docker in 12 Minutes 🐳](https://www.youtube.com/watch?v=YFl2mCHdv24)
- [How to Docker](https://jonnylangefeld.github.io/learning/Docker/How%2Bto%2BDocker.html)
- [What-docker](https://opensource.com/resources/what-docker)
- [Fundamentos de Docker - Platzi](https://platzi.com/clases/docker/)

<div align="right">
  <small><a href="#Docker">🡡 Go to Index</a></small>
</div>
