FROM centos:8.3.2011
USER root

# install packages
RUN yum install -y wget git zip dotnet-sdk-3.1

# download necessary files
RUN mkdir -p /web &&\
    wget -P /tmp https://pleasanter.org/downloads/Pleasanter.NetCore_1.1.24.0.zip &&\
    unzip /tmp/Pleasanter.NetCore_1.1.24.0.zip -d /web

# daemonize pleasanter
RUN yum install -y epel-release &&\
    yum install -y supervisor
COPY supervisord.conf /usr/local/etc/supervisord.conf

# init pleasanter
RUN mkdir /web/pleasanter/cmdnetcore
COPY pleasanter.sh /web/pleasanter/cmdnetcore/pleasanter.sh
COPY build.sh /web/pleasanter/cmdnetcore/build.sh
COPY ./init.sh /tmp/init.sh
RUN chmod 744 /web/pleasanter/cmdnetcore/*.sh &&\
    chmod 744 /tmp/init.sh &&\
    /web/pleasanter/cmdnetcore/build.sh

EXPOSE 80
CMD ["/usr/bin/supervisord", "-n", "-c", "/usr/local/etc/supervisord.conf"]