FROM debian

ENV DEBIAN_FRONTEND noninteractive

# Update the package repository
RUN apt-get update && apt-get upgrade -y && apt-get install -y wget curl ssh nginx

COPY vhost.conf /etc/nginx/sites-enabled/default
ADD start.sh /start.sh
RUN chmod a+x /start.sh

RUN echo "\ndaemon off;" >> /etc/nginx/nginx.conf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/identity_access.log
RUN ln -sf /dev/stderr /var/log/nginx/identity_error.log

EXPOSE 22 80
ENTRYPOINT ["/start.sh"]
