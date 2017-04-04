FROM ubuntu:14.04.5
ADD cnc /
ADD db.sql /
RUN apt-get -y update \
	&& echo "#!/bin/sh\nexit 0" > /usr/sbin/policy-rc.d \
	&& apt-get install -y debconf-utils \
    && echo mysql-server mysql-server/root_password password root | debconf-set-selections \
    && echo mysql-server mysql-server/root_password_again password root | debconf-set-selections \
    && apt-get install -y mysql-server -o pkg::Options::="--force-confdef" -o pkg::Options::="--force-confold" --fix-missing \
    && apt-get install -y mysql-client \
    && mysql -u root -p"root" < /db.sql
CMD service mysql start \
	&& /cnc
EXPOSE 23
