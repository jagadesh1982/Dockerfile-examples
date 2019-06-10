FROM centos
MAINTAINER jagadish <jagadish.manchala@gmail.com>
LABEL vendor="jagadish" \    
      Version="2.4.6"

ARG user_name=root
USER ${user_name}

WORKDIR /
RUN yum -y install epel-release && \
    yum -y install httpd httpd-tools && \
    yum clean all

VOLUME /var/www/html
RUN rm -rf /etc/httpd/conf/httpd.conf
COPY httpd.conf /etc/httpd/conf/httpd.conf
COPY index.html /var/www/html/
ADD http://www.africau.edu/images/default/sample.pdf /
EXPOSE 8080
HEALTHCHECK --interval=5m --timeout=3s --retries=4 CMD curl -f http://localhost:8080/ || exit 1
ONBUILD RUN mkdir /tmp/tempo
ENV CONTAINER_NAME demoContainer
ENTRYPOINT ["/usr/sbin/httpd"]
CMD ["-D", "FOREGROUND"]
