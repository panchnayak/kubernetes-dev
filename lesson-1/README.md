# Lesson-1 - Container Basics

## Preparing the Development Environment

Install VirtualBox on your Laptop, and then create a VM using VirtualBox, install CentOS 7 on the VM.

### Install Docker on CentOS on your Laptop

```
Log into your machine as a user with sudo or root privileges.

$ ssh username@IP-ADDRESS-OF-VM 
$ sudo yum update -y
$ curl -sSL https://get.docker.com | bash

Add a non-root user to the "docker" group, by doing this you grant the user the ability to run containers which can be used to obtain root privileges on the docker host.

$ sudo usermod -aG docker "your-user-name"

Then logout and login again so that the user gets the required access to run the docker containers.

```

## Docker commands reference

```
$ docker ps
$ docker container ls
$ docker ps –a
$ docker images
$ docker stop
$ docker rm
$ docker rmi
$ docker run –dit -p 8080:80 -v v /hostdir/:/dockerdir
$ docker attach
$ docker exec -it <container name> <command to excute inside the container> 
```
## Docker-compose commands

```
The following command runs your wordpress site in detached mode, pulls the needed Docker images from dockerhub , and starts the wordpress and database containers.
$ docker-compose up -d

$ docker-compose down
This command stops the containers removes the default network, but preserves your WordPress database.

$ docker-compose down --volumes 
The above command removes the containers, default network, and the WordPress database.
```
