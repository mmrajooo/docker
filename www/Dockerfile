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
RUN apt-get install -y vim rsync git elinks wget curl dnsutils dialog traceroute whois 

VOLUME /etc/nginx
VOLUME /usr/share/nginx

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 80
EXPOSE 443

CMD    ["nginx","-g","daemon off;"]
