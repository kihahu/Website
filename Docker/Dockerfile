FROM ubuntu:14.04
# Install dependencies
RUN apt-get update -y
RUN apt-get install -y git curl apache2 php5 libapache2-mod-php5 php5-mcrypt php5-mysql libapache2-mod-php5
RUN a2enmod rewrite
RUN chown -R www-data:www-data /var/www
ENV APACHE_RUN_USER www-data
ENV APACHE_RUN_GROUP www-data
ENV APACHE_LOG_DIR /var/log/apache2


RUN mkdir -p /root/.ssh

RUN echo "Host github.com\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config

RUN /usr/bin/ssh-keyscan github.com >> /root/.ssh/known_hosts

RUN rm -rf /var/www/html/
RUN mkdir -p /var/www/html/

RUN /usr/bin/git clone https://github.com/yiisoft/yii.git /var/www/yii
ADD apache.conf /etc/apache2/sites-enabled/000-default.conf
COPY supervisord.conf /etc/supervisord.conf

RUN chown -R www-data.www-data /var/www/html/

EXPOSE 22 80 443
CMD ["supervisord", "-c", "/etc/supervisord.conf"]
