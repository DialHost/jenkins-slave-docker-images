FROM php:7.0.7-cli

MAINTAINER Pedro Maia "pedromaia@dialhost.com.br"

RUN apt-get -y update && \
    apt-get -y install openssh-server \
        openjdk-7-jdk \
        git \
        wget

RUN apt-get update && apt-get install -y \
        libmcrypt-dev zlib1g-dev && \
    docker-php-ext-install -j$(nproc) pcntl mcrypt mbstring tokenizer zip && \
    docker-php-ext-enable mcrypt zip pcntl

RUN echo "root:password" | chpasswd && \
    useradd jenkins -m && \
    echo "jenkins:jenkins" | chpasswd

RUN mkdir -p /home/jenkins/.ssh && \
    chown -R jenkins:jenkins /home/jenkins/.ssh

RUN mkdir -p /var/run/sshd && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd

RUN rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

RUN wget https://github.com/clue/phar-composer/releases/download/v1.0.0/phar-composer.phar && \
    mv phar-composer.phar /usr/local/bin/composer-phar && \
    chmod +x /usr/local/bin/composer-phar

CMD ["/usr/sbin/sshd", "-D"]