# Easydock - Docker automation utility

```
Easydock is a docker automation utility that aims to simplify control of docker images and containers through uses of standardized templates/"recipes", aka, run scripts like the file provided that helps to design and automate a single service in a way similar and corresponding to docker-compose files, corresponding areas such as parameters (i.e. -t => tty=true, -i => stdin etc).

Essentially at its core, this particular filesystem structure is part of a bigger suite that when joined together, will allow you to manage multiple docker images, containers together in an environment similar to docker-compose.

The flow of operation that i'm proposing is as such
    /
    |
    |-- [docker images/container folder]/
        |
        |-- [service-name]/
            |
            |-- easydock : Your easydock recipe/startup definitions for this current service
            |-- Dockerfile : (Optional) Your dockerfile to build if you are not using a remote image
            |-- Dependencies/ : Folder to contain your requirements/dependencies/other files
                |
                |-- other-files-here
          
In a sense, as I mentioned previously, like docker-compose, there will be a central main application that will utilize the service folder, the easydock run scripts, dependency files to provide an easier time controlling multiple services without the use of yaml and/or docker-compose.

This project as you might tell, is primarily focused on docker, Dockerfiles, docker run and docker exec.
This is because as docker-compose exists, there are some areas that docker, Dockerfile and docker-compose does not cover such as in the area of parameters, making it hard for some users to move from docker run to docker-compose

Hence, the end goal here is to make the experience of using multiple docker run and docker execs just as usable as docker-compose.
```

## Setup
### Pre-Requisites
+ Add user to 'docker' group
- (Optional) if your container is using a Dockerfile self-built image
    + Create [Dockerfile](Dockerfile)

### Dependencies
+ docker
+ (Optional) docker-compose

### Preparation
- Change permission
    ```console
    chmod u+x easydock-runner
    ```

## Documentation
### Synopsis/Syntax
- easydock-runner
    ```console
    ./easydock-runner {commands|actions|flags} <arguments>
    ```

### Parameters
- Positional Arguments
    - Actions
        + -b | --build : (OPTIONAL) Build a Dockerfile if you are creating your image from a Dockerfile local image
            - Type: String

- Optionals

### Usage

## Wiki
### Variables
#### Global Variables
- DOCKERFILE_PATH : The path to the dockerfile you wish to build (OPTIONAL - remove if doesnt use a Dockerfile)
    + Type: String
    + Value: Path to Dockerfile
- IMAGE_NAME : The name of the image to make the container from
    + Type: String
- SERVICE_NAME : The name of the service (similar to docker-compose's services)
    + Type: String
- CONTAINER_NAME : The name of the container (similar to docker-compose's container_name)
    + Type: String
- volumes : A mapping of the volumes to mount from your host system into the container as well as its permissions
    + Type: Associative Array (aka Dictionary/HashMap in Shellscript)
    + Format: [volume_name]="host-system-path:container-path:permission"
    - Permissions
        + z : Special All Permissions
        + r : Read Only
        + w : Write Only
        + rw : Read + Write
       
### Functions
- view : View statistics based on keyword provided
    - Keywords
        + ps : View container processes
- build
- run
- start
- stop
- remove
- teardown
- exec_shell

