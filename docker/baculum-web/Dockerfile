FROM gpmidi/bacula-base:latest
MAINTAINER Paulson McIntyre <paul+ftec-bacula@gpmidi.net>
ARG EL_VERSION="8"

RUN rpm --import https://www.bacula.org/downloads/baculum/baculum.pub
COPY baculum.repo /etc/yum.repos.d/baculum.repo

RUN dnf install -y yum-utils
RUN dnf install -y https://rpms.remirepo.net/enterprise/remi-release-$EL_VERSION.5.rpm
RUN yum-config-manager --enable remi
RUN yum install -y \
	sudo \
	php-fpm \
	baculum-common \
	baculum-web \
	baculum-web-httpd \
	supervisor

COPY sudoers-baculum /etc/sudoers.d/sudoers-baculum 
COPY timezone.ini /etc/php.d/timezone.ini
COPY confs/supervisord.conf /etc/supervisord.conf

VOLUME ["/opt/bacula/etc","/etc/baculum"]
EXPOSE 9095/tcp

RUN mkdir -p /run/php-fpm
RUN yum -y clean all && rm -rf /var/cache/yum

CMD ["/usr/bin/supervisord"]
