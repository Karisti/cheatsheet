## Docker
### Installation
- https://docs.docker.com/get-docker/
- `docker version`
- `docker info`

### Hello world
`docker run hello-world`

### Containers
Un contenedor ejecuta sus procesos de forma nativa, como si fuera cualquier otro proceso de la maquina host, pero no puede ver los procesos de fuera del contenedor. De la misma forma, solo puede acceder a los recursos que se le han asignado, no sabrán si el host tiene más recursos. En cuanto al sistema de archivos, solamente puede ver a partir de su root, no más arriba.

### Basic commands
- `docker run <IMAGE_NAME>` ejecuta un contenedor.
	- `docker run -it <IMAGE_NAME>` interactive with my shell.
	- `docker run --mount src=<NAME_VOLUME> dst=</PATH/TO/DEST> <IMAGE_NAME>` interactive with my shell.
	- `-p 8080:80` (publish) bound hosts port '8080' to containers port '80'.
	- `docker run -d <IMAGE_NAME>` (detach) if this has output, don´t show me.
	- `docker run <IMAGE_NAME> tail -f /dev/null` it execute the comand that we want, instead of default one. In this case tail -f "/dev/null" to get a infinite loop.
	- `docker run --name <CONTAINER_NAME> <IMAGE_NAME>` corremos IMAGE_NAME con el nombre CONTAINER_NAME en vez de un nombre al azar.
	- `-env <NAME>=<ENVIROMENT_VARIABLE>` assign environment variable.
	- `docker run --rm <IMAGE_NAME>` deletes container when this ends.
	
- `docker ps` only shows running containers by default.
	- `docker ps -a` shows all containers.
	- `docker ps -aq` shows quiet containers.
- `docker exec -it <CONTAINER_NAME> bash` executes command on running container.
- `docker kill <CONTAINER_NAME>` to stop container.
- `docker rm <CONTAINER_NAME>` to remove container.
	- `docker rm $(docker ps -aq)` and we remove quiet containers.
- `docker logs <CONTAINER_NAME>` to see the output of a container, even if this one is stopped.
- `docker rename <CONTAINER_NAME> <NEW_NAME>` cambiar nombre a un contenedor.
- `docker inspect <CONTAINER_ID or CONTAINER_NAME>` metadata sobre el estado del contenedor.
- `docker inspect -f '{{ json .Config.Env }}' <CONTAINER_ID or CONTAINER_NAME>` filtramos el resultado de inspect para obtener un valor concreto. En este caso el path del contenedor.

### Networking
Three types of networks by default: bridge, host, none.
- `docker network ls` list networks.
- `docker network create --attachable <NETWORK_NAME>` list networks. Attachable: we allow other containers connection on the future.
- `docker network connect <NETWORK_NAME> <CONTAINER_NAME>` connects container to given network.
- `docker network inspect <NETWORK_NAME>` all the information about the network.

### Data
Each container with the original image (from 0) when we run it, so if we need data persistence, we have to manage it. We need to mount directory we want from the host on the desired directory of the container.
#### Bind mount
- `-v /Host/directory:Container/directory` makes data persistence between indicated host directory and the directory inside the container. Changes from one side are reflected in the other, so it can be insecure, as external processes can have access.

#### Volume
Stored place is managed by Docker, so external processes should not have access to this. Containers can create volumens by default.
- `docker volume create <NAME_VOLUME>` creates a volume. We can use it when running, with --mount.
- `docker volume ls` list volumes.
- `docker volume prume` deletes volumes that are not being used by some container.

#### tmpfs mount
Temporal file system. It works on memory, so when it stops its deleted. Very useful for security.

### Images
Images in Docker are built with layers. Each layer is one 'difference' with the previus one on the files.
- `docker pull <IMAGE_NAME>` or `docker pull <IMAGE_NAME>:<VERSION>` pull image from Docker repository.
- `docker image ls` list images.
- `docker build -t <TAG_NAME> <PATH>` to build image from Dockerfile. We indicate the tag with -t. The Docker daemon can use the files only from PATH on build time.
- `docker tag <PREVIOUS_TAG> <MY_USER>/<NEW TAG>` to rename image tag, so we can push to our Docker repository.
- `docker push <IMAGE_NAME>` or `docker push <IMAGE_NAME>:<VERSION>` to push image from to Docker repository.
- `docker history <IMAGE_NAME>` to see how image was created.
	- `-- no-trunc` to avoid truncating output.
- `dive <IMAGE_NAME>` we can use Dive to see history better (https://github.com/wagoodman/dive).

### Dockerfile
We can specify how we want to be our image in this Dockerfile.
- `FROM <BASE_IMAGE>:<VERSION>` we indicate which base image to use.
- `RUN <COMMAND TO EXECUTE>` to execute commands when building the image.
- `COPY ["<BUILD_CONTEXT_PATH>", "<DEST_PATH>"]` to copy files from the build context to a dest on the image.
- `WORKDIR <DIRECTORY>` change working directory.
- `EXPOSE <PORT>` to expose port.
- `CMD ["<COMMAND>", "<COMMAND>"]` default command that will run if it is not specified.

### Docker compose
Describe declaratively the structure of our application. It uses compose files in yml format. It creates a default network for all the services.

`docker-compose up` to run.
`docker-compose down` to clean.

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
		- "<HOST_PORT>:<CONTAINER_PORT>
	
<DEPENDENCY_NAME>:
    image: <IMAGE_NAME>
```
#### Docker compose commands
Are similar to the other docker commands:
- `docker-compose up -d`
- `docker-compose ps`
- `docker-compose logs <SERVICE_NAME>`
- `docker-compose exec <SERVICE_NAME> <COMMAND>`
