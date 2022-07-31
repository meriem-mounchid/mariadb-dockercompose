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

In the above command:

### Using DockerCompose To Create MariaDB
```
docker-compose up -d
```
