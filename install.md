# Roteiro de instalação do Moodle por linha de comando

## 1. Criação dos Volumes

### 1.1 Criação do volume do banco de dados
docker volume create vol-mysql-db

### 1.2 Criação do volume da aplicação
docker volume create vol-moodle-app

## 2. Criação do conteiner do banco de dados

docker run -d --name moodle-man-db -p 3306:3306 --mount src=vol-db,dst=/var/lib/mysql -e MYSQL_ROOT_PASSWORD="moodle" -e MYSQL_DATABASE="moodle" -e MYSQL_USER="moodle_user" -e MYSQL_PASSWORD="moodle_pass" mysql:8.0
