FROM nginx

ADD nginx.conf /etc/nginx/nginx.conf
ADD sites-enabled/* /etc/nginx/conf.d/
RUN mkdir -p /www-root/htdocs && mkdir -p /www-root/log && mkdir -p /www-root/log/nginx
RUN chown -R www-data.www-data /www-root/htdocs /www-root/log

EXPOSE 80
VOLUME ["/www-root"]