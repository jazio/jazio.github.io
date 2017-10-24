============================================================

Docker.

============================================================


# Get docker container [DOCKER_ACCOUNT]/[PACKAGE]
docker pull wadmiraal/drupal:7.41

# Run docker
docker run -d -p 8083:80 -p 8024:22 -t wadmiraal/drupal

or
```
mkdir -p modules/ themes/
docker run -d -p 8083:80 -p 8024:22 -v `pwd`/modules:/var/www/sites/all/modules/custom -v `pwd`/themes:/var/www/sites/all/themes wadmiraal/drupal
```


#Remove or stop all containers
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)

# Or, build one of your own
1. Create a `Dockerfile`

e.g install nodejs

```
# Based on the Fedora image created by Matthew Miller.
FROM mattdm/fedora:f19
# Install nodejs and npm packages.
RUN yum update -y
RUN yum install -y --skip-broken nodejs npm
# Clean up
RUN yum clean all
# Start a server listening on 8080 using nodejs
ADD . /src
RUN cd /src; npm install
EXPOSE  8080 
CMD ["node", "/src/server.js"]
``` 

# Get into docker
ssh root@localhost -p 8024

# Check available images
docker images

# Remove images
http://stackoverflow.com/questions/17665283/how-does-one-remove-an-image-in-docker



# ====================================================================================================
# This file contains all the commands a user could call on the command line to assemble an image.
# Based on this file and your OS context (local files PATH and URL) the command `docker build Dockerfile` will create a build.
# The build will be run by a component called docker daemon.
# ====================================================================================================

# Pulling repository docker.io/library/debian.
FROM debian:jessie

MAINTAINER Ovi Farcas <farcaso@protonmail.com>
ENV DEBIAN_FRONTEND noninteractive

# Update the repository sources list once more
RUN apt-get update

# Note: In order to effectively utilize the cache keep common instructions at the top of the Dockerfile and only add the alterations at the end.



RUN apt-get install -y \
    vim \
    git \
    apache2 \
    php5-cli \
    php5-mysql \
    php5-gd \
    php5-curl \
    php5-xdebug \
    php5-sqlite \
    libapache2-mod-php5 \
    curl \
    mysql-server \
    mysql-client \
    phpmyadmin \
    wget \
RUN apt-get clean


# Setup PHP.
RUN sed -i 's/display_errors = Off/display_errors = On/' /etc/php5/apache2/php.ini
RUN sed -i 's/display_errors = Off/display_errors = On/' /etc/php5/cli/php.ini




RHEL

# ====================================================================================================
# This file contains all the commands a user could call on the command line to assemble an image.
# Based on this file and your OS context (local files PATH and URL) the command `docker build Dockerfile` will create a build.
# The build will be run by a component called docker daemon.
# ====================================================================================================

FROM registry.access.redhat.com/rhel7:latest 
MAINTAINER Ovi Farcas <farcaso@protonmail.com>


# Update the repository sources list once more
RUN yum clean all -y

# Note: In order to effectively utilize the cache keep common instructions at the top of the Dockerfile and only add the alterations at the end.


RUN yum install -y \
    vim \
    git \
    tar \
    apache2 \
    php5-cli \
    php5-mysql \
    php5-gd \
    php5-curl \
    php5-xdebug \
    php5-sqlite \
    libapache2-mod-php5 \
    curl \
    mysql-server \
    mysql-client \
    phpmyadmin \
    wget \


    RUN a2enmod rewrite

RUN /sbin/service mysqld start; /usr/bin/mysqladmin -u root password "password"; /usr/bin/mysql -uroot -ppassword -e "CREATE DATABASE dev; CREATE USER 'dev'@'localhost' IDENTIFIED BY 'password'; GRANT ALL PRIVILEGES ON dev.* TO 'dev'@'localhost'; FLUSH PRIVILEGES;"



basj file

DOCKER_USER=jazio
DOCKER_IMAGE=fpfis_lamp
PATH_TO_MOUNT=/var/www/html


# to build
docker build --rm=true -t ${DOCKER_USER}/${DOCKER_IMAGE} . < Dockerfile

# to run
docker run -d -p 8080:80 -v ${PATH_TO_MOUNT}:/var/www:ro ${DOCKER_USER}/${DOCKER_IMAGE} /bin/bash -c '/sbin/service mysqld start; /sbin/service httpd start; tail -f /var/log/httpd/error_log &> /dev/null'