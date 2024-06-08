FROM php:8-apache

WORKDIR /var/www/html/

COPY . .

EXPOSE 80

RUN chown -R www-data:www-data /var/www

# Adicionando a linha abaixo para garantir permissões de escrita na pasta messages
RUN mkdir -p /var/www/html/messages && chown -R www-data:www-data /var/www/html/messages

# Ou, se a pasta messages já existir no contexto do build, apenas ajustando permissões
# RUN chown -R www-data:www-data /var/www/html/messages
