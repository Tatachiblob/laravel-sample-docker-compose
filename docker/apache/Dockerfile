FROM centos:centos7

LABEL maintainer="Yuta <yuta_inoue@commude.ph>"

# update yum
RUN yum -y update && \
    yum -y install yum-utils && \
    yum clean all

# install apache
RUN yum install -y httpd

# install php73
RUN yum -y install wget curl zip unzip file && \
    yum -y install http://rpms.remirepo.net/enterprise/remi-release-7.rpm && \
    yum -y install epel-release yum-utils && \
    yum-config-manager --disable remi-php54 && \
    yum-config-manager --enable remi-php73 && \
    yum -y install php \
        php-opcache \
        php-cli \
        php-fpm \
        php-mysqlnd \
        php-zip \
        php-devel \
        php-gd \
        php-exif \
        php-redis \
        php-mcrypt \
        php-mbstring \
        php-curl \
        php-session \
        php-tokenizer \
        php-iconv \
        php-xml \
        php-pear \
        php-bcmath \
        php-json && \
    yum clean all

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer --version=1.9.3

# Set configuration files
COPY ./conf/httpd.conf /etc/httpd/conf
COPY ./conf/php.ini /etc

RUN mkdir -p /var/www/html/public

EXPOSE 80

CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
