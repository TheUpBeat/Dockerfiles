FROM debian:latest

RUN apt-get update && \
	apt-get install -y qbittorrent \
	&& rm -rf /var/lib/apt/list/*

ENTRYPOINT ["qbittorrent"]
