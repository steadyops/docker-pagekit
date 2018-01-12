# Pagekit CMS Docker image
Docker image for Pagekit CMS. Based on php:7.2.1-cli-alpine3.7

# Note

### TO BE USED IN DEVELOPMENT MODE ONLY!!

This is a minimal image for development, it uses php's built-in server on port 10000. The image size is less than 95 MB.

Everytime a container is newly created you will have go through Pagekit set-up wizard (map config.php to container to avoid this)

Personally I find it easier to have such a light weight container, I even use sqlite only for development.

# How to use

### using docker run

This is the fastest option, you can use Sqlite as a DB

```
docker run --name pagekit -d -p 10000:10000 steadyops/docker-pagekit
```

### using docker compose

```
version: '3.1'

services:

  php-pagekit:
    image: pagekit
    restart: always
    ports:
      - 10000:10000
    volumes:
        - /your/path/to/pagekit-extensions-or-themes/:/var/www/html/packages/

  db:
    image: mariadb:10.3
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example
    volumes:
      - pagekit_db:/var/lib/mysql/
      
  volumes:
    pagekit_db:

```
