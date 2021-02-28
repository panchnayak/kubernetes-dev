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

Now start the docker demon by starting and enabling the docker system service

$ sudo systemctl enable docker --now

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
$ docker run –dit -p 8080:80 -v /hostdir/:/dockerdir
$ docker attach
$ docker exec -it <container name> <command to excute inside the container> 
```

## Install a webserver using docker
```
$ docker run -dit --name boc-web -p 80:80 -v /home/pnayak/wordpress/:/var/www/html centos/httpd
-d option is for detached mode
-i interactive
-t is for terminal

```
## install docker compose on CentOS
```
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.28.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
$ sudo chmod +x /usr/local/bin/docker-compose
$ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
$ docker-compose --version

Next step : Prepare the docker-compose.yml configuration file, you can download the docker-compose-yml file from this repository, this is a smaple configuration for install and running wordpress, this docker compose installes and run 2 docker containers.

1.latest mysql docker container 
2.latest wordpress server 

Wordpress serer is basically a webserver and the wordpress code already installed for you and packaged in a single docker container.
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
