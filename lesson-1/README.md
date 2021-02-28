### Installing Docker on your Laptop

A step by step instruction will be followed aftr the live session

## Lesson-1 - Container Basics

## Docker commdands reference

### $ docker ps
### $ docker container ls
### $ docker ps –a
### $ docker images
### $ docker stop
### $ docker rm
### $ docker rmi
### $ docker run –dit -p 8080:80 -v v /hostdir/:/dockerdir
### $ docker attach
### $ docker exec -it <container name> <command to excute inside the container> 

# Docker-compose commands

The following command runs your wordpress site in detached mode, pulls the needed Docker images from dockerhub , and starts the wordpress and database containers.
### $ docker-compose up -d

### $ docker-compose down
This command stops the containers removes the default network, but preserves your WordPress database.

### $ docker-compose down --volumes 
The above command removes the containers, default network, and the WordPress database.
