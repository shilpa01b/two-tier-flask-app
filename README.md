#  Containerize Flask + MySQL Two-Tier App with Docker

This is a simple Flask application that connects to a MySQL database using Docker.

## Features
- Flask web application
- MySQL database container
- Custom Docker network
- Persistent MySQL data using Docker volume

## Project Structure

project-folder/
  -templates/
    index.html
  -app.py
  -Dockerfile
  -message.sql
  -README.md
  -requirements.txt
  


## Prerequisites
Make sure you have the following installed:
- Docker
- Git (optional, for cloning the repository)

## Build the Flask Image

docker build -t myapp .


## Create a Custom Network

docker network create two-tier


## Create a Volume for MySQL Data

docker volume create mysql-data


## Run MySQL Container

 docker run -d --name mysql --network two-tier -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops mysql


## Run Flask Container
docker run -d --name mysql --network two-tier -v mysql-data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=devops mysql

## Access the App
Open your browser and go to:

http://localhost:5000


## Stop the Containers

docker stop <cont_id> && docker rm <cont_id>

## Remove Network and Volume

docker network rm two-tier
docker volume rm mysql-data


## Notes
- Use `MYSQL_HOST=mysql` because container names are used for service communication inside the same Docker network.
- The MySQL container stores data in a volume, so data remains even after container restart.
- If Flask cannot connect to MySQL, check if both containers are on the same network.


