FROM node:5.9.1

MAINTAINER Pedro Maia "pedromaia@dialhost.com.br"

RUN DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && \
    apt-get -y install openssh-server \
        openjdk-7-jdk \
        git

RUN echo "root:password" | chpasswd && \
    useradd jenkins -m && \
    echo "jenkins:jenkins"
  
RUN mkdir -p /var/run/sshd && \
    sed -i 's|session    required     pam_loginuid.so|session    optional     pam_loginuid.so|g' /etc/pam.d/sshd

CMD ["/usr/sbin/sshd", "-D"]