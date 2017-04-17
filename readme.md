![Docker logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_logo.png)

- Introduction

#### GL1 , tp base de donnee 

Bases de donnees reparties

________________________

Rezig Mahdi,Yosra Bettaieb, Bouchnak Wael, Rim Zouiter

big thanks to https://github.com/theodorosploumis 

---

### Question ?

- Qui a une connaissance à propos Docker [Docker](http://docker.com)?
- Qui a utilisé Docker pour le développemnt?
- Qui a utilisé Docker pour la production?


---

### C'est quoi Docker (v1.11)

> Docker est une plate-forme ouverte pour le développement, l'exécution des applications .

> Docker vous permet d'empaqueter une application avec toutes ses dépendances dans une format normalisée pour le développement de logiciels.

---

### Docker vs VMs

![Docker vs traditional Virtualization](https://insights.sei.cmu.edu/assets/content/VM-Diagram.png)

---

### L'histoire de Docker 

 - Solomon Hykes ([@solomonstre](https://twitter.com/solomonstre))
 - dotCloud (now Docker Inc)
 - Mars 2013
 - Apache 2.0 license
 - 30k étoiles sur Github
 - 260k référentiels publiques sur hub.docker.com
 - Docker rejoint l' "[Open Container Initiative](https://www.opencontainers.org/)", June 2015

---

### Les Bénéfices de Docker 

 - Rapide (deploiment, migration, restarts)
 - Securisé
 - Léger (save disk & CPU)
 - Open Source
 - Portable 
 - Microservices et integrations (APIs)
 - Simplifié DevOps
 - capabilité de Version de control 

---

###  Usages Communs de Docker

 - Environnement Sandbox  (developper, tester, deboguer, eduquer)
 - Continuité d' Integration & Deploiment
 - Mise à l'échelle des applications
 - Developpement collaboratif
 - configuration d'Infrastructure 
 -  developpement local
 - Multi-tier applications
 - PaaS, SaaS

###### Voir [survey results for 2016](https://www.docker.com/survey-2016)

---

### La technologie derrière Docker

 - Linux [x86-64](https://www.wikiwand.com/en/X86-64)
 - [Go](https://golang.org/) language
 - [Client - Server](https://www.wikiwand.com/en/Client%E2%80%93server_model) (deamon) architecture
 - Union file systems ([UnionFS](https://www.wikiwand.com/en/UnionFS): AUFS, btrfs, vfs etc)
 - [Namespaces](https://en.wikipedia.org/wiki/Cgroups#NAMESPACE-ISOLATION) (pid, net, ipc, mnt, uts)
 - Control Groups ([cgroups](https://www.wikiwand.com/en/Cgroups))
 - Container format ([libcontainer](https://github.com/opencontainers/runc/tree/master/libcontainer "Libcontainer provides a native Go implementation for creating containers with namespaces, cgroups, capabilities, and filesystem access controls. It allows you to manage the lifecycle of the container performing additional operations after the container is created."))

###### Voir [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### L'architecture de Docker 

![Docker architecture](https://docs.docker.com/engine/article-img/architecture.svg)
###### Voir [Understanding docker](https://docs.docker.com/engine/understanding-docker/)

---

### Les composants de Docker 

 - (Docker) client
 - daemon
 - engine
 - machine
 - compose
 - swarm
 - registry

---

### Docker client

Le premier  utilisateur de l'interface de Docker. Docker accepte les commandes de l'utilisateur
et les communique  travers le daemon Docker .

---

### Docker daemon

Il exécute la machine local. L'utilisateur n'interagit pas directement avec le daemon,
mais à travers le client Docker gràce à le RESTful api or sockets.

---

### Docker engine

 Client avec Daemon est considéré comme  docker-compose tool. Généralement appelé "docker".

---

### Docker machine

![Docker machine logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_machine.png)

l'outil qui rend facile de créer Docker hosts sur votre pc,
sur cloud  et dans votre centre de données.
création de serveurs, installation de Docker , puis configuration de client Docker pour communiquer avec.
Obligatoir pour les utilisateurs du Mac, Windows .

---

### Docker compose

![Docker compose logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_compose.png)

un outil pour définir et exécuter les applications complex  avec Docker
(exemple :  multi-container application) avec un seul fichier.

---

### Docker swarm

![Docker swarm logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_swarm.png)

un outil cluster native pour Docker. Swarm regroupe les machines Docker et les expose comme une seules machine virtuelle Docker . Il s'élargit à plusieurs machines.

---

### La distribution Docker 

![Docker distribution logo](https://raw.githubusercontent.com/theodorosploumis/docker-presentation/gh-pages/img/docker_distribution.png)

Un service conteneur référenciel d'une images qui repond à l' API Registry .

---

### Les étapes de Docker workflow

```
docker run -i -t -d ubuntu:15.04 /bin/bash
```

 - Pulls the ubuntu:15.04 [image](https://docs.docker.com/engine/userguide/containers/dockerimages/ "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot.") from the [registry](https://docs.docker.com/registry/ "The central place where all publicly published images live. You can search it, upload your images there and when you pull a docker image, it comes the repository/hub.")
 - Creates a new [container](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/ "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides.")
 - Allocates a filesystem and mounts a read-write [layer](https://docs.docker.com/engine/reference/glossary/#filesystem "A set of read-only files to provision the system. Think of a layer as a read only snapshot of the filesystem.")
 - Allocates a [network/bridge interface](https://www.wikiwand.com/en/Bridging_%28networking%29 "")
 - Sets up an [IP address](https://www.wikiwand.com/en/IP_address "An Internet Protocol address (IP address) is a numerical label assigned to each device (e.g., computer, printer) participating in a computer network that uses the Internet Protocol for communication.")
 - Executes a process that you specify (``` /bin/bash ```)
 - Captures and provides application output

---

## L'image docker 

![ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/image-layers.jpg "A read-only layer that is the base of your container. It can have a parent image to abstract away the more basic filesystem snapshot. Each Docker image references a list of read-only layers that represent filesystem differences. Layers are stacked on top of each other to form a base for a container’s root filesystem.")

---

### Le  conteneur docker 

![container using ubuntu:15.04 image](https://docs.docker.com/engine/userguide/storagedriver/images/container-layers.jpg "A runnable instance of the image, basically it is a process isolated by docker that runs on top of the filesystem that an image provides. For each containers there is a new, thin, writable layer - container layer - on top of the underlying stack (image).")

---

### The Dockerfile

> Le Dockerfile est une document  text qui contient toutes les commandes que l'utilisateurs peut l'utiliser pour créer une image.

 - [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) on docker docs
 - Official Dockerfiles ([rails](https://github.com/docker-library/rails/blob/master/Dockerfile), [nodejs](https://github.com/ReadyTalk/nodejs-docker/blob/master/base/Dockerfile), [django](https://github.com/docker-library/django/blob/master/3.4/Dockerfile), [Drupal](https://github.com/docker-library/drupal/blob/master/8.1/fpm/Dockerfile))

---

### les commandes Docker 

```
// General info
man docker // man docker-run
docker help // docker help run
docker info
docker version
docker network ls

// Images
docker images // docker [IMAGE_NAME]
docker pull [IMAGE] // docker push [IMAGE]

// Containers
docker run
docker ps // docker ps -a, docker ps -l
docker stop/start/restart [CONTAINER]
docker stats [CONTAINER]
docker top [CONTAINER]
docker port [CONTAINER]
docker inspect [CONTAINER]
docker inspect -f "{{ .State.StartedAt }}" [CONTAINER]
docker rm [CONTAINER]

```

---

### examples Docker 

- SSH into a container
- Build an image
- Docker [Volume](https://docs.docker.com/engine/userguide/containers/dockervolumes/)
- [Linked](https://docs.docker.com/engine/userguide/networking/default_network/dockerlinks/) containers
- Using [docker-compose](https://docs.docker.com/compose/)
- Scale containers with docker-compose
- Share an image (share this presentation)
- Package an app with its environment
- Screen and sound within containers (x-forward)

---

### Example: SSH into a container


```
docker pull ubuntu
docker run -it --name ubuntu_example ubuntu /bin/bash
```

---

### Example: 2 mysql 2 phpmyadmin

https://hub.docker.com/r/phpmyadmin/phpmyadmin/
https://hub.docker.com/_/mysql/

```
curl -sSL https://get.docker.com/ | sh
mkdir -p /opt/mysql
docker run --name mysql  -v /opt/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=pass_here -p 3306:3306 -d mysql
docker run --name phpmyadmin --link mysql:db -p 8080:80   -d phpmyadmin/phpmyadmin 
mkdir -p /opt/mysql2
```
link the tow bd using phpmyadmin

---

### Example: Docker compose + wordpress

https://www.digitalocean.com/community/tutorials/how-to-install-wordpress-and-phpmyadmin-with-docker-compose-on-ubuntu-14-04

```

mkdir ~/wordpress && cd $_

nano ~/wordpress/docker-compose.yml






wordpress:
  image: wordpress
  links:
    - wordpress_db:mysql
  ports:
    - 8080:80
wordpress_db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: examplepass
phpmyadmin:
  image: corbinu/docker-phpmyadmin
  links:
    - wordpress_db:mysql
  ports:
    - 8181:80
  environment:
    MYSQL_USERNAME: root
    MYSQL_ROOT_PASSWORD: 



 docker-compose up -d
```

---


### Example: mysql cluster 

https://en.wikipedia.org/wiki/MySQL_Cluster

https://hub.docker.com/r/h3nrik/mysql-cluster/

https://github.com/g17/MySQL-Cluster.git

https://dev.mysql.com/doc/refman/5.7/en/mysql-cluster-install-configuration.html

```
git clone https://github.com/g17/MySQL-Cluster.git
cd MySQL-Cluster
docker build -t h3nrik/mysql-cluster .


1-

[NDBD DEFAULT]
NoOfReplicas=2
DataMemory=80M
IndexMemory=18M
datadir=/usr/local/mysql/data

[NDB_MGMD DEFAULT]
datadir=/var/lib/mysql-cluster

[NDB_MGMD]
NodeId=1
hostname=192.168.0.1

[NDBD]
NodeId=10
hostname=192.168.0.10

[NDBD]
NodeId=11
hostname=192.168.0.11

[MYSQLD]
NodeId=100
hostname=192.168.0.100

[MYSQLD]
NodeId=101
hostname=192.168.0.101
#Usage


 docker run -d --name ndb_mgmd01 --net=host -p 192.168.0.1:1186:1186 -v /path/to/your/config.ini:/etc/mysql-cluster.ini:ro h3nrik/mysql-cluster ndb_mgmd

 docker run -it --rm --name ndb_mgm h3nrik/mysql-cluster ndb_mgm 192.168.0.1

 docker run -d --name ndbd01 --net=host h3nrik/mysql-cluster ndbd 192.168.0.1
 docker run -d --name ndbd02 --net=host h3nrik/mysql-cluster ndbd 192.168.0.1


 docker run -d --name mysqld01 --net=host -p 192.168.0.100:3306:3306 h3nrik/mysql-cluster mysqld 192.168.0.1
 docker run -d --name mysqld02 --net=host -p 192.168.0.101:3306:3306 h3nrik/mysql-cluster mysqld 192.168.0.1

```

---

