# Docker
# Docker Zero to Hero - Day 24 Summary

## Overview
This is Day 24 of a complete DevOps course focusing on Docker fundamentals. The instructor (Abhishek) covers Docker basics, from understanding containers to creating and sharing your first Docker image.

---

## Key Topics Covered

### 1. *Why Containers are Lightweight*
- *Virtual Machines* have a complete guest OS (heavy, ~2.3 GB for Ubuntu)
- *Containers* only include:
  - Application code
  - Application dependencies
  - Minimal system dependencies for isolation
  - Share kernel and critical resources from host OS
- *Example**: Official Ubuntu Docker image is only **28.16 MB* vs 2.3 GB for VM

*Files/Folders in Containers:*
- `/bin` - binary execution files
- `/sbin` - system binaries
- `/etc` - configuration files
- `/lib` - library files
- `/usr` - user-related files
- `/var` - log files
- `/root` - root user home directory

*Shared from Host OS:*
- Host file system
- Networking stack
- System calls
- Namespaces
- Control groups (cgroups)
- Kernel resources

---

### 2. *Docker Architecture*

*Components:*
- *Docker Client* - CLI tool for user commands
- *Docker Daemon* - Heart of Docker, listens to API requests and manages containers
- *Docker Registry* - Storage for Docker images (Docker Hub, private registries)

*Workflow:*
```
Docker CLI → Docker Daemon → Creates Images/Containers → Push to Registry
```

---

### 3. *Docker Lifecycle*

1. *Write Dockerfile* - Set of instructions for building image
2. *Build Image* - `docker build` command creates Docker image
3. *Run Container* - `docker run` command executes the image
4. *Share* - Push to registry for others to use

---

### 4. *Important Terminology*

| Term | Definition |
|------|------------|
| *Docker Daemon* | Background service that manages Docker operations |
| *Docker Client* | CLI interface for user commands |
| *Docker Registry* | Platform to store/share images (Docker Hub, Quay.io) |
| *Dockerfile* | Text file with instructions to build image |
| *Docker Image* | Snapshot/template containing app + dependencies |
| *Docker Container* | Running instance of an image |

---

### 5. *Hands-On: First Docker Container*

*Installation Steps (Ubuntu EC2):*
```bash
# Update repositories
sudo apt update

# Install Docker
sudo apt install docker.io -y

# Verify Docker is running
sudo systemctl status docker

# Add user to docker group (avoid sudo)
sudo usermod -aG docker ubuntu

# Logout and login back for changes to take effect
```

*Sample Dockerfile:*
```dockerfile
FROM ubuntu:latest
WORKDIR /app
COPY . /app
RUN apt-get update && apt-get install -y python3
CMD ["python3", "app.py"]
```

*Build and Run:*
```bash
# Build image with tag
docker build -t username/my-first-docker-image:latest .

# Run container
docker run -it username/my-first-docker-image:latest

# Login to Docker Hub
docker login

# Push to registry
docker push username/my-first-docker-image:latest
```

---

## Key Takeaways

1. **Containers vs VMs**: Containers are ~100x smaller because they share the host OS kernel
2. **Security**: Containers provide logical isolation through minimal system dependencies
3. **Efficiency**: Multiple containers can run on a single VM, sharing resources when idle
4. **Portability**: Docker images can run anywhere without dependency installation
5. **Docker Hub vs GitHub**: Docker Hub stores images, GitHub stores source code

---

## Common Beginner Mistakes

- *Permission denied errors* - Need to add user to docker group and re-login
- *Docker daemon not running* - Check with `systemctl status docker`
- *Forgetting to tag images* - Always use meaningful tags for organization

---

## Next Steps (Day 25)

- Multi-stage Docker builds
- Reducing Docker image size
- Docker best practices
- Advanced Dockerfile techniques
- Docker interview questions

---

## Resources

- GitHub Repository: Contains detailed explanations and example files
- Docker Hub: Create free account for sharing images
- Docker Desktop: Alternative for Windows/Mac users (includes VM automatically)