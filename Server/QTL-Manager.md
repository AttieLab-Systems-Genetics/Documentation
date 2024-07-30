# Docker Compose Management for QTL-Viewers
This guide explains how to manage Docker Compose projects for QTL-Viewers using various `docker compose` commands. Follow the steps below to start, stop, restart, pull images, and check logs for your Docker Compose services.
## Prerequisites
Ensure you have the following installed:
- Docker
- Docker Compose
## Usage
### Navigate to Your Project Folder
First, navigate to the folder containing your `docker-compose.yml` file. For QTL-Viewers, this folder is usually named `qtl-viewers`:
```sh
cd <path_to_your_project_folder>
```
### Docker Compose Commands
1. **Start Docker Compose Services:**
```sh
docker compose -p <folder-name> up -d
```
- `up`: Builds, (re)creates, starts, and attaches to containers for a service.
- `-d`: Runs containers in the background (detached mode).
- `-p <folder-name>`: Specifies the project name (usually the folder name).
2. **Stop Docker Compose Services:**
```sh
docker compose -p <folder-name> down
```
- `down`: Stops and removes containers, networks, images, and volumes created by `up`.
- `-p <folder-name>`: Specifies the project name (usually the folder name).
3. **Restart Docker Compose Services:**
```sh
docker compose -p <folder-name> down && docker compose -p <folder-name> up -d
```
- This command sequence stops the services and then starts them again.
- `-p <folder-name>`: Specifies the project name (usually the folder name).
4. **Pull Latest Docker Images:**
```sh
docker compose -p <folder-name> pull
```
- `pull`: Fetches the newest version of the images specified in the `docker-compose.yml` file.
- `-p <folder-name>`: Specifies the project name (usually the folder name).
5. **Get Docker Container Logs:**
```sh
docker logs <container_name>
```
- `logs`: Fetches the logs of a container.
- `<container_name>`: The name of the container whose logs you want to fetch.
