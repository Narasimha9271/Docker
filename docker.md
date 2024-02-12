-   As a surveys find Docker to be the most popular tool used by 57% of professional developers.
-   We have to master Docker fundamentals to use other people's Docker images and create and publish your own images to the docker Hub container Library as well as run and manage containers.
-   Docker is a platform that enables the development packaging and execution of applications in a unified environment by clearly specifying our applications requirements such as no Js versions and necessary packages.
-   Docker generates a self-contained box that includes its own operating system and all the components essential for running our application this box acts like a separate computer virtually providing the operating system run times and everything required for our application to run smoothly.

### Advantages of Docker

-   Consistemcy Across Environments
-   Boosts Collaboration
-   Makes development and deployment faster
-   Isolation -> b/w our app and its dependencies
-   portability -> can easily b/w stages like Development to testing and Testing to Production.
-   Docker container are light weight. => more efficency => faster application's start time.
-   USing Docker, we can return to prev version of our app (likely VCS like git).
-   Scalability -> easy to handle more users by creating copies of our application.
-   Devops Integration -> it stramlines the flow b/w coding and deployment.

### Two Important Concepts in Docker

-   **Images**
-   **Containers**

### Images

-   It is a lightweight, standalone, execution package eveything needed to run a piece of software. includes code, runtimes(like node.js), libraries, system tools, OS.

### Container

-   It is a runnable instance of a Docker Image.
-   It's like execution Environment.
-   Container takes everything from image and follows its instructions by executing necessary cmds like downloading packages and setting thinggs up to run our appp.
-   Like For a given ingridients of a cake, we can make multiple types of cakes, Similarly We can run multiple containers from the same image.

### Volumes

-   it is a persistent data storage mechanism that allows data to be stored b/w docker container and the host machine.

### Networks

-   It is a communication channel that allows different containers to talk to each other.

## Docker Workflow in 3 parts

1. **Docker client**

-   UI for user to interact with docker.
-   Tool we use to give Docker cmds via CLI or GUI instructing it to build, run or managing images or containers.

2. **Docker Host aka Docker Daemon**

-   It is a background service that manages the building, running and distributing of Docker containers.
-   It listens for Docker client cmds or Docker API requests and manages Docker objects like images, containers, networks and volumes.
-   It is the server part of the Docker.
-   The Docker client and the daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon.
-   The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.
-   The Docker daemon is the process that runs in the operating system to which the Docker client sends commands.
-   The Docker daemon can also communicate with other daemons to manage Docker services.

3. **Docker Registry aka Docker Hub**

-   It is a service that allows you to store and distribute **Docker images**.
-   It is a central repository for Docker images.
-   It hosts both public and private packages or registrys.

![imag](https://media.licdn.com/dms/image/D5622AQGR5LO5Wffl9Q/feedshare-shrink_800/0/1703485799355?e=1710374400&v=beta&t=d-O3kKCiQxNzvekdQO_PPuEadD1nhvmfsv4I7TLGJCU)

## How to create a Docker Image

**FROM** -> specifies the base image to use the new image

**WORKDIR** -> sets the working directoryt for the following instructions.

**COPY** -> copies the directory from the build context to the image

**RUN** -> executes cmds in a shell during image build.

**EXPOSE** -> informs docker to listen at a specified N/W port at run time.

**ENV** -> setting environment variables

**ARG** -> defines the built time variables.

**VOLUME** -> creates a mount point for externally mounted volumes.

**CMD** -> default cmds executes when the container starts.

**ENTRYPOINT** -> configures a container that will run as an executable.

-   **CMD != ENTRYPOINT** but both used to run default cmds when a container starts.
-   Differnece is **CMD** is more flexible and acn be overriden when running the containerle **ENTRYPOINT** cannot be overriden.
-   CMD is default -> can be changed
-   ENTRYPOINT is Fixed starting point -> can't be changed.

### HOW TO RUN A CONTAINER

-   `docker run -it image_name`

### HOW TO CREATE OUR OWN DOCKER IMAGES

1. Create a file named `Dockerfile` with above mentioned commands.
2. Run `docker build -t image_name .` to build the image.
   To verify image created or not, Run `docker images`
3. Run `docker run image_name` to run the container.
   TO run in shell mode `docker run -it image_name sh`
   To run with port mapping `docker run -p 5173:5173 image_name`
4. If we want to push this image into Docker Hub, then follow these steps:
    - `docker login` -> login to docker hub
    - `docker tag image_name username/image_name` -> tag the image
    - `docker push username/image_name` -> push the image to docker hub.

## Cmds related to container

-   `docker ps` -> to see all running containers
-   `docker ps -a` -> to see all containerss
-   `docker stop id` -> to stop a specific container
-   `docker container prune` -> to stop all containers -`docker rm id --force` -> To remove the running container

### NOTE

-   After building and running image, if you made changes in html, it won't reflect -> That's what docker is -. more secure
-   So to do this render in our webapp, stop the running container
-   DO `docker  run -p 5173:5173 -v "$(pwd):/app" -v /app/node_modules image_name`

## How to publish docker image

1. `docker login`
2. `docker tag image_name narasimha9271/image_name`
3. `docker push narasimha9271/image_name`

**The above way is hectic for devs to write all**

### Docker compose

-   A tool used to define and manage multi container docker applications.
-   It uses a YAML file to configure the application's services, networks and volumes.
-   We don't write 10 cmds to run 10 containers for an application.
-   We write a single file `docker-compose.yml` to configure all the containers.

-   Using this, we can automate alll by eriting one cmd `docker compose up`
-   start with `docker init`
-   Besides it's building and running app in one cmd but it needs configuration settings like adding --host, changing UI needed to rebuild etc..

There comes

### Docker compose watch

-   It re runs the app, rebuilds and is upto date with new features by defining build section in compose.yaml file.
-   It's a new feature that automatically updates
-   It has 3 main things

1. **sync** -> it moves changed files from our cp to data in container
2. **Rebuild** -> it restart the container, Most revent version of the code is in operation.
3. **Sync-restart** -> sync + rebuild

### Docker Scout

-   Tool that is proactive about security.
-   It scans container images , looks at the layers and software pieces like building blocks inside them => creates a detail list called SBOM(Software Bill of Materials)
-   We can use Docker Scout in different places like Docker Desktop, Docker Hub, Docker CLI.
