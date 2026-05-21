# Docker

This guide covers essential terminal commands for building, running, monitoring, and managing Docker containers, images, volumes, and networks.

---

## 1. `docker run` - Run a Container
Creates and starts a container from a specified image.

* **Syntax:** `docker run [options] <image> [command]`
* **Example Usage:**
  ```bash
  # Run a detached Nginx container, mapping local port 8080 to container port 80, named web-server
  docker run -d -p 8080:80 --name web-server nginx
  ```
* **Useful Flags:**
  * `-d`: Run container in background (detached mode).
  * `-it`: Interactive mode with a pseudo-TTY (useful for shells).
  * `-p <host_port>:<container_port>`: Map ports.
  * `-v <host_path>:<container_path>`: Mount volumes.
  * `--rm`: Automatically remove the container when it exits.
  * `--name <name>`: Assign a name to the container.
  * `--env-file <file>`: Load environment variables from a file.

---

## 2. `docker ps` - List Containers
Lists containers on the system.

* **Syntax:** `docker ps [options]`
* **Example Usage:**
  ```bash
  # List all running and stopped containers
  docker ps -a
  ```
* **Useful Flags:**
  * `-a`: Show all containers (default shows running only).
  * `-q`: Only display container IDs (numeric IDs).
  * `-s`: Display total file sizes.

---

## 3. `docker images` - List Images
Lists images stored locally.

* **Syntax:** `docker images [options]`
* **Example Usage:**
  ```bash
  docker images
  ```
* **Useful Flags:**
  * `-a`: Show all images (including intermediate image layers).
  * `-q`: Show only numeric image IDs.

---

## 4. `docker build` - Build an Image
Builds an image from a Dockerfile.

* **Syntax:** `docker build [options] <path_or_url>`
* **Example Usage:**
  ```bash
  # Build an image from current directory and tag it as "myapp:v1.0"
  docker build -t myapp:v1.0 .
  ```
* **Useful Flags:**
  * `-t <name:tag>`: Name and optionally a tag in the 'name:tag' format.
  * `-f <filename>`: Specify custom Dockerfile name.
  * `--no-cache`: Do not use cache when building the image.

---

## 5. `docker exec` - Execute Command in Running Container
Runs a new command in an already active container.

* **Syntax:** `docker exec [options] <container> <command>`
* **Example Usage:**
  ```bash
  # Open interactive bash shell inside a container named "web-server"
  docker exec -it web-server /bin/bash
  ```
* **Useful Flags:**
  * `-it`: Interactive mode, allocate TTY.
  * `-u <username>`: Username or UID (format: <name|uid>[:<group|gid>]).

---

## 6. `docker stop` & `docker start` - Control Containers
Stops running containers or starts stopped ones.

* **Syntax:**
  * `docker stop [options] <container_id_or_name>`
  * `docker start [options] <container_id_or_name>`
* **Example Usage:**
  ```bash
  # Stop and restart web-server
  docker stop web-server
  docker start web-server
  ```

---

## 7. `docker rm` & `docker rmi` - Remove Containers/Images
Deletes containers (`rm`) or images (`rmi`) from local storage.

* **Syntax:**
  * `docker rm [options] <container_name_or_ID>`
  * `docker rmi [options] <image_name_or_ID>`
* **Example Usage:**
  ```bash
  # Force remove a running container
  docker rm -f running-container-name

  # Remove all unused/dangling images
  docker rmi $(docker images -f "dangling=true" -q)
  ```
* **Useful Flags:**
  * `-f` (rm): Force the removal of a running container (using SIGKILL).
  * `-f` (rmi): Force removal of the image.

---

## 8. `docker logs` - View Container Logs
Fetches stdout and stderr outputs of a container.

* **Syntax:** `docker logs [options] <container>`
* **Example Usage:**
  ```bash
  # Tail logs and follow them in real time
  docker logs -f --tail 100 web-server
  ```
* **Useful Flags:**
  * `-f`: Follow log output.
  * `--tail [lines]`: Number of lines to show from the end of the logs.
  * `-t`: Show timestamps.

---

## 9. `docker volume` - Manage Volumes
Handles persistent storage options separate from container lifecycles.

* **Syntax:** `docker volume <subcommand>`
* **Example Usage:**
  ```bash
  # Create a volume
  docker volume create db-data

  # List all volumes
  docker volume ls

  # Remove unused local volumes
  docker volume prune
  ```

---

## 10. `docker network` - Manage Networks
Handles connectivity and network bridging between containers.

* **Syntax:** `docker network <subcommand>`
* **Example Usage:**
  ```bash
  # Create custom bridge network
  docker network create app-network

  # List existing networks
  docker network ls
  ```

---

## 11. `docker compose` - Multi-Container Orchestration
Defines and runs multi-container Docker applications configured via a `docker-compose.yml` file.

* **Syntax:** `docker compose [options] [command]`
* **Example Usage:**
  ```bash
  # Start all services defined in docker-compose.yml in detached background mode
  docker compose up -d

  # Stop and remove containers, networks, and volumes
  docker compose down -v
  ```
* **Useful Commands:**
  * `up`: Create and start containers.
  * `down`: Stop and remove resources.
  * `logs`: View output logs of all services.
  * `ps`: List containers.
  * `restart`: Restart services.
