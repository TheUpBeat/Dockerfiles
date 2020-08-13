FROM debian:latest

RUN apt-get update \
        && apt-get install -y \
        telegram-desktop \
        libgl1-mesa-dri \
        libgl1-mesa-glx \
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
        libpangox-1.0-0 \
        libpulse0 \
        libv4l-0 \
        alsa-utils \
        pulseaudio \
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

CMD telegram-desktop
