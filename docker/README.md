## Docker
### Installation
- https://docs.docker.com/get-docker/
- `docker version`
- `docker info`

### Hola Mundo
`docker run hello-world`

### Contenedores
Un contenedor ejecuta sus procesos de forma nativa, como si fuera cualquier otro proceso de la maquina host, pero no puede ver los procesos de fuera del contenedor. De la misma forma, solo puede acceder a los recursos que se le han asignado, no sabrán si el host tiene más recursos. En cuanto al sistema de archivos, solamente puede ver a partir de su root, no más arriba.

### Comandos
- `docker run <IMAGE_NAME>` ejecuta un contenedor.
	- `docker run -it <IMAGE_NAME>` interactive with my shell.
	- `docker run <IMAGE_NAME> tail -f /dev/null` it execute the comand that we want, instead of default one. In this case tail -f "/dev/null" to get a infinite loop.
	- `docker run --name <CONTAINER_NAME> <IMAGE_NAME>` corremos IMAGE_NAME con el nombre CONTAINER_NAME en vez de un nombre al azar.
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



