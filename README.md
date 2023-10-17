# Lobste.rs-Edna

## About

This repo contains a working example of how to use and deploy [Lobsters][lobsters] within a Docker environment, running with Edna support.
This image is built off of the official Ruby Docker image ([ruby:2.7-alpine][ruby-alpine])

## Quick Start

Using this repository.  
This will serve up Lobsters at `http://localhost:3000`

```shell
git clone git@github.com:tslilyai/docker-lobsters-edna.git
cd docker-lobsters
git submodule update --init --recursive
make
docker-compose up
```

To generate fake data:
```
docker exec -ti docker-lobsters-edna_app_1 /bin/bash
./bin/rails fake_data
```

## Use DockerHub
(Warning: untested)

Using the prebuilt docker hub build and official [MariaDB image][mariadb image].  
This will serve up Lobsters at http://localhost:3000/

```shell
docker run --name lobsters -v lobsters_data:/var/lib/mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=lobsters -d mariadb
docker run -p 3000:3000 --link lobsters:mariadb tslilyai/lobsters
```


[lobsters]: https://github.com/lobsters/lobsters
[ruby-alpine]: https://hub.docker.com/_/ruby/
[mariadb image]: https://hub.docker.com/_/mariadb/
