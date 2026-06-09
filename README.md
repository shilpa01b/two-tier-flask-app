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
  -docker-compose.yml # NEW: Docker Compose configuration


## Prerequisites
Make sure you have the following installed:
- Docker
- docker compose
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

## Quick Start with Docker Compose(NEW: Docker Compose configuration)

### 1. Build and Run All Containers

docker compose up 
  or
docker compose up -d (for dettached mode)

This will:
- Build the Flask image automatically
- Create the MySQL container with data volume
- Set up the custom network
- Start both containers together

### 2. Access the App

Open your browser and go to:
http://localhost:5000

### 3. Stop the Containers

docker compose down

This stops and removes:
- All containers
- Networks created by compose

### 4. Remove Everything (including volume)

docker compose down --volumes

## Push image to Docker Hub

The Flask app image is built locally and pushed to Docker Hub as
'''
shilpabiswas09/two-tier-app:latest
'''
 so it can be pulled and run through Docker Compose on any machine.

## Notes
- Use `MYSQL_HOST=mysql` because container names are used for service communication inside the same Docker network.
- The MySQL container stores data in a volume, so data remains even after container restart.
- If Flask cannot connect to MySQL, check if both containers are on the same network.
- Docker Compose automatically waits for MySQL to be ready before starting the Flask app (using `depends_on`)
- To view logs: docker compose logs or 

