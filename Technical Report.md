<<<<<<< HEAD
# Some Understanding of Distributed Systems
## How to understand the word "distributed"?
"Distributed Systems", "Distributed Computing", "Distributed Algorithms". So what is the specific meaning of "distributied" here? In a narrow sense, it means that multiple PCs are geographically distributed in different places.  

## Distributed Systems
__Distributed system__: A group of computers (called nodes) that can run independently. Each node uses a computer network for information transfer to achieve a common "target or task."  

__Distributed program__: A computer program that runs on a distributed system.  

__Distributed Computing__: Use distributed system solutions to compute problems. In distributed computing, a problem is refined into multiple tasks, each of which can be done by one or more computers.  

Distinguish distributed computing  parallel computing: The commonality is that large tasks are divided into small tasks.  

Differences:  
* Distributed computing: Based on multiple PCs, each PC completes a different part of the same task. The task is decomposed and the smaller tasks are independent of each other. The results between the nodes hardly affect each other, and the real-time requirements are not very high.  
* Parallel computing: Based on the same PC, use the multicore of the CPU to accomplish a task together.  

### Distributed Operating System  
Responsible for managing distributed processing system resources and controlling distributed program operations. It differs from centralized operating systems in terms of resource management, process communication, and system architecture.  

### Distributed File System  
Distributed file systems have the ability to perform remote file access, and manage/access files distributed across the network in a transparent manner.  

### Distributed Programming and Compiler Interpretation System
Distributed programming language is used to write distributed programs that run on distributed computer systems. A distributed program consists of several program modules that can be executed independently, and they are executed simultaneously on multiple computers in a distributed processing system. It has three characteristics compared to a centralized programming language: distribution, communication, and robustness.  

### Hierarchical Application
Hierarchical applications can be partitioned by number of layers, and information can be transferred from the data layer (usually stored in the database) to the presentation layer (displayed on the client). Usually each layer runs in a different system than the other layers, or in different process spaces in the same system. Layering benefits: Reduce the complexity of the entire application; enable applications to scale better and keep up with the needs of enterprise development.  

* Two-tier application: Typical architecture, a client PC (front end) and a web server (backend) with a database. Logically based on the physical location of them. Usually the client contains most of the business logic. As the database and stored procedures evolve, the SQL language allows business logic to be stored and executed in the database server.
* Three-tier application: The most commonly used three-tier application structure includes a user service layer (presentation layer), a business service layer and a data service layer. The business logic layer is separated from the user interface and data source. Distributed applications are usually divided into three or more layers due to the functional limitations of a two-tier application(i.e. the client/server architecture). Each layer of components performs a specific type of processing.  

### Distributed Database
__My conclusion__:  
Distributed database consists of multiple databases (called sites) that are distributed in different places geographically which are connected based on a computer network. The distributed DBMS is used to manage each site in a unified manner, and each site is logically unified. It seems to be managing data on a single site based on the transparency of data distribution. The advantages are fault tolerance and increased access speed.  

__Official explanation__: A distributed database is a logically unified database composed of a plurality of physically dispersed database units connected by a computer network. Each connected database unit is called a site or node. A distributed database has a unified database management system for management, called a distributed database management system.  

The basic characteristics of distributed databases include: physical distribution, logical integrity, and site autonomy. Other features that can be derived from these three basic characteristics are: data distribution transparency, control mechanism combining concentration and autonomy, appropriate data redundancy, and distribution of transaction management. The distributed database is divided into heterogeneous distributed database and isomorphic distributed database according to the similarities and differences of the data model of the database management system in each site. According to the type of control system, it is divided into global control centralized type, global control distributed type and global control variable type.  

## Hadoop , HDFS, HBase, Hive
__My conclusion__:  
__Hadoop__ is a distributed system infrastructure framework. Based on this framework, the development of distributed applications leverages the power of clustered high-speed computing and storage. This is similar to the development of parallel programs based on NVIDIA's CUDA parallel architecture which leverages the parallel computing power of the GPU.  

__HDFS__ is the file system of Hadoop. Based on HDFS, you can manipulate files, such as create, delete, edit, rename, and so on.  

__Hbase__: A database system based on the Hadoop architecture. It is not a relational database. In addition, HBase is based on column rather than row based schema.  

__Hive__: A high-level language based on Hbase. Similar to SQL —— Computer language for accessing and processing relational databases.  

__Wiki explanation__: 
Apache Hadoop is a collection of open-source software utilities that facilitate using a network of many computers to solve problems involving massive amounts of data and computation. It provides a software framework for distributed storage and processing of big data using the MapReduce programming model. Originally designed for computer clusters built from commodity hardware — still the common use — it has also found use on clusters of higher-end hardware. All the modules in Hadoop are designed with a fundamental assumption that hardware failures are common occurrences and should be automatically handled by the framework.  

The core of Apache Hadoop consists of a storage part, known as Hadoop Distributed File System (HDFS), and a processing part which is a MapReduce programming model. Hadoop splits files into large blocks and distributes them across nodes in a cluster. It then transfers packaged code into nodes to process the data in parallel. This approach takes advantage of data locality, where nodes manipulate the data they have access to. This allows the dataset to be processed faster and more efficiently than it would be in a more conventional supercomputer architecture that relies on a parallel file system where computation and data are distributed via high-speed networking.  

The Hadoop distributed file system (HDFS) is a distributed, scalable, and portable file system written in Java for the Hadoop framework. Some consider it to instead be a data store due to its lack of POSIX compliance, but it does provide shell commands and Java application programming interface (API) methods that are similar to other file systems. A Hadoop is divided into HDFS and MapReduce. HDFS is used for storing the data and MapReduce is used for the Processing the Data. HDFS has five services as follows:  
1. Name Node  
2. Secondary Name Node  
3. Job tracker  
4. Data Node  
5. Task Tracker  

Top three are Master Services/Demons/Nodes and bottom two are Slave Services. Master Services can communicate with each other and in the same way Slave services can communicate with each other. Name Node is a master node and Data node is its corresponding Slave node and can talk with each other.  

HBase is an open-source, non-relational, distributed database modeled after Google's Bigtable and written in Java. It is developed as part of Apache Software Foundation's Apache Hadoop project and runs on top of HDFS (Hadoop Distributed File System), providing Bigtable-like capabilities for Hadoop. That is, it provides a fault-tolerant way of storing large quantities of sparse data (small amounts of information caught within a large collection of empty or unimportant data, such as finding the 50 largest items in a group of 2 billion records, or finding the non-zero items representing less than 0.1% of a huge collection).  

HBase features compression, in-memory operation, and Bloom filters on a per-column basis as outlined in the original Bigtable paper. Tables in HBase can serve as the input and output for MapReduce jobs run in Hadoop, and may be accessed through the Java API but also through REST, Avro or Thrift gateway APIs. HBase is a column-oriented key-value data store and has been idolized widely because of its lineage with Hadoop and HDFS. HBase runs on top of HDFS and is well-suited for faster read and write operations on large datasets with high throughput and low input/output latency.  

Apache Hive is a data warehouse software project built on top of Apache Hadoop for providing data query and analysis. Hive gives an SQL-like interface to query data stored in various databases and file systems that integrate with Hadoop. Traditional SQL queries must be implemented in the MapReduce Java API to execute SQL applications and queries over distributed data. Hive provides the necessary SQL abstraction to integrate SQL-like queries (HiveQL) into the underlying Java without the need to implement queries in the low-level Java API.  

__Hadoop Architecture__:  
Hadoop evolved from a three-tier structure of 1.0 to a current four-tier architecture after its 2.0 version changed resource management from MapReduce to a generic framework.  
1. Bottom layer —— storage layer, file system HDFS
2. Middle layer —— resource and data management, YARN and Sentry
3. Upper layer —— MapReduce, Impala, Spark and other computing engines
4. Top layer —— advanced packaging tools based on MapReduce, Spark and other computing engines, e.g. Hive, Pig, Mahout, etc.  

![image](https://github.com/thcyang/dist-sys-practice/blob/master/screenshot/hadoop4tier.png)  
* Storage layer  
HDFS has become the standard for big data disk storage, and it is used for online storage of massive log files.  
* Management layer  
Management is divided into data management and resource management.  
* Computation engine layer  
* Service layer  
The service layer is the programming API details of the underlying engine, providing a more abstract access model for business people, such as Pig, Hive, and so on.  

## References
Wikipedia entry: Apache Hadoop, Apache HBase, Apache Hive
=======
# Hello Docker

<div align=center>

![Docker](https://github.com/haoduoding/dist-sys-practice/blob/master/lab%20screenshots/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202018-12-09%2018.42.57.png?raw=true)

</div>

<div align=center>

```Docker: Build, Ship, and Run Any App, Anywhere```

</div>

I heard about the name of Docker not long after it was released. 
At that time, I didn't have any specific concepts about distributed systems, so I didn't go deep into Docker.
This semester I chose the course distributed system from [Prof. Tim Wood](https://faculty.cs.gwu.edu/timwood/). 
I was once again exposed to Docker, a cute blue whale, during class and after class.
This Technical Report briefly summarizes some of the important concepts involved in Docker. 

## What's Docker

Docker is written in GO and uses several features of the Linux kernel to provide its functionality. 
Docker lets you manage CPU, memory, network and disk resources just like managing virtual machines. 
Docker is an open platform for rapid development, distribution, and deployment of applications. 
It provides an abstraction at the operating system level and isolates the application's dependencies on the infrastructure (operating system, etc.). 
At the same time, Docker solves the consistency of production, testing, and deployment environments.

Docker provides containers (loosely coupled and isolated environments) to package and run applications. 
Good security and isolation allow us to run multiple containers on a single host. 
Because the container is a load that runs directly in the kernel of the host machine and does not require an additional hypervisor (such as a virtual machine that requires a VMware hypervisor), 
the container is said to be lightweight (This is one of our final exam questions :) ).

## Docker Engine

<div align=center>

![Docker Engine](https://github.com/haoduoding/dist-sys-practice/blob/master/lab%20screenshots/docker%20engine.png?raw=true)

</div>

As you can see from the figure, 
the client uses the docker CLI (command line tool) to interact with the docker daemon (docker daemon) through the Docker REST API. 
The docker daemon is responsible for creating and managing Docker objects (such as images, containers, networks, and storage volumes).

## Docker's Application Scenario

<div align=center>

![8 Dockers Use Case](https://github.com/haoduoding/dist-sys-practice/blob/master/lab%20screenshots/docker%20application.png?raw=true)

</div>

**Deliver Applications Quickly and Consistently**

Docker streamlines the development cycle by using a container that provides applications and services to provide a standardized working environment. 
Containers are very useful in continuous integration and continuous development (CI/CD).

Consider the following example scenario:

* Developers write code locally and share their work with colleagues using Docker containers.

* Developers use Docker to push applications into the test environment and perform automated and manual tests. 
When developers find errors, they can fix them in the development environment and redeploy them to the test environment for testing and verification.

* Once the test is complete, pushing the fix to the customer is as simple as pushing the updated image to the production environment.

**Responsive Deployment and Scaling**

Docker's portability and lightweight features also make it easy to dynamically manage workloads, expanding and shrinking applications and services in real-time as demanded.

**Run Multiple Workloads on a same Hardware**

Docker's lightweight and fast-running features allow us to do more with fewer resources and maximize the use of computer resources. 
Docker is ideal for high-density environments and small to medium-sized deployments.

##  Architecture of Docker

<div align=center>

![Docker Architecture](https://github.com/haoduoding/dist-sys-practice/blob/master/lab%20screenshots/docker%20arch.png?raw=true)

</div>

As we can see from the figure, Docker is a C/S architecture. 
The client interacts with the Docker daemon through the REST API, which pulls the image from the Registry (the repository, such as DockerHub), builds, runs, and distributes the container.

## Docker VS Vitual Machine

First, Docker is a container management technology, not a virtualization technology. 
It is fundamentally different from the virtual machines we know:

<div align=center>

![Docker And VM](https://github.com/haoduoding/dist-sys-practice/blob/master/lab%20screenshots/VM_vs_Docker.png?raw=true)

</div>

As you can see from the above figure, Docker is based on the Docker engine to share the hardware resources of the host, using the container to provide a stand-alone operating environment to run the application. 
The VM is based on the Supervisor (virtual hypervisor) using virtual machine technology to provide isolated virtual machines, providing operating environment on the virtual machine's operating system. 
While both provide good resource isolation, it's clear that Docker's virtualization overhead is lower.


<div align=center>

| Characteristic | Container | VM |
| :------| :------ | :------ |
| Start up | Second level | Minute level |
| Hard disk usage | ~MB | ~GB |
| Performance | Close to native | Worse than |
| System support | Stand-alone support for thousands of containers | Tens of |

</div>

## Core terminology

Below we will focus on some of the core terms that Docker involves: Registry, Image, Container, Stack, Service, and Swarm.

**Registry**

The Docker Registry is used to store Docker images. For example, Docker's official [Docker Hub](https://hub.docker.com/) is an open repository. 
Above we can find the image we want. Of course, we can also create a private mirror warehouse.

When we execute the ```Docker pull``` or ```Docker run``` command, if there is no required image locally, then an image will be downloaded from the repository (typically DockerHub). 
Docker executes the run method to get a container, and the user performs various operations in the container. 
Docker executes the commit method to convert a container into a mirror. 
Docker pushes the local image to the repository using commands such as login and push. 
This image can be used on other machines or servers to generate a container to run the corresponding application.
In addition, we can perform mirroring transactions in the [Docker Store](https://store.docker.com/).

**Image**

The image is self-reading and is used to create Docker containers.
We can commit ourselves to our own image after making some additional custom changes based on an image. 
You can also use Dockerfile to build our own image. Docker uses mirror layering technology, and each instruction in the Dockerfile is created as a layer in the image.

**Container**

The container is the most important concept in docker. 
Container is a running instance of mirror. It is an isolated, resource-controlled portable runtime environment, which contains the operating system, the programs that need to run, the dependencies of running programs, and the environment variables, etc. 
We can create a container for the specified image through ```docker run <image>```, which will attach a read-write layer to the image when the container is created. 
We can connect the container to one or more networks and attach storage to it, or create a new image based on its current state. 
Docker uses namespace technology to achieve isolation between containers. 
Changes to the container are temporary, and when the container is stopped, the corresponding changes are lost. 
We can persist the storage by mounting the volume.

**Docker Swarm**

Docker Swarm is the name of Docker's standalone native clustering tool. 
Docker Swarm clusters multiple Docker hosts and exposes them as a single virtual Docker host.

**Service**

Through the service we can do a good job of container expansion. 
By default, the service is load balanced between all working nodes under Swarm. 
In Docker we define, run, and extend services by writing ```docker-compose.yml```.

**Stack**
A Stack is a group of interrelated services that share dependencies and can be coordinated and scaled together. 
A single Stack can define and coordinate the functionality of the entire application.

This is my first time writing a technical report in the form of a blog. I hope I can do better in the future.

## References

[Docker Offcial Documents](https://docs.docker.com/engine/docker-overview/)

[Docker glossary](https://docs.docker.com/glossary/)





>>>>>>> origin/patch-5
