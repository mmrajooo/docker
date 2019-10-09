# From Debian Latest
FROM debian:latest

LABEL maintainer="MMRAJOO"

# Install NGINX Plus
RUN set -x \
  && apt-get update && apt-get upgrade -y \
  && apt-get install -y apt-utils \
  && apt-get install -y apt-transport-https ca-certificates dialog tzdata procps \
  && echo "America/New_York" > /etc/timezone \
  && dpkg-reconfigure -f noninteractive tzdata \
  && apt-get install -y nginx-extras transmission-daemon gpg vim rsync \
  && apt-get install -y onionbalance dyndns libnet-dns-cloudflare-ddns-perl \
  && apt-key adv --keyserver  keyserver.ubuntu.com --keyserver-options timeout=10 --recv-keys EAF9B4E3C0145138 \
  && echo "deb http://moblock-deb.sourceforge.net/debian stretch main"      > /etc/apt/sources.list.d/pgl.list \
  && echo "deb-src http://moblock-deb.sourceforge.net/debian stretch main" >> /etc/apt/sources.list.d/pgl.list \ 
  && apt-get update && apt-get install -y pgld pglcmd
  
# Forward request logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80
EXPOSE 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
