FROM debian:latest

RUN apt-get update && \
	apt-get install -y \
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
	apt-transport-https \
	ca-certificates \
	curl \
	gnupg \
	hicolor-icon-theme \
	libcanberra-gtk* \
	libgl1-mesa-dri \
	libgl1-mesa-glx \
	libpangox-1.0-0 \
	libpulse0 \
	libv4l-0 \
	fonts-symbola \
	alsa-utils \
	pulseaudio \
	&& rm -rf /var/lib/apt/lists/*

ADD https://github.com/FreeTubeApp/FreeTube/releases/download/v0.7.3-beta/FreeTube_0.7.3_amd64.deb FreeTube.deb

RUN dpkg -i FreeTube.deb

CMD /usr/bin/freetube --no-sandbox
