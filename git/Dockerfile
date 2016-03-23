FROM ubuntu

MAINTAINER Pedro Maia "pedromaia@dialhost.com.br"

RUN DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && \
    apt-get -y install openssh-server \
        openjdk-7-jdk \
        git

RUN echo "root:password" | chpasswd  && \
    useradd jenkins && \
    echo "jenkins:jenkins" | chpasswd
  
RUN mkdir -p /var/run/sshd && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd

RUN rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64