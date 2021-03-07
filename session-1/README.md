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

$ sudo usermod -aG docker $USER

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
