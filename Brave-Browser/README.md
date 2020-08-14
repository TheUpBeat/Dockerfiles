# Build

To build the Docker image

```
docker build --build-arg user=$USER --build-arg uid=$(id -u) --build-arg gid=$(id -g) -t brave .
```

# Run

```
docker run -d --rm \
	--ipc=host \
	--net host \
        -e DISPLAY=unix$DISPLAY \
        --volume="$HOME/.Xauthority:/root/.Xauthority:rw" \
        -v /tmp/.X11-unix:/tmp/.X11-unix \
        --mount type=bind,source=$HOME/Documents/BraveSoftware,target=$HOME/.config/BraveSoftware/Brave-Browser \ # To store the .config of the docker for future purposes
        --device /dev/snd \
        -v /dev/shm:/dev/shm \
        --device /dev/dri \
        --device /dev/video0 \
        --group-add video \
        --group-add audio \
        -e PULSE_SERVER=unix:$XDG_RUNTIME_DIR/pulse/native \
        -v $XDG_RUNTIME_DIR/pulse/native:$XDG_RUNTIME_DIR/pulse/native \
        -v ~/.config/pulse/cookie:/root/.config/pulse/cookie \
        --group-add (getent group audio | cut -d: -f3) \
	--security-opt seccomp=$HOME/chrome.json \ # Use the seccomp of chrome wget https://raw.githubusercontent.com/jfrazelle/dotfiles/master/etc/docker/seccomp/chrome.json -O ~/chrome.json
        brave
```
