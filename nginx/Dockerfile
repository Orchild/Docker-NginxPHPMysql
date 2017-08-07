FROM nginx

COPY nginx.conf /etc/nginx/nginx.conf
COPY sites-enabled/* /etc/nginx/conf.d/
RUN usermod -u 1000 www-data \
    && mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.bak \
    && mkdir -p /www-root/html && mkdir -p /www-root/log && mkdir -p /www-root/log/nginx \
    && chown -R www-data:www-data /www-root/html /www-root/log

EXPOSE 80
VOLUME ["/www-root"]