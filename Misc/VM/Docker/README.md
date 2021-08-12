# prerequisite

1. Making sure you are members of non-root docker user

    a) Creating docker group:
```
        sudo groupadd docker
```

    b) Adding yourself into docker group
```
        sudo usermod -aG docker ${USER}
```

    c) Log out and re-log in

# Using Dockerfile to prepare docker image

1. Creating a docker image with command:
```
	docker build -t ${IMAGE TAG} .
```

    a) Docker official recommend you to use ${USER}/${IMAGE}:${VERSION} to form your ${IMAGE TAG}, and
low characters allow.

    b) Making sure there is a valid Dockerfile in your current path, like the one with this README.

    c) Official reference for writing Dockerfile is here: 
        https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
        https://docs.docker.com/engine/reference/builder/

# Constrocting docker container from docker image

1. Creating a docker container with commad:
```
        docker run -d -P -v ${HOST FOLDER}:${DOCKER MOUNT} --name ${CONTAINER NAME} ${IMAGE TAG}
                   -- -- --------------------------------- ------------------------ ------------
```

    a) -d: Running your container as a daemon

    b) -P: Dynamically assign port to Docker port.
        For examlpe, you can use "EXPOSE 22" in Dockerfile to expose SSH port to host; then you need to add "-P" arguments to
        create your containers to assign dynamic port. Otherwise, you can NOT use ssh to connect to your container.

        To check which dynamic port are binding with your container, you can use command:
            docker port ${CONTAINER NAME}

    c) -v: Sharing folders on both host and container.

	For excample: -v /var/opt/Docker:/mnt/host

    d) --name: Naming your container. You can use "docker ps" or "docker container ls -a" to see your containers with these names.

    e) ${IMAGE TAG}: Tag name for your docker image. Checking step 2.

# Misc 

    a) How to find the dynamic port for running docker containers?

        You can find the port either by executing command "docker ps", or "docker port ${CONTAINER NAME}.

    b) How to find IP address for running docker containers?

        docker inspect -f "{{ .NetworkSettings.IPAddress }}" ${CONTAINER NAME}

    c) How to get into running docker container?

        docker exec -it -u root ${CONTAINER NAME} /bin/bash

    d) How to run another Dockerfile in a Dockerfile

	1. Try to create a Docker image from Dockerfile A, and tag it as ${BASE IMAGE}
	2. In another Dockerfile, starting command like "FROM ${BASE IMAGE}"

