FROM dialhost/jenkins-slaves:nvm

MAINTAINER Pedro Maia "pedromaia@dialhost.com.br"

RUN nvm install v5.9.0 && \
    npm install -g gulp

CMD ["/usr/sbin/sshd", "-D"]