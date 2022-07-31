# How to run Mariadb with Docker and Docker-Compose

### Prerequisites:
Docker installed locally and permissions to use it to launch containers and Docker compose is installed locally.

Install docker / dockercompose On Ubuntu:
```
sudo apt-get update
sudo apt upgrade -y
sudo apt install docker.io -y
sudo apt install curl vim -y
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
# sudo usermod -aG docker [USER]
```

### Using Docker Run Command To Create MariaDB
Create data dir:
```
sudo mkdir -p /data/mariadb
```
Run the container
```
docker run -d --name my-mariadb -p 3306:3306 -v /data/mariadb:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=S3cret -e MYSQL_PASSWORD=An0thrS3crt -e MYSQL_USER=citizix_user  -e MYSQL_DATABASE=citizix_db mariadb
```
<img width="1184" alt="Screen Shot 2022-07-31 at 5 13 21 PM" src="https://user-images.githubusercontent.com/43518207/182035476-8537260d-086e-462a-aa4e-caa025dcf4c5.png">

In the above command:
```
• -d instructs docker container to run container in background and print container ID.
• -p is for port mapping.
• -v directive is used to mount volumes. 
• -e argument is for the environment variables.
```
To check that our container is running use `docker ps` command:
<img width="974" alt="Screen Shot 2022-07-31 at 5 14 06 PM" src="https://user-images.githubusercontent.com/43518207/182035618-7a07f3bd-4f45-47a8-b151-af4c08714b39.png">

### Using DockerCompose To Create MariaDB
Docker Compose allows you to define the service (Mariadb in our case) with properties like the image to use, ports to expose, volumes to mount and environment variables.

Save this as docker-compose.yaml:
```
version: '3.3'

services:
  mysql:
    image: mariadb
    ports:
      - 3306:3306
    volumes:
      -  /data/mysql:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=S3cret
      - MYSQL_PASSWORD=An0thrS3crt
      - MYSQL_USER=citizix_user
      - MYSQL_DATABASE=citizix_db
```
Now bring up the containers:
```
docker-compose up -d
```
<img width="693" alt="Screen Shot 2022-07-31 at 11 51 10 AM" src="https://user-images.githubusercontent.com/43518207/182035111-5b8e5930-cf8b-485e-9944-cfc2d5ad2aef.png">

The commands:
```
• up brings up the container
• -d in a detached mode
```
Verify the container processes using `docker-compose ps` :
<img width="810" alt="Screen Shot 2022-07-31 at 11 52 05 AM" src="https://user-images.githubusercontent.com/43518207/182035122-14a1b447-9c36-4ac4-bc2e-a2456a2f6cac.png">

