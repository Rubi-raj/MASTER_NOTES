# What is Docker ?
  Docker is a virtualization software, makes developing and deploying applications much easier.
## Docker Images Vs Containers
  Images are templates for containers.
### Docker Images
  - Executable application artifact
  - Any services (postgres, npm, node)
  - Environment variables, create directories, files etc.
### Docker Containers
  - A running instance of an image is a container.
  - Can run multiple containers from 1 image.
## Docker Registries
  - A storage and distribution system for Docker images.
  - Docker hosts one of the biggest Docker Registry, called “Docker Hub”.
---
# Docker Commands
| Command | Description |
|--------|-------------|
| `docker images` or `docker image ls` | List all Docker images |
| `docker ps` | List running containers |
| `docker pull {imageName}:{tag}` | Pull an image from a registry <br> _eg:-_ `docker pull nginx:stable-alpine3.20-perl`
| `docker run {imageName}:{tag}` | Run a container <br> _eg:-_ `docker run nginx:stable-alpine3.20-perl`|
| `docker container prune`|Remove all stopped containers|
| `docker run {imageName}:{tag}` | Run container | `docker run nginx:stable-alpine3.20-perl` |
| `docker logs {containerId/name}` | View logs from container | `docker logs nginx` |
| `docker stop {containerId/Name}` | Stop running container |
| `docker exec -it {containerId/Name} /bin/bash` | Open inside a container to debug |
---
# Docker Run Commands
```bash
docker run -d -p {hostPort}:{containerPort} -e {key}={value} --name {containerName} --rm {imageName}:{tag}
```
 - `-d` Run container in background and print container ID
 - `-p {hostPort}:{containerPort}` Publish a container's port to the host
 - `-e {key}={value}` Environment variable
 - `--name {containerName}` Assign a name to the container
 - `--rm` Delete the container once it stop
---
# Slim & Alphine Images
| Slim | Alphine |
|--------|-------------|
| Small image | Typically smaller image |
| Debian-based Linux | Alpine Linux |
---
# Docker Mounts
 - Volumes
 - Bind-mounts
 - Tempfs mounts <br>
`docker run -v {/path/in/host}:{/path/in/container} {imageName}:{tag}`
