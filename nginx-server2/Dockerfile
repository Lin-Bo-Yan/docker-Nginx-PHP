FROM nginx:1.23.1
COPY ./conf.d/default.conf /etc/nginx/conf.d/default.conf
USER root
RUN ["apt", "update"]
RUN ["apt-get", "update"]
RUN ["apt", "install","net-tools"]
RUN ["apt-get", "install","lsof"]
RUN apt-get install -y --force-yes iputils-ping
RUN apt-get install telnetd -y