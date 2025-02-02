# Revere Riders Website

## Tools

To initialize environment following tools are necessary

1. Visual Studio Code is recommended
2. VS Code mySql extension
3. Git Bash
4. Docker desktop
5. Docker images for mysql and wordpress

<a href="[url](https://hub.docker.com/_/wordpress)">Docker Wordpress</a>

<a href="[url](https://hub.docker.com/_/mysql)">Docker mySql</a>

## Docker Compose notes

To build the app from terminal execute: 

<pre>docker compose up --build</pre>

The <b>ports</b> configuration opens a local port 8080 and redirects it to 80</br>

<b>Volumes</b> tells docker to use local directory nginx and override inside docker the directory /etc/nginx and override the conf.d file with the default.conf file in local directory nginx</br>

<b>Wordpress docker image fpm: </b>includes docker configuration telling it how to execute php code without us needing to configure a lot of that plumbing on our own. The fpm image comes with php working out of the box

## All notes below are for manual installation without use of docker-compose 

### Docker

Steps to obtain wordpress docker and start it on your local machine:

1. docker pull mysql:latest
2. docker pull wordpress:php8.3-apache
3. docker images
4. docker network create my-network
5. docker run -d --name mysql --network my-network -p 3306:3306 -e MYSQL_ROOT_PASSWORD=secret -e MYSQL_DATABASE=mySchema mysql:latest
6. docker run -d --name wordpress --network my-network -p 8080:80 wordpress:php8.3-apache 

<b>Note:</b> in the setup for connecting wordpress to mysql you will need to use the "Gateway" IP address, NOT localhost. This is probably going to be 172.18.0.1, but you can verify in docker desktop via inspecting the container and selecting network

Example for starting docker container: 

<pre>
$ docker images

REPOSITORY   TAG             IMAGE ID       CREATED        SIZE
wordpress    php8.3-apache   64694fe21a99   2 months ago   998MB

$ docker run -d --expose 3306 -p 8080:80 wordpress:php8.3-apache 
</pre>

After it's running access via http://localhost:8080
