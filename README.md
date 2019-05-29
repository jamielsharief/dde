# Dockerized Development Environment (PHP)

This is my DDE ripped from my PHP framework [OriginPHP](https://www.originphp.com)

It has the following

 - Php
 - MySQL
 - Memcache
 - Redis
 - PostgreSQL
 - XDebug
 - PHPUnit
 - Composer

## Installation

Install [Docker Desktop](https://www.docker.com/products/docker-desktop)

Go to your project run the composer require command.

```
$ cd <folder>
$ composer require jamielsharief/dde
```

First you will need to build the container

```linux
$ docker-compose build
```

Then start the container

```linux
$ docker-compose up
```

You can now access the server at [http://localhost:8000](http://localhost:8000).

To access the MySQL client you will first need to access the Docker container, then connect using the hostname `db` since the database server is also run in a Docker container. 

If you want to access MySQL from your computer (not from within the Docker container) such as with MySQL admin program or a locally installed MySQL client then use localhost and port 3306.

> Inside the contianer the MySQL server hostname is db not localhost

To access the Docker container

```linux
$ docker-compose run app bash
```

To run the MySQL client

```linux
$ mysql -h db -uroot -p
```

The username is `root` and password is `root`.

> Change the password in the docker files if you are thinking of deploying this container.

To shutdown the Docker container:

```linux
$ docker-compose down
```

Any questions or suggestions, use the [https://github.com/jamielsharief/dde/issues](https://github.com/jamielsharief/dde/issues).