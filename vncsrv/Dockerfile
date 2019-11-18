# From Debian 
FROM debian:buster

LABEL maintainer="MM RAJOOO <https://github.com/mmrajooo/docker>"

RUN set -x \
  && apt-get update \
  && apt-get install -y apt-utils libterm-readline-ttytter-perl \
  && apt-get upgrade -y \
  && echo "America/New_York" > /etc/timezone \
  && dpkg-reconfigure -f noninteractive tzdata

RUN apt-get install -y openssh-server supervisor x11vnc openbox fbpanel xserver-xorg xterm fonts-dejavu xfonts-base
RUN apt-get install -y vim rsync git elinks wget curl dnsutils dialog traceroute whois 

# Setup SSH Server ---------
RUN /usr/sbin/sshd-keygen
RUN mkdir /root/.ssh

ADD vnc-server-key.pub /root/.ssh/authorized_keys
RUN chown root:root /root/.ssh/authorized_keys && chmod 600 /root/.ssh/authorized_keys

# Setup minimal X server
ADD openbox.autostart /.config/openbox/autostart
ADD openbox.rc.xml /.config/openbox/rc.xml
RUN mkdir /.config/fbpanel && cp /usr/share/fbpanel/default /.config/fbpanel/default

# Configure supervisord
ADD supervisord.conf /etc/
ADD supervisor.xvfb.conf /etc/supervisord.d/
ADD supervisor.x11vnc.conf /etc/supervisord.d/

RUN apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# VNC port for display :1
EXPOSE 5900

CMD [ "/usr/bin/supervisord" ]


