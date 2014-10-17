FROM phusion/baseimage
MAINTAINER Michael A. Smith <msmith3@ebay.com>
RUN apt-get -qqy update && apt-get -qqy install trafficserver && mkdir -p /var/run/trafficserver
COPY records.config /etc/trafficserver/records.config
COPY ts /usr/local/bin/ts
RUN chmod +x /usr/local/bin/ts
EXPOSE 8000
CMD /usr/local/bin/ts
