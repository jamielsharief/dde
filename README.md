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

Install [Docker Desktop](https://www.docker.com/products/docker-desktop) first.

Copy the `Dockerfile`, `docker-compose.yml` and `apache.conf` to your project root directory and then create a folder called logs, this is where Apache will store the logs, if you do not do this Apache will not start. You can change this in the `apache.conf` file.

## Using the Docker Container

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

## Using PostgreSQL instead of MySQL

Adjust the db node under services in the `docker-compose.yml` file. (Currently MySQL stuff). 
> Don't use tabs in Yaml files.

```yaml
  db:
    image: postgres
    volumes:
      - pg-data:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
    ports:
        - "5432:5432"
```

Change name of the volume in the volumes node so it looks like this

```yaml
volumes:
  pg-data:
```

## Using Redis

To use Redis add the following under the services node after the db node in the  `docker-compose.yml` file.

```yaml
 redis:
    image: redis
```

## Using Memcached

To use Memcached add the following under the services node after the db node in the `docker-compose.yml` file.

```yaml
  memcached:
    image: memcached
```

## Using XDebug

Xdebug is installed, but it causes serious performance issues.

To enable this for the command line access the Docker container, then echo the settings into the cli configuration,
these will be gone next time you restart.

```
$ docker-compose run app bash
$ echo 'zend_extension="/usr/lib/php/20170718/xdebug.so"' >> /etc/php/7.2/cli/php.ini
$ echo 'xdebug.default_enable=0' >> /etc/php/7.2/cli/php.ini
```