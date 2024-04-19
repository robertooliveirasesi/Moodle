# Roteiro de instalação do Moodle por linha de comando

## 1. Criação dos Volumes

### 1.1 Criação do volume do banco de dados
docker volume create vol-mysql-db

### 1.2 Criação do volume da aplicação
docker volume create vol-moodle-app

## 2. Criação do conteiner do banco de dados a partir da imagem do mysql8.0

docker run -d --name moodle-db -p 3306:3306 --mount src=vol-mysql-db,dst=/var/lib/mysql -e MYSQL_ROOT_PASSWORD="moodle" -e MYSQL_DATABASE="moodle" -e MYSQL_USER="moodle_user" -e MYSQL_PASSWORD="moodle_pass" mysql:8.0

## 3. Criação da imagem do moodle a partir do Dockerfile
docker build -t moodle:4.2 .

Certifique-se de estar na mesma pasta do arquivo Dockerfile ou apontar para a pasta correta.

## 4. Criação do conteiner do moodle da imagem criada acima
docker run -d --name moodle-app -p 9090:80 --mount src=vol-moodle-app,dst=/var/www/moodledata -e MOODLE_DATABASE_NAME="moodle" -e MOODLE_DATABASE_USER="moodle_user" -e MOODLE_DATABASE_PASSSWORD="moodle_pass" -e MOODLE_DATABASE_HOST="moodle-man-db" moodle:4.2

## 5. Instalação do Moodle
No navegador de sua preferência digite: http://localhost:9090/install.php

### 5.1. A tela abaixo será mostrada:
![image](https://github.com/robertooliveirasesi/Moodle/assets/166535151/ef486dea-b245-438c-a22b-6179e7aec263)

--> Selecione o idioma desejado e clique no botão "Next" ou "Próximo"

### 5.2. A tela abaixo será mostrada:
![image](https://github.com/robertooliveirasesi/Moodle/assets/166535151/cd11a50f-946f-4c28-be8f-25a3a5a775af)

--> Clique no botão "Next" ou "Próximo"

### 5.3. Selecione o tipo do banco de dados que foi instalado:

![image](https://github.com/robertooliveirasesi/Moodle/assets/166535151/ab715e15-f0b7-4dc6-9f91-24a559c26522)

--> Clique no botão "Next" ou "Próximo"

### 5.4. Preencha as informações:

![image](https://github.com/robertooliveirasesi/Moodle/assets/166535151/c7f5b803-4543-463f-8239-08735814d711)

--> Preencha: Host do banco de dados; Nome do banco de dados; Usuário do banco de dados; e prefixo das tabelas "mdl_" (Valor fixo)

Se tudo estiver correto, a tela a seguir será mostrada:
![image](https://github.com/robertooliveirasesi/Moodle/assets/166535151/d9042475-0035-4c80-99a4-bf03772b69e7)

Obs: Confirme no conteiner do banco em qual IP ele está rodando.

--> Clique no botão "Next" ou "Continuar"

A tela a seguir será mostrada:

![image](https://github.com/robertooliveirasesi/Moodle/assets/166535151/202514e7-4b90-4ed6-8a2f-c0a661a32978)

Se o servidor atender à todos os requisitos da versão do Moodle, todos os STATUS devem estar "OK" ou "Verificar". Caso contrário a instalação não proseguirá até que essas condições sejam satisfeitas

--> Clique no botão "Next" ou "Continuar"



