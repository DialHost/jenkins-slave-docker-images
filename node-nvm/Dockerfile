FROM ubuntu:15.04

MAINTAINER Pedro Maia "pedromaia@dialhost.com.br"

RUN DEBIAN_FRONTEND=noninteractive

RUN rm /bin/sh && \
    ln -s /bin/bash /bin/sh

RUN apt-get -y update && \
    apt-get -y install openssh-server \
        openjdk-7-jdk \
        git \
        curl

RUN echo "root:password" | chpasswd  && \
    useradd jenkins -m && \
    echo "jenkins:jenkins" | chpasswd
  
RUN mkdir -p /var/run/sshd && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd

RUN git clone git@github.com:creationix/nvm.git /opt/nvm && \
    mkdir /usr/local/nvm && \
    mkdir /usr/local/node

COPY ./nvm.sh /etc/profile.d/

RUN rm -rf /var/lib/apt/lists/*
  
ENV HOME /root
ENV NODE_VER v5.9.0
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

CMD ["/usr/sbin/sshd", "-D"]