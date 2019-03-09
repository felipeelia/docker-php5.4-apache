# A Apache+PHP5.4 docker image (for tests purpose only)

Based on the [10up legacy image](https://github.com/10up/Docker-Images/tree/master/legacy/php/5.4/apache).

----

## Instructions

The text below is just a suggestion. You can adapt this to whatever you want :)

In project root directory, you'll have to create
1. Two folders:
    * `dev`: you'll use this folder to keep your PHP files. It'll be mapped to apache's `/var/www/html`
    * `db_data`: docker will use this folder to keep your MariaDB data.

2. A `docker-compose.yml` file with this content:
```
version: '3'

services:
  wordpress:
    build: https://github.com/felipeelia/docker-php5.4-apache.git
    links:
      - mysql
    ports:
      - 80:80
    volumes:
      - ./dev/:/var/www/html

  mysql:
    image: mariadb
    volumes:
      - ./db_data/:/var/lib/mysql
    ports:
     - 3306:3306
    environment:
      MYSQL_ROOT_PASSWORD: wordpress
      MYSQL_DATABASE: wordpress
      MYSQL_USER: wordpress
      MYSQL_PASSWORD: wordpress

volumes:
    db_data:
```

Run `docker-compose up` in the project root and docker will build the image. It'll take a while for the first time, but it'll be cached for the next time.

DO NOT use this image for production.
