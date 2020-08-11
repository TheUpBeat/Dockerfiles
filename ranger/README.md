## Build

* To build the Docker image

```
docker build ranger .
```

* To run the Docker image

```
docker run -it --rm \
	-v $HOME:$HOME \
	ranger
```
