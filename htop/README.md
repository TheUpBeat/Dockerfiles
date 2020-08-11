## Build

* To build the Docker image

```
docker build -t htop .
```

## Run

* To run the Docker image

```
 docker run -it --rm \
 	--pid=host \
 	htop
```
