## Build 

* To build the Docker image

```
docker build -t transmission .
```

## Run

* To run the Docker image

```
docker run --rm \
	-e DISPLAY=$DISPLAY \
        -v /tmp/.X11-unix:/tmp/.X11-unix \
        -v $HOME/Downloads:/downloads \
        -v $HOME/.local:/home/transmission/.local \
        -v $HOME/.config:/home/transmission/.config \
        -v $HOME/.cache:/home/transmission/.cache \
        transmission
```
