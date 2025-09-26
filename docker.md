# Docker Cheat Sheet

## Table of Contents
- [Installation & Setup](#installation--setup)
- [Basic Commands](#basic-commands)
- [Images](#images)
- [Containers](#containers)
- [Dockerfile](#dockerfile)
- [Docker Compose](#docker-compose)
- [Volumes](#volumes)
- [Networks](#networks)
- [Registry & Hub](#registry--hub)
- [System Management](#system-management)
- [Best Practices](#best-practices)
- [Troubleshooting](#troubleshooting)

## Installation & Setup

### Check Installation
```bash
# Check Docker version
docker --version
docker version

# Check Docker info
docker info

# Check Docker Compose version
docker-compose --version
```

### First Steps
```bash
# Test Docker installation
docker run hello-world

# Enable Docker to start on boot (Linux)
sudo systemctl enable docker
sudo systemctl start docker
```

## Basic Commands

### Getting Help
```bash
# Get help for Docker
docker --help

# Get help for specific command
docker run --help
docker build --help
```

### System Information
```bash
# Show Docker system information
docker info

# Show disk usage
docker system df

# Show events in real-time
docker events
```

## Images

### Managing Images
```bash
# List all images
docker images
docker image ls

# Search for images on Docker Hub
docker search <image-name>

# Pull image from registry
docker pull <image-name>
docker pull <image-name>:<tag>

# Remove image
docker rmi <image-id>
docker image rm <image-name>

# Remove unused images
docker image prune

# Remove all unused images
docker image prune -a
```

### Building Images
```bash
# Build image from Dockerfile
docker build -t <image-name> .

# Build with specific Dockerfile
docker build -f <dockerfile-path> -t <image-name> .

# Build with build arguments
docker build --build-arg ARG_NAME=value -t <image-name> .

# Build without cache
docker build --no-cache -t <image-name> .
```

### Image Information
```bash
# Show image history
docker history <image-name>

# Inspect image details
docker inspect <image-name>

# Show image layers
docker image inspect <image-name>
```

## Containers

### Running Containers
```bash
# Run container
docker run <image-name>

# Run container in background
docker run -d <image-name>

# Run container with custom name
docker run --name <container-name> <image-name>

# Run container with port mapping
docker run -p <host-port>:<container-port> <image-name>

# Run container with volume mount
docker run -v <host-path>:<container-path> <image-name>

# Run container with environment variables
docker run -e ENV_VAR=value <image-name>

# Run interactive container
docker run -it <image-name> /bin/bash
```

### Container Management
```bash
# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Stop container
docker stop <container-name>

# Start stopped container
docker start <container-name>

# Restart container
docker restart <container-name>

# Remove container
docker rm <container-name>

# Remove running container forcefully
docker rm -f <container-name>

# Remove all stopped containers
docker container prune
```

### Container Information
```bash
# Show container logs
docker logs <container-name>

# Follow logs in real-time
docker logs -f <container-name>

# Show last N lines of logs
docker logs --tail 50 <container-name>

# Inspect container details
docker inspect <container-name>

# Show container processes
docker top <container-name>

# Show container resource usage
docker stats <container-name>
```

### Executing Commands in Containers
```bash
# Execute command in running container
docker exec <container-name> <command>

# Execute interactive bash session
docker exec -it <container-name> /bin/bash

# Execute as specific user
docker exec -u <username> -it <container-name> /bin/bash
```

## Dockerfile

### Basic Dockerfile Structure
```dockerfile
# Use official base image
FROM node:16-alpine

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy application code
COPY . .

# Expose port
EXPOSE 3000

# Set environment variable
ENV NODE_ENV=production

# Create non-root user
RUN addgroup -g 1001 -S nodejs
RUN adduser -S nextjs -u 1001

# Change to non-root user
USER nextjs

# Define startup command
CMD ["npm", "start"]
```

### Common Dockerfile Instructions
```dockerfile
# Base image
FROM ubuntu:20.04

# Maintainer information
LABEL maintainer="your-email@example.com"

# Set working directory
WORKDIR /app

# Copy files
COPY source destination
ADD source destination  # Can also extract archives

# Run commands during build
RUN apt-get update && apt-get install -y python3

# Set environment variables
ENV PATH=/usr/local/bin:$PATH
ENV DEBUG=true

# Expose ports
EXPOSE 80 443

# Set user
USER 1000

# Volume mount point
VOLUME ["/data"]

# Entry point (not overridden by docker run)
ENTRYPOINT ["python3"]

# Default command (can be overridden)
CMD ["app.py"]

# Health check
HEALTHCHECK --interval=30s --timeout=3s --retries=3 \
  CMD curl -f http://localhost/ || exit 1
```

### Multi-stage Builds
```dockerfile
# Build stage
FROM node:16 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Production stage
FROM node:16-alpine AS production
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/package*.json ./
RUN npm install --only=production
CMD ["npm", "start"]
```

## Docker Compose

### Basic docker-compose.yml
```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=development
    volumes:
      - .:/app
      - /app/node_modules
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
    volumes:
      - postgres_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

volumes:
  postgres_data:

networks:
  default:
    external:
      name: my-network
```

### Docker Compose Commands
```bash
# Start services
docker-compose up

# Start services in background
docker-compose up -d

# Build and start services
docker-compose up --build

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v

# View logs
docker-compose logs

# Follow logs for specific service
docker-compose logs -f web

# Execute command in service
docker-compose exec web bash

# Scale service
docker-compose up --scale web=3

# View running services
docker-compose ps
```

## Volumes

### Volume Management
```bash
# Create volume
docker volume create <volume-name>

# List volumes
docker volume ls

# Inspect volume
docker volume inspect <volume-name>

# Remove volume
docker volume rm <volume-name>

# Remove unused volumes
docker volume prune
```

### Volume Types
```bash
# Named volume
docker run -v my-volume:/data <image-name>

# Bind mount (absolute path)
docker run -v /host/path:/container/path <image-name>

# Bind mount (relative path)
docker run -v $(pwd):/app <image-name>

# Tmpfs mount (in-memory)
docker run --tmpfs /tmp <image-name>
```

## Networks

### Network Management
```bash
# List networks
docker network ls

# Create network
docker network create <network-name>

# Create network with driver
docker network create -d bridge <network-name>

# Inspect network
docker network inspect <network-name>

# Connect container to network
docker network connect <network-name> <container-name>

# Disconnect container from network
docker network disconnect <network-name> <container-name>

# Remove network
docker network rm <network-name>

# Remove unused networks
docker network prune
```

### Running Containers with Custom Networks
```bash
# Run container with custom network
docker run --network <network-name> <image-name>

# Run container with network alias
docker run --network <network-name> --network-alias <alias> <image-name>
```

## Registry & Hub

### Docker Hub
```bash
# Login to Docker Hub
docker login

# Logout from Docker Hub
docker logout

# Tag image for Docker Hub
docker tag <image-name> <username>/<repository>:<tag>

# Push image to Docker Hub
docker push <username>/<repository>:<tag>

# Pull image from Docker Hub
docker pull <username>/<repository>:<tag>
```

### Private Registry
```bash
# Run local registry
docker run -d -p 5000:5000 --name registry registry:2

# Tag image for private registry
docker tag <image-name> localhost:5000/<image-name>

# Push to private registry
docker push localhost:5000/<image-name>

# Pull from private registry
docker pull localhost:5000/<image-name>
```

## System Management

### Cleanup Commands
```bash
# Remove all stopped containers, unused networks, images, and build cache
docker system prune

# Remove everything including volumes
docker system prune -a --volumes

# Remove unused containers
docker container prune

# Remove unused images
docker image prune

# Remove unused volumes
docker volume prune

# Remove unused networks
docker network prune
```

### Resource Management
```bash
# Set memory limit
docker run -m 512m <image-name>

# Set CPU limit
docker run --cpus="1.5" <image-name>

# Set CPU and memory limits
docker run -m 512m --cpus="1.0" <image-name>

# Show resource usage
docker stats

# Show resource usage for specific container
docker stats <container-name>
```

## Best Practices

### Dockerfile Best Practices
- Use official base images
- Use specific tags, avoid `latest`
- Minimize layers by combining RUN commands
- Use `.dockerignore` to exclude unnecessary files
- Run as non-root user when possible
- Use multi-stage builds for smaller images
- Order instructions from least to most frequently changing

### Security Best Practices
```dockerfile
# Use non-root user
RUN groupadd -r appuser && useradd -r -g appuser appuser
USER appuser

# Use specific versions
FROM node:16.14.0-alpine

# Scan for vulnerabilities
docker scan <image-name>
```

### Performance Tips
- Use `.dockerignore` file
- Leverage build cache
- Use small base images (Alpine Linux)
- Minimize image layers
- Use multi-stage builds
- Clean up package managers in same layer

### Sample .dockerignore
```dockerignore
node_modules
npm-debug.log
.git
.gitignore
README.md
.env
.nyc_output
coverage
.pytest_cache
```

## Troubleshooting

### Common Issues
```bash
# Container exits immediately
docker logs <container-name>

# Port already in use
docker ps -a  # Find container using the port
docker stop <container-name>

# Permission denied
sudo docker <command>  # Or add user to docker group

# Out of disk space
docker system prune -a

# Container can't connect to another container
docker network ls
docker network inspect bridge
```

### Debugging Containers
```bash
# Run container in interactive mode
docker run -it <image-name> /bin/sh

# Override entrypoint for debugging
docker run -it --entrypoint /bin/sh <image-name>

# Check container filesystem
docker exec -it <container-name> ls -la

# Check container environment
docker exec -it <container-name> env

# Copy files from container
docker cp <container-name>:/path/to/file ./local-file

# Copy files to container
docker cp ./local-file <container-name>:/path/to/file
```

### Performance Monitoring
```bash
# Monitor resource usage
docker stats

# Check container processes
docker exec <container-name> ps aux

# Check container disk usage
docker exec <container-name> df -h

# System events
docker events --filter container=<container-name>
```

---

*Remember: Docker can consume significant disk space. Regularly clean up unused containers, images, and volumes using `docker system prune`.*