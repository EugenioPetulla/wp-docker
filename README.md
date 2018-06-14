![wp-docker-logo](https://github.com/EugenioPetulla/wp-docker/blob/master/assets/wp-docker-logo.png)

# Welcome to wp-docker
An handy script that helps you to create and run a docker local environment for WordPress developing.

## Requirements

Only Linux and OSX are fully supported from this script.

First of all you need to install `docker` and `docker-compose` for your OS.  

If you don't know how to do it I strongly recommend to follow the official guide linked below.

- [Install docker](https://docs.docker.com/engine/installation/)  
- [Install docker-compose](https://docs.docker.com/compose/install/)

## What Docker Containers are included?

Actually this is just a script I made in order to make the process of creating a local WordPress environment based on docker less boring and prone to errors. Actually it works well but it's still under developing so the tools included are based on my personal needing. I'm open to suggestions and contribution in order to make wp-docker a complete tool for other WordPress developers.  

[WordPress on Apache](https://hub.docker.com/_/wordpress/), a webserver based on alpine linux capable of switching between different PHP and WordPress versions.

[MariaDB Docker Container](https://hub.docker.com/_/mariadb/), a great and essential MySQL database

[phpMyAdmin](https://hub.docker.com/r/phpmyadmin/phpmyadmin/), optional web interface for MySQL and MariaDB

[WordMove](https://hub.docker.com/r/welaika/wordmove/), optional tool for online deploy that runs in its own separated container.

## How-to

### Basics

Place the script in `/usr/local/bin` folder or execute it directly, it's a simple bash script!!

```bash
  curl https://raw.githubusercontent.com/EugenioPetulla/wp-docker/master/wp-docker -o /usr/local/bin/wp-docker
  chmod +x /usr/local/bin/wp-docker
```


When you run the script it asks you for a project unique name and it will create a folder with the same name. Inside it you can find a `docker-compose.yml` file and a `public` folder that coincides with the root folder of your webserver containing all the WordPress files and directories.

After the setup is completed you can simply point your browser to the desired container. They are mapped like this:

- WordPress is on `localhost:8080` or `0.0.0.0:8080`
- phpMyAdmin is on `localhost:8082` or `0.0.0.0:8082`

You have to stop your project containers before running a new one. This doesn't mean that you have to destroy it, just stop the execution for avoiding network configuration conflicts.

In order to do it you have just to navigate into your project's folder root and type `docker-compose stop`.

In order to restart a stopped composed container just navigate into the project's root folder and type `docker-compose up -d`.

If you want check what containers actually you are running and their informations like names, commands, status and port mapping, just navigate into the project's root folder and type `docker-compose ps`.

If you want to destroy all the project's containers just type `docker-compose down` from the root folder.

### WordMove container how-to

You can find the movefile in the config folder under the root of your project. Edit only the production data and fill it with your production ssh credential.

In order to access to WordMove container and execute its command you have to find the name of the container and then prompt `docker exec -it your_project_wordmove /bin/bash`.

You can find more information on [WordMove usage here](https://github.com/welaika/wordmove/wiki/Usage-and-flags-explained) on the official documentation.

## Changelog

- 3.2: Better folder mapping avoids to be root when using SSH keys with wordmove
- 3.1: Switch to the official welaika/wordmove container
- 3.0: Switch to an updated WordMove container
- 2.2: Add default Movefile
- 2.1: Add WordMove container
- 2.0: Reorder folders
- 1.0: First release
