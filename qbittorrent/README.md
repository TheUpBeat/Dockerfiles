## Build

* To build the Docker image

```
docker build -t qbittorrent .
```

* To run the Docker image

```
docker run -d --rm\
	-e DISPLAY=$DISPLAY \
	--volume="$HOME/.Xauthority:/root/.Xauthority:rw" \
	--net=host \
	qbittorrent
```
