FROM ubuntu:15.04

MAINTAINER Pedro Maia "pedromaia@dialhost.com.br"

RUN DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && \
    apt-get -y install openssh-server \
        openjdk-7-jdk

RUN echo "root:password" | chpasswd && \
    useradd jenkins -m && \
    echo "jenkins:jenkins" | chpasswd

RUN mkdir -p /home/jenkins/.ssh && \
    chown -R jenkins:jenkins /home/jenkins/.ssh
  
RUN mkdir -p /var/run/sshd && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd

RUN rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64

CMD ["/usr/sbin/sshd", "-D"]