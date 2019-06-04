FROM nginx:latest
WORKDIR /
RUN apt-get update && apt-get upgrade
RUN yes | apt install apt-transport-https lsb-release ca-certificates
RUN yes | apt-get install -y wget 
RUN wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
RUN echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list
RUN apt-get update
RUN yes | apt-get install -y php7.2-cli php7.2-pdo php7.2-mysql
RUN yes | apt-get install -y supervisor
RUN yes | apt-get install curl
COPY ["queue-worker.conf", "/etc/supervisor/conf.d/queue-worker.conf"]
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
RUN touch /var/run/supervisor.sock
RUN chmod 777 /var/run/supervisor.sock
RUN supervisorctl start 