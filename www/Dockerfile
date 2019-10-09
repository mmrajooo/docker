# From Debian Latest
FROM debian:latest

LABEL maintainer="MMRAJOO"

# Install NGINX Plus
RUN set -x \
  && apt-get update && apt-get upgrade -y \
  && apt-get install -y apt-transport-https ca-certificates nginx-extras dialog tzdata transmission-daemon gpg vim rsync \
  && apt-get install -y procps onionbalance dyndns libnet-dns-cloudflare-ddns-perl \
  && echo "America/New_York" > /etc/timezone \
  && dpkg-reconfigure -f noninteractive tzdata \
  && gpg --keyserver keyserver.ubuntu.com --recv-keys EAF9B4E3C0145138 \
  PGL_GPGKEY=EAF9B4E3C0145138; \
  found=''; \
  for server in \
    ha.pool.sks-keyservers.net \
    hkp://keyserver.ubuntu.com:80 \
    hkp://p80.pool.sks-keyservers.net:80 \
    pgp.mit.edu \
  ; do \
    echo "Fetching GPG key $PGL_GPGKEY from $server"; \
    apt-key adv --keyserver "$server" --keyserver-options timeout=10 --recv-keys "$PGL_GPGKEY" && found=yes && break; \
  done; \
  test -z "$found" && echo >&2 "error: failed to fetch GPG key $PGL_GPGKEY" && exit 1; \
  && echo "deb http://moblock-deb.sourceforge.net/debian stretch main"      > /etc/apt/sources.list.d/pgl.list  \
  && echo "deb-src http://moblock-deb.sourceforge.net/debian stretch main" >> /etc/apt/sources.list.d/pgl.list  \
  && apt-get update && apt-get install -y pgld pglcmd 
  
# Forward request logs to Docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
  && ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80
EXPOSE 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
