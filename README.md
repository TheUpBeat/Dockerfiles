# Understanding Docker

## What is Docker?

* Dockers are used to host/deploy an application in a sandbox called containers. They are mostly a virtual machine but with less overhead.

* The most important feature of Docker is it permits the user to create a package of the application with all the dependencies that can be deployed in a different machine (or) moved to a different server.

* Every application executed using dockers run separately and does not depend on other applications. 

## Dockerfile -> Image -> Container

* **Dockerfile:** This file contains some normal text that are the commands to build an Docker image. 

* **Docker Image:** Built from the Dockerfile, creating a template which is then executed to create a container.

* **Container:** This is the container that contains the application and all the required libraries and dependencies.

## Bulking Up

* There are not much libraries required to install the Docker. 

Note: As I use Void Linux, the following post will be according to it.

* Install docker

```
xbps-install docker
```

* Symlink the docker to `/var/service/`

```
ln -s /etc/sv/docker/ /var/service
```

* Start the service

```
sv up docker
```

* To test your Docker installation, run the following command:

```
docker run hello-world
```

* To add Docker group and add an user:

```
sudo groupadd docker
```

* To add an user to the group

```
sudo usermod -aG docker $USER
```

## Writing, Building, Running Dockerfiles

### Writing Dockerfiles

* To build a custom docker for a specific application, the user must create a Dockerfile that contains that commands that is to be executed.

* To start writing Dockerfiles, create a folder for storing the Dockerfile of the specific application. In this case I will write a docker file for `htop`.

```
mkdir htop
cd htop
```

* Create a file with name `Dockerfile` and add the following text

```
FROM ubuntu:latest

RUN apt-get update -y && apt-get upgrade -y && apt-get install -y htop

CMD ["htop"]
```

* The first line `FROM ubuntu:latest`, import the image of the Ubuntu from the docker hub with the help of FROM command. The docker needs this for the desktop environment.

* The second line, executes the apt-get to update, upgrade the system and install the `htop`.

* The last line, as mentioned executes a command cause of the keyword CMD.

### Building Dockerfiles

* After writing the Dockerfiles, they are needed to be built with the help of `docker build`.

* To build the newly created Dockerfile

```
docker build -t htop .
```

* This builds the Dockerfile present in the current directory, tagged with the name htop.

### Running the Docker images

* To run the built docker images

```
docker run -it --rm --pid=host htop
```

* The command run the created `htop` image. The additional parameters are `-it` is for interactive shell, `--rm` to remove the docker after exiting, `--pid=host` sends the PID namespace of the current user and `htop` the tag of the Dockerfile that is previously created.

---
**NOTE**

Using `Alpine` instead of `Ubuntu` can decrease the resource usage and avoid installing packages that are not needed.

---

### GUI in Docker

* For a GUI application we XServer to run. In a normal desktop this is present, whereas for the docker container the host's XServer is shared.

* Sharing the XServer is done by creating a volume

```
--volume="&HOME/.Xauthority:/root/.Xauthority:rw"
```

* Similarly share the host's Display

```
--env="DISPLAY"
```

* Run the docker with the host's network driver

```
--net=host
```

* Create folder and a Dockerfile to install `xman`, which is used to look into man pages.

	- Contents of the Dockerfile

	```
	FROM debian:latest
	
	RUN apt-get update && apt-get install -y x11-apps #Contains may other apps
	
	CMD ["xman"]
	```

	- Build the Dockerfile

	```
	docker build -t xman .
	```

	- Run the Docker image

	```
	docker run --rm --volume="$HOME/.Xauthority:/root/.Xauthority:rw" --env="DISPLAY" --net=host xman
	```

* Create a folder and a Dockerfile to install `transmission`.

	- Contents of the Dockerfile

	```
	FROM debian:latest

	RUN apt-get update && apt-get install -y transmission

	CMD ["transmission-gtk"]
	```

	- Build the Dockerfile

	```
	docker build -t transmission .
	```

	- Run the Docker image

	```
	docker run -it \
		-e DISPLAY=$DISPLAY \
        	-v /tmp/.X11-unix:/tmp/.X11-unix \
                -v $HOME/Downloads:/downloads \
                -v $HOME/.local:/home/transmission/.local \
                -v $HOME/.config:/home/transmission/.config \
                -v $HOME/.cache:/home/transmission/.cache \
                transmission
	```
