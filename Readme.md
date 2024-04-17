# Agenda of Docker

1. Problem Statement
2. Installation of Docker CLI and Desktop
3. Understanding Images v/s Containers
4. Running Ubuntu Image in Container
5. Multiple Containers
6. Port Mappings
7. Environment Variables
8. Dockerization of Node.js Application
    1. Dockerfile
    2. Caching Layers
    3. Publishing to Hub
9. Docker Compose
    1. Services
    2. Port Mapping
    3. Env Variables

# 1. Problem Statement

- There can be versioning issue if multiple user want to implement a project on there machine.

- Multiple Enviornment -> Replicate

- Docker uses container which make configuration and can be use in any machine(Linux and Windows)

- Containers are lightweight , can be build , share , deploy on cloud , destory e.t.c

# 2 Installation

- Docker Daemon - Images pull , make
- Docker Desktop - GUI , Show images

- Vesion:
    - ```Bash
            PS C:\Users\ayush> Docker -v
            Docker version 25.0.3, build 4debf41
         ```
- Running Ubuntu:
    - ```Bash
        PS C:\Users\ayush> docker run -it ubuntu
        Unable to find image 'ubuntu:latest' locally
        latest: Pulling from library/ubuntu
        3c645031de29: Pull complete
        Digest: sha256:1b8d8ff4777f36f19bfe73ee4df61e3a0b789caeff29caa019539ec7c9a57f95
        Status: Downloaded newer image for ubuntu:latest
        root@81c5133fb90d:/#
       ```
         - ```Bash
                root@81c5133fb90d:/# whoami
                root
                root@81c5133fb90d:/# ls
                bin   dev  home  lib32  libx32  mnt  
                proc  run   srv  tmp  var
                boot  etc  lib   lib64  media   opt  
                root  sbin  sys  usr
            ```
        - `-it` -> for interactive

# 3.  Images vs Container
- Images :
        - Like a operating system
        - To run image we use container.
        - One image can be run in multiple container .

- Container:
        - Each container have their own data .
        - Data is not shareable.
        - There can be situation one image running in two 
            different container.

# 4. Running Ubuntu Image in Container

- Show Running Container(CLI):
    - ```Bash
             PS C:\Users\ayush> Docker container ls
             CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS         PORTS     NAMES
             81c5133fb90d   ubuntu    "/bin/bash"   18 minutes ago   Up 7 seconds             eloquent_feistel
        ```
- Show all Container:
    - `PS C:\Users\ayush> Docker container ls -a`

- Start & Stop the Container :
    - ```Bash
        PS C:\Users\ayush> docker start eloquent_feistel
         eloquent_feistel
        PS C:\Users\ayush> docker stop eloquent_feistel
        eloquent_feistel
         ```
- Show images:
    - ```Bash
            PS C:\Users\ayush> docker images
            REPOSITORY                 TAG       IMAGE ID       CREATED        SIZE
            ubuntu                     latest    7af9ba4f0a47   6 days ago     77.9MB
            docker/welcome-to-docker   latest    c1f619b6477e   5 months ago   18.6MB
       ```

# 6. Port Mapping
- It mainly maps the docker server port with local server port.
- `docker run -it -p 1024:1025`
    - maps the container port 1025 to my local machine port 1024

- It needs to expose to run.

# 7. Environment variable
- To pass extra data using environment variable
    - `docker run -it 1025:1025 -e key=value -e key=value mailhog/mailhog


# 8. Dockerization of Node.js Application

- make a Docker file -> `Dockerfile`

- Firstly we need a base image -> Here we have chosen `Ubuntu`
- Choose Base Image wisely.
- After making `Dockerfile` 
- Run command : `docker build -t app_name .`
- It will run all configuration i.e.  given in `Dockerfile` and make an image
- All will be done inside container
- Running the Image :
    - ```Bash
            PS C:\Users\ayush> docker run -it -p 8000:8000 docker-nodejs
            Server started on PORT:8000
        ```
    
- At localhost:8000 -
    - `{"message:":"Hey , I am nodejs in conatiner"}`

- Changing post using `Enviornment Variable`:
    - ```Bash
            Create and run a new container from an image
            PS C:\Users\ayush> docker run -it -e PORT=4000 -p 4000:4000 docker-nodejs
            Server started on PORT:4000
        ```
    - Now on localhost:4000 -
        - `{"message:":"Hey , I am nodejs in conatiner"}`

 
## Chaching layer
    - Common lines should be written above in Dockerfile
    - When we build again it only build that part which has been changed.

## Publishing to Hub
    - Created a repo `docker-nodejs`
    - Then made a image `docker build -t unstoppableayush/docker-nodejs . `
    - Pushed the images `docker push unstoppableayush/docker-nodejs`


# 9. Docker Compose
- There can be a situation where we have to make multiple container.
- Container -> postgres , redis , nodejs , mailhog , mongodb
- We can create , setup , destroy multiple container using Docker Compose.

- To run Config - `Docker compose up`
- TO stop - `Docker compose down`
