FROM ubuntu:24.04
    EXPOSE 5901

    # dosemu2 is not in the default Ubuntu repos.
    # see: https://github.com/dosemu2/dosemu2
    RUN set -eux \
      && apt -y update \
      && apt install -y --no-install-recommends \
        software-properties-common \
      && add-apt-repository ppa:dosemu2/ppa

    RUN set -eux \
      && apt install -y --no-install-recommends \
        dosbox \
        dosemu2 \
        tightvncserver \
        xfonts-base \
        lwm \
        xterm \
        vim-tiny \
        less \
        wget \
        ca-certificates \
        supervisor \
        zip \
        unzip \
        pwgen \
        xdotool \
        telnet \
        mtools \
        nano \
      && apt clean \
      && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

    COPY startvnc /usr/local/bin
    COPY dosboxconsole /usr/local/bin
    COPY supervisor/ /etc/supervisor/conf.d/
    COPY setup.sh /
    RUN set -eux \
      && /setup.sh

    CMD ["/usr/bin/supervisord", "-n", "-c", "/etc/supervisor/supervisord.conf"]
