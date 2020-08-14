FROM debian:bullseye-slim

RUN apt-get update && \
        apt-get install -y \
        apt-transport-https curl \
        gnupg

RUN curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add - \
        && echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ stable main" | tee /etc/apt/sources.list.d/brave-browser-release.list

RUN apt-get update \
        && apt-get install -y \
        brave-browser \
        fonts-liberation \
        fonts-roboto \
        hicolor-icon-theme \
        libcanberra-gtk-module \
        libexif-dev \
        libgl1-mesa-dri \
        libgl1-mesa-glx \
        libpangox-1.0-0 \
        libv4l-0 \
        fonts-symbola \
        libgl1-mesa-dri \
        libgl1-mesa-glx \
        libpangox-1.0-0 \
        libpulse0 \
        libv4l-0 \
        fonts-symbola \
        alsa-utils \
        pulseaudio \
        libgtk-3-0 \
        libnotify4 \
        libnss3 \
        libxss1 \
        libxtst6 \
        xdg-utils \
        libatspi2.0-0 \
        libappindicator3-1 \
        libsecret-1-0 \
        libasound2 \
        ca-certificates \
      --no-install-recommends \
       && rm -rf /var/lib/apt/lists/*

ARG user
ARG uid
ARG gid

ENV USERNAME ${user}
RUN useradd -m $USERNAME && \
        echo "$USERNAME:$USERNAME" | chpasswd && \
        usermod --shell /bin/bash $USERNAME && \
        usermod  --uid ${uid} $USERNAME && \
        groupmod --gid ${gid} $USERNAME

USER ${user}
ENV HOME /home/${user}
WORKDIR ${HOME}

ENTRYPOINT /usr/bin/brave-browser-stable
