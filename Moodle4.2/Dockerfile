# Use a imagem oficial do PHP com Apache como base
FROM php:8.0-apache

# Atualize e instale as dependências necessárias
RUN apt-get update && apt-get install -y \
    wget \
    git \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    libzip-dev \
    unzip \
    libicu-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) gd mysqli opcache zip intl 

# Especifica configurações do PHP necessárias para o Moodle
# php.ini
RUN set -ex \
    && { \
        echo 'log_errors = on'; \
        echo 'display_errors = off'; \
        echo 'always_populate_raw_post_data = -1'; \
        echo 'cgi.fix_pathinfo = 1'; \
        echo 'session.auto_start = 0'; \
        echo 'upload_max_filesize = 128M'; \
        echo 'post_max_size = 150M'; \
        echo 'max_execution_time = 1800'; \
        echo 'max_input_vars = 5000'; \
        echo '[opcache]'; \
        echo 'opcache.enable = 1'; \
        echo 'opcache.memory_consumption = 128'; \
        echo 'opcache.max_accelerated_files = 8000'; \
        echo 'opcache.revalidate_freq = 60'; \
        echo 'opcache.use_cwd = 1'; \
        echo 'opcache.validate_timestamps = 1'; \
        echo 'opcache.save_comments = 1'; \
        echo 'opcache.enable_file_override = 0'; \ 
    } | tee /usr/local/etc/php/conf.d/php.ini

WORKDIR /var/www/html

# Baixar e extrair o Moodle 4.2
RUN git clone -b MOODLE_402_STABLE --depth 1 git://git.moodle.org/moodle.git /var/www/html

#Dar permissões de usuário a pasta
RUN chown www-data.www-data /var/www/html -R

# Baixe e instale os plugins  ## Aqui ele pede usuário e senha do github para baixar os plugins
RUN git clone -b v4.3.3 --depth 1 https://github.com/lmsace/academi /var/www/html/theme/academi \
    && git clone -b 2.1.2 --depth 1 https://github.com/Limekiller/moodle-block_openai_chat /var/www/html/blocks/openai_chat \
    && git clone -b moodle42b --depth 1 https://bitbucket.org/dw8/moodle-format_tiles/src/master/ /var/www/html/course/format/tiles \
    && git clone -b v4.2.4 --depth 1 https://github.com/markn86/moodle-mod_customcert mod/customcert


# Cria o diretório de arquivos do Moodle e dá permissões
RUN mkdir /var/www/moodledata && \ 
chmod 0770 /var/www/moodledata -R

#Dá permissões de usuario a pasta moodledata
RUN chown www-data /var/www/moodledata -R

# Definir as permissões corretas
RUN chown -R www-data:www-data /var/www/html && \
    chmod -R 755 /var/www/html

# Exponha a porta 80
EXPOSE 80

#habilita o CRON
RUN echo "*/1 * * * * root php -q -f /var/www/html/moodle/admin/cli/cron.php > /var/log/moodle_cron.log" >> /etc/crontab

# Comando para iniciar o Apache
CMD ["apache2-foreground"]

