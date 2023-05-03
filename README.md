# m169p2
DockerImage
  docker compose up -d / docker compose down

services:
  maria:
    image: mariadb
    restart: always
    hostname: maria
    environment:
      - MYSQL_RANDOM_ROOT_PASSWORD=1
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=test
      - MYSQL_PASSWORD_FILE=/run/secrets/pwd
    secrets:
      - pwd
  wp:
    image: wordpress
    restart: always
    hostname: wp
    environment:
      - WORDPRESS_DB_HOST=maria
      - WORDPRESS_DB_USER=test
      - WORDPRESS_DB_NAME=wordpress
      - WORDPRESS_DB_PASSWORD_FILE=/run/secrets/pwd
    ports:
      - "8888:80"
    secrets:
      - pwd
secrets:
  pwd:
    file: pwd.txt
