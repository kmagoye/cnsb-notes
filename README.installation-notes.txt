CNSB - Cloud Native Spring Boot Action 
- This is the notes repository, responsible for executing the commands as defined in the book

- Managing different Java versions and distributions on your machine might be painful. I recommend using a tool like sdkman (https://sdkman.io) to install, update, and switch between different JDKs easily. On macOS and Linux, you can install sdkman as follows:
> curl -s "https://get.sdkman.io" | bashcurl -s "https://get.sdkman.io" | bash

- Once it’s installed, check all the available OpenJDK distributions and versions by running the following command:

> sdk list java

---
- There is this to consider
> Omit Identifier to install default version 17.0.8.1-tem:
>   $ sdk install java
> Use TAB completion to discover available versions
>   $ sdk install java [TAB]
> Or install a specific version by Identifier:
>   $ sdk install java 17.0.8.1-tem
> Hit Q to exit this list view
---

Then choose a distribution and install it. For example, I can install the latest 17 version of Eclipse Temurin available at the moment of writing as follows:

$ sdk install java 17.0.3-tem

By the time you read this section, newer versions might be available, so please check the list returned from the list command to identify the latest one.

At the end of the installation procedure, sdkman will ask whether you want to make that distribution the default one. I recommend you say yes to ensure that you have access to Java 17 from all the projects you build throughout the book. You can always change the default version with the following command:

$ sdk default java 17.0.3-tem
Let’s now verify the OpenJDK installation:

$ java --version
openjdk 17.0.3 2022-04-19
OpenJDK Runtime Environment Temurin-17.0.3+7 (build 17.0.3+7)
OpenJDK 64-Bit Server VM Temurin-17.0.3+7 (build 17.0.3+7, mixed mode)
You also have the option to change the Java version only within the context of the current shell:

$ sdk use java 17.0.3-tem
Finally, if you want to check which version of Java is configured in the current shell, you can do that as follows:

$ sdk current java
Using java version 17.0.3-tem

Mine did not work but I was able to use the following command

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
kmagoye@kabojja00:/usr/lib/jvm$ sudo update-alternatives --config java
There are 4 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
  0            /usr/lib/jvm/java-17-openjdk-amd64/bin/java      1711      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
* 2            /usr/lib/jvm/java-17-openjdk-amd64/bin/java      1711      manual mode
  3            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode
  4            /usr/lib/jvm/java-8-oracle/jre/bin/java          1081      manual mode

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
(base) kmagoye@kabojja00:~$ docker login
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: kmagoye1
Password:
WARNING! Your password will be stored unencrypted in /home/kmagoye/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store


>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
The Open Container Initiative (OCI), a Linux Foundation project, defines industry standards for working with containers (https://opencontainers.org).

In particular, the OCI Image Specification defines how to build container images, the OCI Runtime Specification defines how to run those container images, and the OCI Distribution Specification defines how to distribute them. The tool we use throughout the book to work with containers is Docker, which is compliant with the OCI specifications.

On the Docker website (www.docker.com), you can find instructions for setting up Docker in your local environment. I’ll be using the latest versions available at the time of writing: Docker 20.10 and Docker Desktop 4.11.

On Linux, you can install the Docker open source platform directly. It’s also known as Docker Community Edition (Docker CE).

On macOS and Windows, you have the option to use Docker Desktop, a commercial product built on top of Docker that makes it possible to run Linux containers from those operating systems. At the time of writing, Docker Desktop is free for personal use, education, non-commercial open source projects, and small businesses. Please read the Docker Subscription Service Agreement carefully before installing the software, and make sure you are compliant with it (www.docker.com/legal).

Docker Desktop provides support for both ARM64 and AMD64 architectures, meaning that you can run all the examples in this book on the new Apple computers with Apple Silicon processors.

If you work on Windows, Docker Desktop provides two types of setup: Hyper-V or WSL2. I recommend you choose the latter, since it offers better performance, and it’s more stable.

Docker comes preconfigured to download OCI images from Docker Hub, a container registry hosting images for many popular open source projects, like Ubuntu, PostgreSQL, and Redis. It’s free to use, but it’s subjected to strict rate-limiting policies if you use it anonymously. Therefore, I recommend you create a free account on the Docker website (www.docker.com).

After creating an account, open a Terminal window and authenticate with Docker Hub (make sure your Docker Engine is running). Since it’s the default container registry, you don’t need to specify its URL:

$ docker login
When asked, insert your username and password.

Using the Docker CLI, you can now interact with Docker Hub to download images (pull) or upload your own (push). For example, try pulling the official Ubuntu image from Docker Hub:

$ docker pull ubuntu:22.04
Throughout the book, you’ll learn more about using Docker. Until then, if you would like to experiment with containers, I’ll leave you a list of useful commands for controlling the container life cycle (table A.1).

Table A.1 Useful Docker CLI commands for managing images and containers

Docker CLI command

What it does

docker images

Shows all images

docker ps

Shows the running containers

docker ps -a

Shows all containers created, started, and stopped

docker run <image>

Runs a container from the given image

docker start <name>

Starts an existing container

docker stop <name>

Stops a running container

docker logs <name>

Shows the logs from a given container

docker rm <name>

Removes a stopped container

docker rmi <image>

Removes an image

All the containers we build throughout the book are OCI-compliant and will work with any other OCI container runtime, such as Podman (https://podman.io). Should you decide to use a platform other than Docker, be aware that some tools we use for local development and integration testing might require additional configuration to work correctly.

Login Succeeded