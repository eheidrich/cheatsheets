# Docker Commands Cheat Sheet

## Basic Container Management

- `docker ps`  
  List all running containers.

- `docker ps -a`  
  List all containers, including those not currently running.

- `docker images`  
  List all locally installed images.

- `docker create <image>`  
  Create a container from an image but do not start it.

- `docker start <container id>`  
  Start a container.

- `docker stop <container id>`  
  Stop a container.

- `docker pause <container id>`  
  Pause a container.

- `docker unpause <container id>`  
  Resume a paused container.

## Running and Managing Containers

- `docker run ...`  
  Run a command in a container. Downloads the image from Docker Hub if it's not available locally. Options include:
  - `-t` for a terminal.
  - `-i` for interaction with the container.
  - `-d` detached, to not lock the terminal.
  - `-e VALOR=value` to pass environment variables to the container.
  - `-p hostport:containerport` to define port communication.
  - `--name <name>` to name the container.
  - `--volume-from <container name>` to use a volume defined in another container.
  - `-m / --memory 512m` to limit memory.
  - `-c / --cpu-shares 1024` to set CPU usage quota.
  - `-v /volume` to create a volume folder at root, or `-v /localpath:/containerpath` to map a local file to the container.
  
  Example: `docker run -ti ubuntu /bin/bash` starts an Ubuntu image with the bash terminal. Downloads the image if it's not available.

  When in a Linux terminal:
  - Ctrl + D exits the terminal and stops the container.
  - Ctrl + PQ exits the terminal but keeps the container running.

- `docker attach <container id>`  
  Connect to a running container. For example, connect directly to the terminal if it's running Linux.

## Updating and Inspecting

- `docker update ...`  
  Update settings of a running container.
  - `-m / --memory 256m` to update memory limit.
  - `-c / --cpu-shares 1024` to update CPU usage quota.

- `docker tag <image id> <name:tag>`  
  Update the name and version (tag) of an image.

- `docker inspect <container id/image/image:version>`  
  Show details of a container or image, like ports, IP, memory limit, CPU, etc.
  - `-f {{.Mounts}}` to show the volume location.

## Monitoring and Logs

- `docker stats <container id>`  
  Show resource usage statistics of a container.

- `docker top <container id>`  
  Show running processes in a container.

- `docker logs <container id>`  
  Show container logs, listing all commands run in bash for Linux containers.

## Cleaning Up

- `docker rm <container id>`  
  Delete a container. Must not be running. Use `-f` to force removal of a running container.

- `docker rmi <image id or name:tag>`  
  Remove an image from the computer.
  - `-f` to force removal, even if a container is using it.

## Building and Pushing Images

- `docker build .`  
  Build an image based on the Dockerfile in the current directory. Always point to the directory, not the file.
  - `-t` to define the image name and tag in the format `<name>:<tag>`.

- `docker history <container id/image/image:version>`  
  Show the history of a container or image.

- `docker login`  
  Log in to Docker Hub.

- `docker push <image id or name:tag>`  
  Upload your created image to Docker Hub. Images created by you need to be named with your Docker Hub username/name.

- `docker search <username>`  
  List images from a user on Docker Hub.

## Executing Commands in Containers

- `docker exec`  
  Execute a command in a running container.  
  Example: `docker exec -it <container id> bash` to open a bash shell in the container.

## Image Repository Management

- `docker pull <image>`  
  Pull an image or a repository from a registry.  
  Example: `docker pull ubuntu` to download the latest Ubuntu image.

- `docker push <image:tag>`  
  Push an image or a repository to a registry.  
  Example: `docker push myimage:tag` to push your custom image to Docker Hub.

## Volume Management

- `docker volume`  
  Manage Docker volumes.  
  Subcommands:
  - `create`: Create a volume.
  - `inspect`: Display detailed information on one or more volumes.
  - `ls`: List volumes.
  - `rm`: Remove one or more volumes.

## Networking

- `docker network`  
  Manage networks in Docker.  
  Subcommands:
  - `create`: Create a network.
  - `connect`: Connect a container to a network.
  - `ls`: List networks.
  - `rm`: Remove one or more networks.

## Docker Compose

- `docker-compose up`  
  Build and start containers as defined in `docker-compose.yml`.

- `docker-compose down`  
  Stop and remove containers and networks created by `up`.

- `docker-compose build`  
  Build or rebuild services in `docker-compose.yml`.

## Copying Files

- `docker cp <containerId>:/file/path/within/container /host/path/target`  
  Copy files/folders between a container and the local filesystem.

## Login/Logout

- `docker login`  
  Log in to a Docker registry server.  
  Example: `docker login` to log in to Docker Hub.

- `docker logout`  
  Log out from a Docker registry server.
