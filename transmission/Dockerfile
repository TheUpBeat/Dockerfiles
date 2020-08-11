FROM debian:latest

RUN apt-get update && \
	apt-get install --no-install-recommends -y transmission \
	&& rm -rf /var/lib/apt/lists/*

CMD ["transmission-gtk"]
