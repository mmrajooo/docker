# From Debian Latest
FROM debian:latest

LABEL maintainer="MMRAJOO"

# Install SSH HOST SYSTEM
RUN set -x \
  && apt-get update && apt-get install apt-utils && apt-get upgrade -y \
  && apt-get install -y apt-transport-https ca-certificates nginx-extras dialog tzdata transmission-daemon gpg vim rsync \
  && apt-get install -y procps onionbalance dyndns libnet-dns-cloudflare-ddns-perl \
  && echo "America/New_York" > /etc/timezone \
  && dpkg-reconfigure -f noninteractive tzdata
  
# Forward request logs to Docker log collector
#RUN ln -sf /dev/stdout /var/log/nginx/access.log \
#  && ln -sf /dev/stderr /var/log/nginx/error.log

#EXPOSE 80
#EXPOSE 443

STOPSIGNAL SIGTERM

CMD ["nginx", "-g", "daemon off;"]
