FROM nginx

ADD nginx.conf /etc/nginx/nginx.conf
ADD sites-enabled/* /etc/nginx/conf.d/
RUN mv /etc/nginx/conf.d/default.conf default.conf.bak
RUN mkdir -p /www-root/html && mkdir -p /www-root/log && mkdir -p /www-root/log/nginx
RUN chown -R www-data.www-data /www-root/html /www-root/log

EXPOSE 80
VOLUME ["/www-root"]