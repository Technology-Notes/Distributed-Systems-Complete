# Distributed Systems Practice
Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

## Docker and Containers
### Beginner Level
* [Why Docker?](https://www.youtube.com/watch?v=RYDHUTHLf8U&t=0s&list=PLBmVKD7o3L8tQzt8QPCINK9wXmKecTHlM&index=23)

Time: 20 min.

This video covers the whys and whats of how the Docker got started, what problems it solves and why should we be learning it.
Learning docker is really important, like the author said, containers are the nextonce-in-a-decade shift in infrastructure and process that make or break you.

**What is Docker:** 
Docker is a computer program that performs operating-system-level virtualization, also known as "containerization".

**Key points:**

1). Yet unlikes previous shifts, like mainframe to PC, Baremetal to virtual and Datacenter to cloud, Docker is focused on the migration experience. 

2). To answer why do we need docker and what is the real benefit, Docker is all about speed and covers the entire lifecycle of software managment.

3). Comtainers reduce the complexity. It allows us to package the same way regardless of our perating systems. It allows us to distribute the software regardless of the setup it. It allows us to run and test the software everywhere we are running it.

4). Docker is freeing up a lot of those rasks of the maintenance of stuff and allowing us to get more of our time to innovate. 

5). Docker is the core essence that you need to understand first but once you've moved beyond that you are probably need to use other tools for filling the gaps in your toolset.

* [Lab: DevOps Docker Beginners Guide](https://training.play-with-docker.com/ops-s1-hello/)

Time: 90min

In this lab we will run a popular, free, lightweight container and explore the basics of how containers work, how the Docker Engine executes and isolates containers from each other. 

![](https://github.com/haoduoding/dist-sys-practice/blob/master/lab%20screenshots/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202018-10-26%2012.54.04.png?raw=true)

Concepts in this exercise:
*Docker engine, Containers & images, Image registries and Docker Store (AKA Docker Hub)* and *Container isolation.*

* *Images* - The file system and configuration of our application which are used to create containers. To find out more about a Docker image, run ```docker image inspect alpine```. In the demo above, I used the ```docker image pull``` command to download the **alpine** image. When I executed the command ```docker container run hello-world```, it also did a ```docker image pull``` behind the scenes to download the **hello-world** image.

* *Containers* - Running instances of Docker images — containers run the actual applications. A container includes an application and all of its dependencies. It shares the kernel with other containers, and runs as an isolated process in user space on the host OS. I created a container using ```docker run``` which you did using the alpine image that you downloaded. A list of running containers can be seen using the ```docker container ls``` command.

* *Docker daemon* - The background service running on the host that manages building, running and distributing Docker containers.

* *Docker client* - The command line tool that allows the user to interact with the Docker daemon.

* *Docker Store* - Store is, among other things, a registry of Docker images. You can think of the registry as a directory of all available Docker images. You’ll be using this later in this tutorial.

> Include notes here about each of the links

## Area 2
> Include notes here about each of the links
