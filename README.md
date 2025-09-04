# Quick reference
* **Github:**
https://github.com/moodlehq/moodle-docker

# Getting started
First, create a new env file:
```
# Set the path to Moodle code directory
export MOODLE_DOCKER_WWWROOT=/path-to/moodle-code
# Set the path to Moodle data directory
export MOODLE_DOCKER_MOODLEDATA=/path-to/moodle-data
# Choose a db server
export MOODLE_DOCKER_DB=mysql
# Database flavour
# MOODLE_DOCKER_DB_VERSION=5.7
# Set the path to MySQL data directory
export MOODLE_DOCKER_MYSQLDATA=/path-to/mysql-data
# PHP version.
export MOODLE_DOCKER_PHP_VERSION=8.4

```
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
    # Add 'platform' for MySQL 5.7 on Apple Silicon
    # platform: linux/x86_64
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
mkdir moodle-code ; mkdir moodle-data ; mkdir mysql-data
source env.moodle-docker
```
```
bin/moodle-docker-compose -f docker-compose.override.yml up -d
```
or use local.yml
```
bin/moodle-docker-compose up -d
```


Access it via `http://localhost:8080`
