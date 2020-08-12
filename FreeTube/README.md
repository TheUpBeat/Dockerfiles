## Build

* To build the Docker image

```
docker build -t freetube .
```

## Run

* To run the Docker image

```
docker run -d --rm --ipc=host \
	-e DISPLAY=unix$DISPLAY \
	--volume=/tmp/.X11-unix:/tmp/.X11-unix \
	--volume="$HOME/.Xauthority:/root/.Xauthority:rw" \
	-v /dev/shm:/dev/shm \
	--net=host \
        --device=/dev/dri \
	--device /dev/snd \
	--device /dev/video0 \
	--group-add video \
	--group-add audio \
	--device /dev/snd \
	-e PULSE_SERVER=unix:$XDG_RUNTIME_DIR/pulse/native \
	-v $XDG_RUNTIME_DIR/pulse/native:$XDG_RUNTIME_DIR/pulse/native \
	-v ~/.config/pulse/cookie:/root/.config/pulse/cookie \
	--group-add (getent group audio | cut -d: -f3) \
	freetube
```

* If faced with an error `Gtk-WARNING: cannot open display: unix:0`

```
run xhost +"local:docker@"
```
