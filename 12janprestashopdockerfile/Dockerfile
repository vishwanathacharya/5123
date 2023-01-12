FROM ubuntu:latest
MAINTAINER vishwanathacahrya14@gmail.com
ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /var/www/html/
RUN chmod +x /var/www/html/
#RUN apt-get install -y apache2
RUN apt-get update && apt-get install -y apt-utils 2>&1 | \
    grep -v "^debconf: delaying package configuartion, since apt-utils.*"
RUN apt-get update && apt-get install -y openssh-server apache2 supervisor
RUN mkdir -p /var/lock/apache2 /var/run/apache2 /var/run/sshd /var/log/supervisor
RUN apt-get install -y apache2 
RUN apt-get install -y postfix 
RUN apt-get install -y software-properties-common 
RUN add-apt-repository ppa:ondrej/php -y 
RUN apt-get update
RUN apt-get install -y php7.3 php7.3-cli php7.3-zip php7.3-json php7.3-common php7.3-mysql  php7.3-gd php7.3-mbstring php7.3-curl php7.3-xml php7.3-bcmath php7.3-simple php7.3-intl libapache2-mod-php7.3 
RUN apt-get install -y mysql-server
RUN service mysql start && mysql -uroot mysql -e "alter user 'root'@localhost identified with mysql_native_password by 'password';create database db;FLUSH PRIVILEGES;"
RUN apt-get install -y curl
RUN apt-get install -y unzip
RUN apt-get install -y wget
#RUN curl -LO https://www.prestashop.com/en/system/files/ps_releases/prestashop_1.7.8.8.zip
#RUN wget https://download.prestashop.com/download/releases/prestashop_1.7.7.4.zip
#RUN unzip prestashop_1.7.7.4.zip && unzip prestashop.zip
COPY info.php /var/www/html/
COPY prestashop/ /var/www/html/
COPY prestashop.sh /usr/sbin/
#COPY prestashop.conf /etc/apache2/sites-available/
#RUN a2dissite 000-default.conf
#RUN a2ensite prestashop.conf
RUN chown -R www-data:www-data /var/www/html/
RUN chmod -R 755 /var/www/html/
#RUN apt-get install -y supervisor
RUN a2enmod rewrite
#COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
#EXPOSE 22 80
#CMD ["/usr/bin/supervisord"]
CMD ["/usr/sbin/prestashop.sh"]
