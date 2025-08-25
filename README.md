# Quick reference
* **Github:**
https://github.com/moodlehq/moodle-docker

# Getting started
First, create a new env file:
# Environment variables

Variable | Value | Description
--- | --- | ---
*MOODLE_DOCKER_WWWROOT* | `/path-to/moodle-code` | **Set the path to Moodle code directory**
*MOODLE_DOCKER_MOODLEDATA* | `/path-to/moodle-data` | **Set the path to Moodle data directory**
*MOODLE_DOCKER_DB* | `mysql` | **Set the database server**
*MOODLE_DOCKER_MYSQLDATA* | `/path-to/mysql-data` | **Set the path to MySQL data directory**
*MOODLE_DOCKER_PHP_VERSION* | `8.4` | **PHP version**

## Run the application using `moodle-docker-compose` and `docker-compose.override` or `local.yml`
```
# Example docker-compose.override.yml/local.yml
services:
  webserver:
    volumes:
      - "${MOODLE_DOCKER_MOODLEDATA}:/var/www/moodledata"  
  db:
    ports:
      - 127.0.0.1:3384:3306
    volumes:
      - "${MOODLE_DOCKER_MYSQLDATA}:/var/lib/mysql"
  exttests:
    profiles:
      - donotstart
  selenium:
    profiles:
      - donotstart 
```
### Usage
```
source env.moodle-docker
```
```
bin/moodle-docker-compose -f docker-compose.override.yml up -d
```
or local.yml if found
```
bin/moodle-docker-compose up -d
```


Access it via `http://localhost:8080`
