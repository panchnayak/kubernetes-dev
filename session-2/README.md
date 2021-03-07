## Working with docker-compose on CentOS 7



### install docker compose on CentOS
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
### Docker-compose commands

```
The following command runs your wordpress site in detached mode, pulls the needed Docker images from dockerhub , and starts the wordpress and database containers.
$ docker-compose up -d

$ docker-compose down
This command stops the containers removes the default network, but preserves your WordPress database.

$ docker-compose down --volumes 
The above command removes the containers, default network, and the WordPress database.
```

### Install Local Docker Registry on CentOS 7

```

$ sudo yum update -y
$ sudo yum -y install docker-distribution
$ sudo systemctl enable docker-distribution

Check the Status if the service is loaded

$ sudo systemctl status docker-distribution

Docker registry by default runs on port 5000

Add the Registry Server to Docker Enginee, edit /etc/docker/daemon.json 

$ sudo vi /etc/docker/daemon.json

Add the following line
{
 "insecure-registries" : ["bn-cr.local:5000"]
}

$ sudo systemctl restart docker-distribution

```
