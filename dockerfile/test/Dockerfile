FROM centos/php-70-centos7

ENV COMPOSER_INSTALLER=https://install.phpcomposer.com/installer
RUN curl $COMPOSER_INSTALLER | php

USER 0

ENV TZ=Asia/Shanghai
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN chmod +x composer.phar
RUN mv composer.phar /usr/local/bin/composer
RUN wget https://phar.phpunit.de/phploc.phar
RUN chmod +x phploc.phar
RUN mv phploc.phar /usr/local/bin/phploc

RUN yum -y install rh-php70-php-pecl-redis rh-php70-php-pecl-xdebug sclo-php72-php-pecl-memcached
RUN yum -y install openssh-server

COPY sshd_config /etc/ssh/sshd_config
COPY etc/15-xdebug.ini /etc/opt/rh/rh-php70/php.d/15-xdebug.ini

RUN useradd -rm -d /opt/app-root -s /bin/bash -g root -u 1000 dev

RUN echo "root:root" | chpasswd

RUN ssh-keygen -A

COPY run $STI_SCRIPTS_PATH/run

WORKDIR /opt/app-root/

CMD $STI_SCRIPTS_PATH/run


