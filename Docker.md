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
| `docker run -d {imageName}:{tag}` | `-d` Run container in background (detached mode) <br> _eg:-_ `docker run -d nginx:stable-alpine3.20-perl`|
| `docker run {imageName}:{tag} --rm` | `--rm` Delete the container once it stop |
| `docker run {imageName}:{tag} --name {containerName}` | `--name {containerName}` To Name a container otherwise it creates own name.
| `docker run -p {hostPort}:{containerPort} {imageName}:{tag}` | `-p {hostPort}:{containerPort}` Run container with port binding and <br> _eg:-_ `docker run -d -p 9000:80 nginx:latest`|
| `docker run -d -p {hostPort}:{containerPort} {imageName}:{tag} --name {containerName}` | Run container with port binding and custom name <br> _eg:-_ `docker run -d -p 9000:80 nginx:latest`|
| `docker logs {containerId/name}` | View logs from container | `docker logs nginx` |
| `docker stop {containerId/Name}` | Stop running container |
| `docker run -e {key1}={val1} -e {key2}={val2} {image}:{tag}` | Run container with environment variables |

---

# Docker Run Commands
	```bash
	docker run -p {hostPort}:{containerPort} \
		-d -e {key1}={val1} -e {key2}={val2} {image}:{tag} \
		```
