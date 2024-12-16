# Layered Architecture And Dockerfiles

## What is a Dockerfile?
A Dockerfile is a document that contains scripts or instructions using which an image can be created.

## Creating a Dockerfile
```bash
vi Dockerfile
```
The `docker build` command by default builds an image by executing the instructions present in the file named **Dockerfile**in the current working directory. So, it is a best practice to always name your Dockerfile as Dockerfile. If you name the file something else, you need to specify the Dockerfile name explicitly using the `-f`option along with the docker build command.

## FROM

`FROM ubuntu:16.04`

A Dockerfile with the above content will build an image from the base Docker image `ubuntu:16.04`

The `FROM` keyword is used to specify the base image and will create a layer using the Docker image `ubuntu:16.04` as the base image.
Note: Best practices related to Dockerfile can be found in the Docker documentation.

### Build the Docker Image

`docker image build -t myubunut:1 .`
The above command will build an image from the Dockerfile we created above with the image name myubuntu and tag `1`. The `.` at the end specifies the current working directory.

## Docker Image Build and Caching
On executing the build command, an image with the name myubuntu will be created with the tag 1. You will notice that the image `myubuntu:1` and ubuntu:16.04 have the same IMAGE_ID. This is because there were no file structure changes on top of the base image, so the new image was tagged with the already existing image.

Now, let's add some more instructions to our Dockerfile.


## Dockerfile Instructions: Label, ENV, RUN, WORKDIR

### Label
The LABEL command is used to add metadata to Docker objects such as images, containers, local daemons, volumes, networks, swarm nodes, and swarm services.

Labels are key-value pairs stored as a string that can be used to organize your images, add licensing information, etc. We can add multiple labels to a Docker object.

```bash 
FROM ubuntu:14.04
LABEL name="your_name"
LABEL email="your_email@example.com"
```
### ENV
The ENV instruction is used to provide environment variables to an image that are persisted when a container is run.

Example Dockerfile with Environment Variables:

```bash
FROM ubuntu:14.04
LABEL name="your_name"
LABEL email="your_email@example.com"
ENV name=nischal
ENV pass=password
```
### RUN
The RUN instruction is used to execute any command on top of the image and add a new layer on top of existing layers
``` bash
FROM ubuntu:14.04
LABEL name="your_name"
LABEL email="your_email@example.com"
ENV name=nischal
ENV pass=password
RUN apt-get update 
RUN touch /tmp/pwd.txt
```
The RUN instruction is used to execute any command on top of the image and add a new layer on top of existing layers
The `RUN` instruction in the above image will update the ubuntu.

Docker daemon executes each instruction in the Dockerfile one by one, and each instruction is executed independently, so the previous instruction has no impact on the next one. Each instruction in the Dockerfile creates a new layer on top of the existing layers.

It is not a best practice and an efficient way to use RUN multiple times in our Dockerfile because it will create many layers. Additionally, Docker uses cache for executing commands that have already been executed for better performance.

If we modify an existing Dockerfile and add a RUN instruction in the middle of the Dockerfile instead of adding it at the end, this will cause Docker to execute each command again as a fresh command and hamper performance.

## Dockerfile Instructions: USER, COPY, ADD
### USER
The USER instruction is used to switch the user for any instruction that follows it in the Dockerfile.
```bash 
FROM ubuntu:16.04
LABEL name="nischal"
ENV name=nischal
ENV pass=password
RUN pwd > /tmp/pwd.txt
WORKDIR /tmp
USER $name
```
### COPY
The COPY instruction is used to copy files or directories from the specified source to the destination inside the container's filesystem.

Example: 
```bash
FROM ubuntu:16.04
LABEL name="nischal"
ENV name=nischal
ENV pass=password
RUN pwd > /tmp/pwd.txt
WORKDIR /tmp
USER $name
COPY project /tmp/project
```
### ADD
The ADD instruction is used to copy files or directories from the specified source to the destination inside the container's filesystem.

Example:
```bash
FROM ubuntu:16.04
LABEL name="nischal"
ENV name=nischal
ENV pass=password
RUN pwd > /tmp/pwd.txt
WORKDIR /tmp
USER $name
ADD project /tmp/project
```
Difference between ADD and COPY in Docker:

The ADD instruction unpacks the source file if it is in a recognized compression format (gzip, bzip2, xz, etc.) while COPY copies the compressed file as-is without unpacking.

## Dockerfile - CMD and ENTRYPOINT

### CMD
The CMD instruction is used to provide a default executable or an entry point for executing the container. The executable provided in the CMD instruction will launch automatically when the container is run.
Example:
```bash
FROM ubuntu:16.04
LABEL name="nischal"
ENV name=nischal
ENV pass=password
RUN pwd > /tmp/pwd.txt
WORKDIR /tmp
USER $name
ADD project /tmp/project
CMD ["python"]
```
**Note**: There can be only one CMD instruction in the Dockerfile. If more than one CMD instruction is listed, the last one will take effect

### ENTRYPOINT
The ENTRYPOINT instruction allows us to configure a container to run as an executable.

Example:
```bash
FROM ubuntu:16.04
LABEL name="nischal"
ENV name=nischal
ENV pass=password
RUN pwd > /tmp/pwd.txt
WORKDIR /tmp
USER $name
ADD project /tmp/project
CMD ["python"]
ENTRYPOINT ["ps-aux"]
```
We can also pass arguments to the script while running the container which is required by the script.

Similarly, the ENTRYPOINT instruction can be used for various purposes based on our needs.