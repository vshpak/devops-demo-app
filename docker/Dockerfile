FROM ubuntu:20.04

RUN apt-get update
RUN apt-get install -y nginx

ADD docker nginx.conf /etc/nginx/nginx.conf
#ADD ./www /www

EXPOSE 80
CMD ["nginx"]