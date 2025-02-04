## Docker Commands

- **List all docker containers**:
  ```bash
  > docker ps -a
  ```
- **Build docker image**:
  ```bash
  > docker build -t <image-tag> .
  ```
- **Login into a docker registry**:
  ```bash
  > docker login -u username --password password --registry my-registry.example.com
  ```
- **Tag a docker image**:
  ```bash
  > docker tag <image-name> <image-name>:latest
  ```
- **Push/Publish a docker image to a registry**:
  ```bash 
  > docker push <image-name>:latest
  ```
- **Launch container in local environment (refer to local .env file, and run in detached mode)**:
  ```bash
  > docker run --env-file .env -d --name <container-name> -p <host-port-number>:<container-port-number> <image-name>
  ```
- **Launch docker container with interactive shell**:
  ```bash
  > docker exec -it <my-container> bash
  ```
- **Launch docker container with docker compose**:
  ```bash
  > docker compose up --build
  ```
- **Exit docker compose**:
  ```bash
  > docker compose down
  ```
- **Stop and remove all containers**:
  ```bash
  > docker stop $(docker ps -aq) && docker remove $(docker ps -aq)
  ```
- **Remove all unused docker data**:
  ```bash
  > docker system prune
  > docker system prune -all
  ```

