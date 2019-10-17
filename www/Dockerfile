# From Debian 
FROM debian:buster

LABEL maintainer="MM RAJOOO <https://github.com/mmrajooo/docker>"

RUN set -x \
  && apt-get update \
  && apt-get install -y apt-utils libterm-readline-ttytter-perl tzdata \
  && apt-get install -y apt-transport-https ca-certificates procps \
  && apt-get upgrade -y \
  && echo "America/New_York" > /etc/timezone \
  && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get install -y nginx-extras transmission-daemon gpg dyndns onionbalance libnet-dns-cloudflare-ddns-perl
RUN apt-get install -y openssh-server

RUN mkdir /var/run/sshd

RUN echo 'root:root' |chpasswd

RUN sed -ri 's/^#?PermitRootLogin\s+.*/PermitRootLogin yes/' /etc/ssh/sshd_config
RUN sed -ri 's/UsePAM yes/#UsePAM yes/g' /etc/ssh/sshd_config

VOLUME /home

RUN mkdir /root/.ssh
RUN echo "usenix:usenix:11001:11001::/home/usenix:/bin/bash" | newusers 

RUN apt-get install -y vim rsync git elinks wget curl dnsutils dialog traceroute whois 

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 22
EXPOSE 80
EXPOSE 443

CMD    ["nginx","-g","daemon off;"]

