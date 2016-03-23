FROM php:5.6.19-cli

MAINTAINER Pedro Maia "pedromaia@dialhost.com.br"

RUN apt-get -y update && \
    apt-get -y install openssh-server \
        openjdk-7-jdk

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
        ext-mbstring \
    && docker-php-ext-install -j$(nproc) iconv mcrypt \
    && docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
    && docker-php-ext-install -j$(nproc) gd

RUN echo "root:password" | chpasswd  && \
    useradd jenkins -m && \
    echo "jenkins:jenkins" | chpasswd
  
RUN mkdir -p /var/run/sshd && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd

RUN rm -rf /var/lib/apt/lists/*
  
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

RUN curl -sS https://getcomposer.org/installer | php && \
    mv composer.phar /usr/local/bin/composer

CMD ["/usr/sbin/sshd", "-D"]