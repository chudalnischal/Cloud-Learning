# Docker Introduction and Architecture

## Introduction
Docker is an open container management platform. It is a software platform for developing, shipping, and running applications based on containers --- small and lightweight execution environments that make shared use of the operating system kernel and run it in isolation from one another. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.

With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker's methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

### Real Experience
Let me give you my real experience of the first time I needed Docker in my career. I was assigned a task to validate the source code of two applications simultaneously. The first application had a dependency on `pywinrm 1.1`, and the second one had a dependency on `pywinrm 2.2`. At the time, I could test only one application. I could have created two VMs and installed each application on a separate VM, but VMs require more memory and resources from the host machine. This is where I leveraged containerization.

---

## VMs vs Containers

### What is a Virtual Machine?
A Virtual Machine (VM) is a system that acts exactly like a computer. VMs are like physical hardware, turning one server into many servers. They use a technology called a hypervisor, which allows multiple VMs to run on a single machine. Each VM has:
- A full copy of an operating system
- The application
- Necessary binaries and libraries

VMs are bulky in nature, with their own memory management and the associated overhead of virtual device drivers. Valuable resources are emulated for the guest OS and hypervisor, enabling multiple instances of one or more operating systems to run in parallel on a single host. Every guest OS runs as an independent entity, akin to an isolated house where no resources are shared.

### What are Containers?
Containers address modern software development's challenge of operating and maintaining applications in an isolated environment without interference. While virtual machines solve this problem, they are bulky due to requiring their own OS, making maintenance and upgrades difficult.

Containers isolate application environments from one another but share the underlying OS kernel. Containers:
- Are an abstraction at the application layer, packaging code and dependencies together
- Run as isolated processes in user space
- Take up less space than VMs (typically tens of MBs in size)
- Require fewer VMs and operating systems

#### Docker Containers
Docker containers are executed using the Docker engine instead of a hypervisor. They:
- Are smaller than VMs
- Enable faster startup with better performance
- Provide less isolation but greater compatibility by sharing the host's kernel

This makes Docker containers comparable to housing society homes, where resources are shared.

---

### Differences Between Docker and VMs

| Feature          | Virtual Machines                     | Docker Containers                  |
|------------------|--------------------------------------|------------------------------------|
| **OS and Architecture** | Host OS and guest OS inside each VM. Guest OS can be any OS. | Host OS shared among containers, making them lightweight. |
| **Portability**   | Cannot be easily ported across platforms. | Easily portable and self-contained. |
| **Performance**   | Bulky due to loading the entire OS.  | Lightweight, with faster boot times. |

---

## Advantages of Containers
- **Lightweight Applications:** Easier to assemble, maintain, and port.
- **Agility:** Containers are more agile than VMs.
- **Hybrid and Multi-Cloud:** Enable seamless adoption.
- **Cost-Effective:** Save on VM licensing.
- **Isolation:** Keep applications isolated from each other and the underlying system.
- **Flexibility:** More adaptable and manageable compared to VMs.

# Docker Introduction and Architecture

## What is Docker?
Docker is an open-source platform that simplifies creating containers and container-based applications. 

## Docker Architecture
Docker uses a client-server architecture. The Docker client communicates with the Docker daemon, which is responsible for building, running, and distributing your Docker containers. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.

Docker is written in the Go language and uses namespaces to provide isolated workspaces (containers). When you run a container, Docker creates a set of namespaces for it. These namespaces:
- Provide a layer of isolation
- Limit access to each container's namespace

Each container operates in its own namespace, ensuring it is isolated from others.

### Docker Daemon
The Docker daemon (`dockerd`) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.

### Docker Client
The Docker client (`docker`) is the primary way that many Docker users interact with Docker. When you use commands such as `docker run`, the client sends these commands to `dockerd`, which runs them. The `docker` command uses the Docker API.

### Docker Registries
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and by default, Docker looks for images on Docker Hub. You can also run your private registry. When you use the `docker pull` or `docker run` commands, the required images are pulled from your configured registry. When you use the `docker push` command, your image is pushed to your configured registry.

## Docker Components

### Images
An image is a read-only template with instructions for creating a Docker container. For example, you can build an image based on the Ubuntu image, install the Apache web server, your application, and configuration details. You can create images by writing a `Dockerfile` and publishing them to a registry. Each instruction in a `Dockerfile` creates a layer in the image.

### Containers
A container is a runnable instance of an image. It is isolated from other containers and the host machine. Containers can be started, stopped, moved, or deleted. When removed, any changes to the container that are not stored in persistent volumes will also be removed.

---

#  Docker Commands Guide

## Listing Docker Images
```bash
docker image ls
```
Displays all the local Docker images.

## Searching for Images
```bash
docker search ubuntu
```
Searches for Docker images with the term "ubuntu" in Docker Hub.

## Pulling Docker Images
```bash
docker image pull ubuntu:14.04
```
Pulls the Ubuntu 14.04 image from Docker Hub.

## Running a Container
```bash
docker container run ubuntu:14.04 cat /etc/os-release
```
Runs a container from the Ubuntu 14.04 image and displays the OS release information.

## Listing Running Containers
```bash
docker container ls
```
Displays all running containers.

## Listing All Containers
```bash
docker container ls -a
```
Lists all containers, including stopped ones.

## Removing a Container
```bash
docker container rm <CONTAINER_ID>
```
Removes a specific container by its ID or name.

## Running a Container in Detached Mode
```bash
docker container run -d ubuntu:14.04 sleep 30
```
Runs a container in the background.


## Docker Interactive Mode
Docker allows you to run a container in interactive mode using the `-it` option. This provides an interactive bash shell for the container.

```bash
docker container run -it ubuntu:14.04 /bin/bash
```

To detach from the container while keeping it running in the background, press `CTRL + P` followed by `CTRL + Q`.

---

## Managing Docker Containers

### Stopping a Container
Stops one or more running containers.

**Syntax:**
```bash
docker container stop [OPTIONS] CONTAINER [CONTAINER...]
```
**Options:**
- `--time, -t`: Seconds to wait before forcibly stopping (default: 10 seconds).

---

### Starting a Container
Starts one or more stopped containers.

**Syntax:**
```bash
docker container start [OPTIONS] CONTAINER [CONTAINER...]
```
**Options:**
- `--attach, -a`: Attach STDOUT/STDERR and forward signals.
- `--interactive, -i`: Attach container's STDIN.

**Example:**
```bash
docker container start <container-name>
```

---

## Inspecting Docker Objects
`docker inspect` provides low-level information on Docker objects such as images, containers, networks, and volumes.

**Syntax:**
```bash
docker inspect [OPTIONS] NAME|ID [NAME|ID...]
```
**Options:**
- `--format`: Format the output using a Go template.
- `--size`: Display total file sizes (if inspecting a container).
- `--type`: Specify the type of object to inspect.

**Examples:**
```bash
docker container inspect <container-name>
docker image inspect ubuntu:14.04
docker volume inspect <volume-id>
docker network inspect <network-id>
```

---

## Viewing Logs
Use the `docker logs` command to view logs from a running container.

**Syntax:**
```bash
docker container logs [OPTIONS] CONTAINER
```
**Options:**
- `-f, --follow`: Follow log output.

**Example:**
```bash
docker container logs <container-name>
```

---

## Restarting and Renaming Containers

### Restarting a Container
Restarts one or more containers.

**Syntax:**
```bash
docker container restart [OPTIONS] CONTAINER [CONTAINER...]
```
**Options:**
- `--time, -t`: Seconds to wait before forcibly restarting (default: 10 seconds).

---

### Renaming a Container
Renames a Docker container.

**Syntax:**
```bash
docker rename CONTAINER NEW_NAME
```
**Example:**
```bash
docker rename old_container new_container
```

---

## Port Mapping
Expose container ports to the outside world using the `-p` or `--publish` flag.

**Examples:**
```bash
-p 8080:80 # Map port 80 in the container to port 8080 on the host.
-P          # Publish all exposed ports to random ports.
```
**Command:**
```bash
docker container run -itd -p 8080:80 nginx
```

---

## Attaching to a Container
Reattach to a running container using its ID or name.

**Syntax:**
```bash
docker attach [OPTIONS] CONTAINER
```
**Options:**
- `--detach-keys`: Override the key sequence for detaching.
- `--no-stdin`: Do not attach STDIN.
- `--sig-proxy`: Proxy all received signals.

**Example:**
```bash
docker container attach <container-name>
```

---

## Killing a Container
Kills the process running inside the container abruptly.

**Syntax:**
```bash
docker kill [OPTIONS] CONTAINER [CONTAINER...]
```
**Options:**
- `--signal, -s`: Signal to send to the container.

**Example:**
```bash
docker container kill <container-id>
```

**Warning:** Avoid using this command in production environments unless necessary.

---

## Pausing and Unpausing Containers

### Pause a Container
Pauses all processes within a container.

**Syntax:**
```bash
docker container pause CONTAINER [CONTAINER...]
```
**Example:**
```bash
docker container pause <container-name>
```

### Unpause a Container
Resumes all processes within a container.

**Syntax:**
```bash
docker container unpause CONTAINER [CONTAINER...]
```

---

## Pruning Containers
Removes all stopped containers.

**Syntax:**
```bash
docker container prune [OPTIONS]
```
**Options:**
- `--force, -f`: Skip confirmation prompt.

**Example:**
```bash
docker container prune
```

---

## Creating and Running Containers

### Creating a Container
Creates a new container in a "created" state.

**Syntax:**
```bash
docker container create [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### Difference Between `create` and `run`
- `docker create` creates a container without starting it.
- `docker run` combines `docker create` and `docker start`.

**Example:**
```bash
docker container create <image-name>
docker container start <container-name>
```

---

## Inspecting Filesystem Changes
Tracks changes to files or directories within a container.

**Syntax:**
```bash
docker container diff <container-id>
```
**Symbols:**
- `A`: Added.
- `C`: Changed.
- `D`: Deleted.

---

## Copying Files
Copies files between a container and the host machine.

**Syntax:**
```bash
docker cp <src-path> <container>:<dest-path>
docker cp <container>:<src-path> <dest-path>
```

---

## Importing and Exporting Containers

### Export a Container
Exports a container's filesystem as a tar archive.

**Syntax:**
```bash
docker container export [OPTIONS] CONTAINER
```
**Example:**
```bash
docker container export <container-name> -o example.tar
```

### Import a Container
Imports a tar archive as a Docker image.

**Syntax:**
```bash
docker image import [OPTIONS] FILE|URL|- [REPOSITORY[:TAG]]
```
**Example:**
```bash
docker image import example.tar example
```

---

## Committing Changes
Creates a new image from a container's changes.

**Syntax:**
```bash
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```
**Options:**
- `--author, -a`: Author of the change.
- `--message, -m`: Commit message.

**Example:**
```bash
docker container commit <container-id> <new-image-name>
```

---

## Managing Docker Images

### Listing Images
Lists all Docker images.

**Syntax:**
```bash
docker image ls [OPTIONS]
```
**Example:**
```bash
docker image ls --format '{{.ID}}, {{.Repository}}, {{.Tag}}'
```

### Viewing Image History
Displays the history of an image.

**Syntax:**
```bash
docker image history <image-name>
```

### Removing Images
Deletes specified images.

**Syntax:**
```bash
docker image rm [OPTIONS] IMAGE [IMAGE...]
```
**Example:**
```bash
docker image rm -f <image-name>
```

### Inspecting Images
Provides detailed information about one or more images.

**Syntax:**
```bash
docker image inspect <image-name>
```

---

This markdown file summarizes the essential Docker commands, providing a quick reference for container and image management.

