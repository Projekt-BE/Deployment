FROM centos:7
RUN yum update -y
RUN yum install -y httpd
RUN yum install -y openssl
RUN yum install -y mod_ssl
RUN openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout /home/privateKey.key -out /home/certificate.crt -subj "/C=PL/ST=Pomerania/L=Gdansk/O=NqProject/OU=./CN=."
RUN yum install -y epel-release yum-utils
RUN yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm
RUN yum-config-manager --enable remi-php71
RUN yum install -y php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysql php-mbstring php-mysqli php-xml php-zip php-intl mod_ssl git


RUN sed -i 's/^/#&/g' /etc/httpd/conf.d/welcome.conf
RUN sed -i "s/Options Indexes FollowSymLinks/Options FollowSymLinks/" /etc/httpd/conf/httpd.conf

RUN git clone https://github.com/Projekt-BE/Prestashop.git /usr/repo

RUN cp -r /usr/repo/src/* /var/www/html
RUN cp /usr/repo/utils/httpd.conf /etc/httpd/conf/httpd.conf
RUN rm -rf /usr/repo

RUN chown -R apache: /var/www/html

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]

EXPOSE 80
EXPOSE 443
