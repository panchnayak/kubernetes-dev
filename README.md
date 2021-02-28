# Kubernetes Developer Hands-On (Deploying Microservices on K8S)

This is the supporting github repository for the Kubernets Developer Course on guru.basicneed.com, Please look here the sample code snippets, sample programs and file discussed in the course.

## Getting Started

These instructions will get you start your course on a local laptop or Desktop for development and testing purposes. 
We ll cover latter how to create and deploy the project on a live systems on cloud environment.

### Prerequisites

Core Java Development is a pre-requisite for this course. This course does not have any mandatory requirements, but core Java programming knowledge is required to get the most out of this course.This course will not teach you Java development nor Springboot Development, it is expected that you have the basics to understand Java and Springboot.The platform of Development is Windows and or MacOS but Deployment will be on Linux Environment (preferably on CentOS) and finally on a Cloud Environment.


### Installing Docker on your Laptop

A step by step instruction will be followed aftr the live session

## Lesson-1 - Container Basics

# Docker commdands reference

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

# Docker-compose commands

The following command runs your wordpress site in detached mode, pulls the needed Docker images from dockerhub , and starts the wordpress and database containers.
$ docker-compose up -d

$ docker-compose down
This command stops the containers removes the default network, but preserves your WordPress database.

$ docker-compose down --volumes 
The above command removes the containers, default network, and the WordPress database.


## Running the tests
---

## Deployment

Add additional notes about how to deploy this on a live system will be given latter

## Built With
------

## Contributing

----------
## Versioning

------

## Authors

* **Panchaleswar Nayak** - *Initial work* - [Panchaleswar Nayak](https://guru.basicneed.com/courses/kubernetes-developer-hands-on/lessons/docker-basics/)


## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

