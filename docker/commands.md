# Docker Commands

## Basic Docker Commands

1. Run docker image (takes an image, creates a container
   from it and then runs it. If run is used multiple times, multiple containers of the same image will be formed)

       docker run <image>
       
2. Start docker (starts docker with existing container)

       docker start <name|id>
3. Stop docker (stop a running docker container,
    to restart container use `docker start`)

       docker stop <name|id>
4. List of docker images

       docker ps [-a include stopped containers]
5. Remove docker container

       docker rm <name|id>
       
6. Docker Version

       docker --version
