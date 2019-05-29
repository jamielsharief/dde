# Dockerized Development Environment (PHP)

This is my DDE ripped from my PHP framework [OriginPHP](https://www.originphp.com)


## Installation

Install [Docker Desktop](https://www.docker.com/products/docker-desktop)

Copy the files into the root directory of your project.

First you need to build the container

```linux
$ docker-compose build
```

Then start the container

```linux
$ docker-compose up
```

You can now access the server at [http://localhost:8000](http://localhost:8000).

To access container.

To access the MySQL client you will first need to access the container, then connect using the hostname db since the database is also run in a docker container. If you want to access MySQL from your computer (not from within the contianer) then use localhost. 

> Inside the contianer the MySQL server hostname is db not localhost

To access the container

```linux
$ docker-compose run app bash
```

To run the MySQL client

```linux
$ mysql -h db -uroot -p
```

The username is `root` and password is `root`.

> Change the password in the docker files if you are thinking of deploying this container.

To shutdown 

```linux
$ docker-compose down
```