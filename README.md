# Dockerfiles

This repo contains the different dockerfiles that I create for personal/professional use.

## For GUIs

Running X11 applications

```
docker run -it \
 	-e DISPLAY=$DISPLAY \
	--volume="&HOME/.Xauthority:/root/.Xauthority:rw" \
	-v /tmp/.X11-unix:/tmp/.X11-unix \
	--ipc=host \
	<dockerimage_name>
```

## Using the current host user for dockers

In Dockerfiles

```
FROM <image>

.........
.........

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

.........
.........
```

Building the Docker images

```
docker build --build-arg user=$USER --build-arg uid=$(id -u) --build-arg gid=$(id -g) -t <tag_name> .
```

## Mounting host partitions in dockers

```
docker run \
	-it \
	--mount type=bind,source=/build,target=/build \
	<dockerimage_name>
```

## Daemonize dockers

```
docker run -d -p 80:80 my_image service nginx start
```

## Solve the GTK error

Run

```
xhost +"local:docker@"
```

To get back to original state

```
xhost -"local:docker@"
```

## Routing Docker traffic through VPN

Assuming that a container of the preferred VPN is running with the name `vpn`. For example, see [Mullvad VPN](https://hub.docker.com/r/xeroxmalf/mullvadvpn)

```
docker run --rm \
      -e DISPLAY=$DISPLAY \
      --volume="$HOME/.Xauthority:/root/.Xauthority:rw" \
       -v /tmp/.X11-unix/:/tmp/.X11-unix \
      --net=container:vpn \
      <dockerimage_name>
```
