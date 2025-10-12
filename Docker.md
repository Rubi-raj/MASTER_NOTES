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
| Command | Description | Example |
|--------|-------------|---------|
| `docker images`<br>`docker image ls` | List all Docker images | — |
| `docker ps` | List running containers | — |
| `docker pull {image}:{tag}` | Pull an image from a registry | `docker pull nginx:stable-alpine3.20-perl` |
| `docker run {image}:{tag}` | Run a container | `docker run nginx:stable-alpine3.20-perl` |
| `docker container prune` | Remove all stopped containers | — |
| `docker run -d {image}:{tag}` | Run container in background (detached mode) | `docker run -d nginx:stable-alpine3.20-perl` |
| `docker run -d {image}:{tag} --rm` | Run container in background and auto-remove on stop | — |
| `docker run -d -p {host}:{container} {image}:{tag} --name {name}` | Run container with port binding and custom name | `docker run -d -p 9000:80 nginx:latest` |
| `docker logs {container}` | View logs from container | `docker logs f2ec61281427` |
| `docker stop {container}` | Stop running container | — |
| `docker run -e {key1}={val1} -e {key2}={val2} {image}:{tag}` | Run container with environment variables | — |

---


