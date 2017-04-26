# Docker Intro
This repo have files for [Docker Get Started](https://docs.docker.com/get-started/).

Visit [https://docs.docker.com/get-started/](https://docs.docker.com/get-started/) to get an idea if you don't know about docker

Docker Image of this tutorial is available at Docker Hub \
[electron0zero/docker-intro](https://hub.docker.com/r/electron0zero/docker-intro/)

## Few gotchas/ Things to keep in mind 

-  On Windows when you use docker using [docker-toolbox](https://www.docker.com/products/docker-toolbox), it runs it on a VirtualBox VM, Which results in ip of VM as address on which you listen, not on localhost.

-  Use [Kitematic](https://kitematic.com/) to figure out this IP

- If you are deploying real applications from windows,Then do not ignore warnings about permission and **make sure you have some mechanism to set appropriate permissions**

*Here is Warning Message*

> SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to double check and reset permissions for sensitive files and directories.


## Basic Commands

**Command:** `docker version`

**Output:**
```
Client:
 Version:      17.03.1-ce
 API version:  1.27
 Go version:   go1.7.5
 Git commit:   c6d412e
 Built:        Tue Mar 28 00:40:02 2017
 OS/Arch:      windows/amd64

Server:
 Version:      17.04.0-ce
 API version:  1.28 (minimum version 1.12)
 Go version:   go1.7.5
 Git commit:   4845c56
 Built:        Wed Apr  5 18:45:47 2017
 OS/Arch:      linux/amd64
 Experimental: false
```

**Explanation:** Self explained imo

---

**Command:** `docker build -t docker-intro .`

**Output:** output of executing Dockerfile and info about image

**Explanation:** Builds image named `docker-intro` from `.` (current dir) \
[*assuming it have a Dockerfile in it**]

---

**Command:** `docker images`

**Output:**
```
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
docker-intro        latest              58274ed93000        4 minutes ago       194 MB
python              2.7-slim            4a323b466a5a        3 hours ago         182 MB
```

**Explanation:** list docker images

---

**Command:** `docker run -p 4000:80 docker-intro`

**Output:**
```
 * Running on http://0.0.0.0:80/ (Press CTRL+C to quit)
```
*This output is from app, running in container.\
Not local system so will not be available that IP, It will be available on mapped port on VM's IP*

- Use [Kitematic](https://kitematic.com/) to figure out ip on which you can access it.

**Explanation:** run docker image `docker-intro` and `-p` flag is used port mapping, here port `4000` of system running docker(host) is mapped to port `80` of container.

---

**Command:** `docker run -d -p 4000:80 docker-intro`

**Output:**
```
1b7d07adb936265a857da1b318e82b29e1bd15ef3f874239f7384948368f5829
```

**Explanation:** run in detached mode

>if you have issue saying `failed: port is already allocated`.
> It means you have an container running on that port, you can resolve it by killing/stopping that running container or changing it to a free port

*use `docker stop <container-id>`, container id can be found by running `docker ps -a`*

Sample Output of `docker ps -a`
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                       PORTS                  NAMES
1b7d07adb936        docker-intro        "python app.py"     2 minutes ago       Up 2 minutes                 0.0.0.0:4000->80/tcp   kind_dijkstra
24146a2050a1        docker-intro        "python app.py"     4 minutes ago       Created                                             unruffled_varahamihira
432528f53e40        docker-intro        "python app.py"     9 minutes ago       Exited (137) 3 minutes ago                          kind_haibt
```


### You can use [Docker Hub](http://hub.docker.com/) to share you images, it is like github for docker images.
*I am not going into this, it is fully described in docker docs*

### Final Thought 
Docker has more stuff then i described, it is just the gist of it. \
See multi-part [getting-started guide](https://docs.docker.com/get-started/) to learn more