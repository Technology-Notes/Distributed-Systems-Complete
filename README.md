 Distributed Systems Practice

Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

# Cloud Web Applications

### Virtualization

- Two different level of privilege to run on computers (Software)
  - Operating system
    - Use instructions
    - Access memory
    - Avoid the applications either maliciously or accidentally
  - Applications
    - Crashes won't take out the whole machine
- Hardware mechanism called Kernel mode Supervisor mode: ring 0
- If run multiple virtual machines on operating system and then run applications on top of that
  - The operating system is running on **user mode**
    - It will try to issue instructions and access things that it doesn't have permissions
    - The hardware provides easy-virtualized instructions
- Hypervisor runs on ring 0, the guest OS traps into the operating system
  - The performance of software emulation is not great
    - More instructions
    - Need to provides protections between domains

### Practice

>  I want to know how many companies actually see my online resume. Thanks to the tutorial I could build a small service for my resume page, which is a pure front end page like github.io, to record the visit history

The note in this section would implement the "record visit" function, separately,  using

- LAMP - provide interface to add record for a website

#### Launch a VM

- Amazon Linux 2 AMI (HVM), SSD Volume Type - ami-0922553b7b0369273

#### Use S3 service to store the records

No permission. Skipped

#### Use LAMP server to record visits of a website

1. Follow the installation instruction to install `php, apache` and the relevant services

2. In **Security Group**, add In **bound Rule** for http/https service

3. Start server. It works

   ![Screen Shot 2018-10-24 at 5.08.03 PM](/Users/zhengxiangyue/Projects/dist-sys-practice/static/1.png)

4. Install **mariadb** and db management tool phpmyadmin

   ![Screen Shot 2018-10-24 at 5.20.10 PM](/Users/zhengxiangyue/Projects/dist-sys-practice/static/2.png)

5. Build a simple project to provide "add record" interface

   ```
   cd /var/www/html
   touch interface.php
   ```

   Allow some other domains to access the script

   ```php
   <?php
   header("Access-Control-Allow-Origin: *");
   ```

   Allow specific client domain to access

   ```php
   $config = array(
       'allow_hosts' => [
           'ec2-54-172-123-139.compute-1.amazonaws.com',
           'zhengxiangyue.github.io'
       ],
   );
   
   if ($_SERVER['HTTP_REFERER'] != null && !in_array(parse_url($_SERVER['HTTP_REFERER'], PHP_URL_HOST), $config['allow_hosts'])) {
       http_response_code(404);
       exit();
   }
   ```

   Create a database and tables for recording website visit record

   ```mysql
   CREATE TABLE `website_visit`.`record` ( 
       `id` INT NOT NULL AUTO_INCREMENT COMMENT 'ai_id' , 
       `info` TEXT CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL COMMENT 'record information in json' , 
       `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP , 
       PRIMARY KEY (`id`)) ENGINE = InnoDB;
   ```

   > Where `info` is a json format string that record the information we would love to record

   Write a simple database connector

   ```php
   class Database
   {
       private static $dbName = 'website_visit' ;
       private static $dbHost = 'localhost' ;
       private static $dbUsername = 'root';
       private static $dbUserPassword = '********';
   
       private static $cont  = null;
   
       public function __construct() {
           die('Init function is not allowed');
       }
   
       public static function connect()
       {
           // One connection through whole application
           if ( null == self::$cont )
           {
               try
               {
                   self::$cont =  new PDO( "mysql:host=".self::$dbHost.";"."dbname=".self::$dbName, self::$dbUsername, self::$dbUserPassword);
               }
               catch(PDOException $e)
               {
                   die($e->getMessage());
               }
           }
           return self::$cont;
       }
   
       public static function disconnect()
       {
           self::$cont = null;
       }
   
       public static function create($table, array $fields, array $values) {
   
           $numFields = count($fields);
           $numValues = count($values);
   
           if($numFields === 0 or $numValues === 0)
               throw new Exception("At least one field and value is required.");
           if($numFields !== $numValues)
               throw new Exception("Mismatched number of field and value arguments.");
   
           $fields = '`' . implode('`,`', $fields) . '`';
           $values = "'" . implode("','", $values) . "'";
           $sql = "INSERT INTO {$table} ($fields) VALUES($values)";
   
           return self::$cont->prepare($sql) and self::$cont->exec($sql);
       }
   
   }
   ```

   When there is a request, record all information in `$_SERVER`

   ```php
   Database::connect();
   Database::create('record', array('info'), array(json_encode($_SERVER)));
   Database::disconnect();
   ```

   Add a a-synchronize request on the front page

   ```javascript
   $.ajax({
       url: 'http://ec2-54-172-123-139.compute-1.amazonaws.com/interface.php',
       success: function(result){
           console.log(result);
       }
   });
   ```

6. Check the result

   ![Screen Shot 2018-10-24 at 6.54.59 PM](/Users/zhengxiangyue/Projects/dist-sys-practice/static/3.png)



![Screen Shot 2018-10-24 at 6.55.43 PM](/Users/zhengxiangyue/Projects/dist-sys-practice/static/4.png)

> Great, now at least I know how many employers have checked my resume, or even their IP address to locate the company

1. During this process, some problems need to be pay attention to
   - Modify header to allow cross domain access
   - Http connection(our service) is not allowed through an https connection(front page), to solve this problem
     - Use https in the service url even though our service is not. This will cause the connection not a trusted connection
     - Configure our service to be an https connection
     - Both use http connections

The site which is using the service: https://zhengxiangyue.github.io/resumeGeneral/
And the site simply show the records: https://http://ec2-54-172-123-139.compute-1.amazonaws.com/show.php

Unfortunately, I do not have permission to create either `DynamoDB` with `Node.js` or  `S3 `with` AWS SDK`, which may also be used as backend script and database.

# Big Data and Machine Learning

- The solution to manage large amount of data is to use more machines, a distributed system
- A distributed system take less time to process data. But challenges are
  - high chances of system failure
  - High programming complexity
- Hadoop is a framework that allows for distributed processing of large data sets across clusters of commodity computers using simple programming models
  - high chances of system failure
  - High bandwidth problem
  - High programming complexity
- 4 key characteristics of Hadoop
  - Economical
    - Ordinary computers can be used for data processing
  - Reliable
    - Stores copies of the data on different machines and is resistant to hardware failure
  - Scalable
    - Can follow both horizontal and vertical scaling
  - Flexible
    - Can store as much of the data and decide to use it later
- Hadoop ecosystem
  - HDFS
    - A storage layer for Hadoop
    - Suitable for the distributed storage and processing
    - Hadoop provides a command line interface to interact with HDFS
    - Streaming access to file system data
    - Provides file permissions and authentication
  - HBASE
    - Stores data in HDFS
    - A NoSQL database or non-relational database
    - Mainly used when you need random, real-time, read/write access to your Big Data
    - Provides support to high volume of data and high throughput
    - The table can have thousands of columns
  - Sqoop
    - A tool designed to transfer data between Hadoop and relational database servers
    - It is used to import data from relational databases such as, Oracle and MySQL to HDFS and export data from HDFS to relational databases
  - Flume
    - A distributed service for ingesting streaming data
    - Ideally suited for event data from multiple systems
  - Spark
    - Provides 100 times faster performance as compared to MapReduce
    - Apache Spark
      - Spark Core and Resilient Distributed Datasets(RDDs)
      - Spark SQL
      - Spark Streaming
      - Machine Learning Library
      - GraphX
  - MapReduce
    - Based on the map and reduce programming model
    - An extensive and mature fault tolerance framework
  - Pig
    - An dataflow system
    - Converts the scripts to Map-Reduce code
  - Impala
    - High performance SQL engine runs on Hadoop cluster
    - Ideal for interactive analysis
    - Very low latency - measured in milliseconds
    - Supports a dialect of SQL
  - Hive
    - For data processing and extract transform load(ETL)
  - Cloudera
    - Nera rea-time access
    - Users do not need SQL or programming skills
    - A fully integrated data processing platform
  - Oozie is a workflow or coordination system used to manage the Hadoop jobs
  - Hue
    - Web interface for analyzing data with Hadoop
- Review 4 steps to process big data
  - Ingest
    - The data is transferred or ingested into hadoop from various sources such as
      - Relational databases
      - systems
      - Local files
    - `Scqop` transfers from RDB management system to HDFS
    - `Flume` transfers event data
  - Processing
    - Data stored in distributed file system `HDFS` and the NoSQL distributed data HBase
    - `Spark` and `MapReduce` perform the data processing
  - Analyze
    - Frameworks such as `Pig`, `Hive` and `Impala`
    - Converts data using map reduce, then analyze it
    - Hive is 
      - base on map reduce programming 
      - Most suitable for structured data
  - Access
    - `Hue`, `cloudera search`
      - Hue is the web interface
      - Clouderas provides a text interface for exploring data

# Containers and VMs

### Pre-knowledge summary

The operating system structure can be simplified to: OS = Kernel + apps. 

The kernel is responsible for **managing the low level hardware**, including CPU, memory, IO devices and providing interfaces(system call). Upper level apps use the hardware resource through system call. 

The **apps(user interface)** may include shell, GUI, services, package management tool(Windows graphics interface is integrated into the kernel while Linux not). The apps are different from what we manually install  onto the operating system.

A kernel with different apps are called different distribution(Ubuntu, Red Had). So the differences of distributions are the apps environments. A package consist of apps is called **image**.

### Docker

The main attributes of docker:

- Flexibility: Both lightweight and complex apps environment can be packaged and containerized
- Lightweight: The containers in the same host share OS kernel so it's lightweight and fast(comparing to VMs)

A container is started by running an image. An image contains the runtime code, libraries, configuration files. A container is a runtime instance of an image.

A **container** runs natively on Linux and shares the kernel of the host machine with other containers

### Docker Architecture

The main modules of Docker architecture include: DockerClient, DockerDaemon, Docker Registry, Graph, Driver, libcontainer and Docker Container.

#### Docker Client

Docker client is provide the communication with Docker Daemon. The executable file "docker" is the way to start Docker Client, we could use docker command to send management request to the docker daemon.

There are three types of communication methods for Docker Client and Docker Daemon:

- Tcp://host:port (http is commonly used in communication between Docker Client and Docker Daemon)
- Unix://path_to_socket
- Fd://socketdf

After the management request is sent from Docker Client, Docker Daemon receives and processes the request. When Docker Daemon returns, Docker Client end its lifespan.

#### Docker Daemon

Docker Daemon is a System Process that keeps running in the background, The main functions of Docker Daemon are:

- Receive requests from Docker Client
- Manage all Docker Containers

After Docker Daemon start, a server will be launched in the background, receiving the requests and distribute the request to the corresponding handler.

The executable file to start Docker Daemon is also "docker", the same as when starting the Docker Client. Different functions will be called by setting parameters.

The architecture of Docker Daemon could be generalized as: **Docker Server**, **Engine** and **Job**

##### Docker Server

Docker Server is dedicated to serve Docker Client, it receive, schedule and distribute the request from Docker Client. If TCP/IP is used, Docker Server is actually an **http server**. Docker is written in Go, and the package gorilla/mux is used as the router module.

For each Docker Client request, Docker Server will create a new service(goroutine), it is responsible for finding the corresponding handler(Job) to process the request and finally response to Docker Client 

##### Engine

Engine stores the information of containers, and manage the execution of most Jobs. In the source code, there is an object called "handlers", the object stores the corresponding handler of each Job. For example, {"create", daemon.ContainerCreate} indicates when Job "create" is requested, the handler "daemon.ContainerCreate" will be launched.

##### Job

Job is the basic execution unit in Docker, every task Docker Daemon accomplish is connected to a specific Job. For example, 

- Run a process in a Docker Container
- Create a new container
- Download a file through internet

are all different Jobs

The Job interface design is similar to Unix process. Each Job has a name, runtime parameters, environment variables, standard input/output/error, return status etc.

#### Docker Registry

Docker Registry is a warehouse storing Docker Images. Docker Images contains the file systems' content used when creating a container.

When Docker is running, three kinds of possible communication with Docker Registry exist, they are searching image, download image and upload image. The name of the three jobs are search, pull and push. Docker Daemon may use different Docker Registry. Public registry and private registry are two kinds of Registries. Docker access Docker Hub through the internet, user can also build local private Registry.

#### Graph

The role of Graph in Docker is custodian of container image. Images are managed by Graph, no matter they are downloaded or constructed locally. Graph provides management for many types of different image like "aufs", "devicemapper", "Btrfs".

- The same type of images are called "repository". 
  - all images named Ubuntu belong to the same repository
- Images within the same repository show some difference based on different tags
  - Ubuntu with tag 12.04 and with tag 14.04 are different images in the same repository

#### Driver

Driver provide the ability of customizing the runtime environment of Docker Container. Mainly includes:

- Network environment
- Storage method
- Container execution mode 

The implementation of Docker Driver mainly contains three parts:

- **graphdriver**
- **networkdriver**
- **execdriver**

Graphdriver is mainly used to implement the management(download, save) of container image. 

- When user download a specific container image, graphdriver stores the container image hierarchically in a local directory
- When user need to construct containers with specified container image, graphdriver fetches the container image from the local storage, and prepare rootfs for the container
- When user need to construct new container image through Dockerfile, graphdriver is responsible for storage management of new images

Four types of file system drivers will be registered in DockerDaemon before graphdriver initialized

- aufs
- btrfs
- vfs
- devmapper

Aufs, btrfs and devmapper are used to manage container images. Vfs is used to mange container volume. Before initialing Docker, the environment variable DOCKER_DRIVER will be fetched to specify the type of driver. All Graph operations are based on this driver later on.



Networkdriver configures the Docker Container's network environment, including:

- Create network bridge when Docker Daemon is launching
- Allocate network interface resources before Docker image launch
- Assign Docker Container IP, ports and NAT port mapping with host machine
- Configure firewall



As the execution driver of Docker container, execdriver is responsible for 

- Create runtime namespace for container
- Statistics and restrictions on the use of container resources
- Run the actual internal process of the container



> Before Docker 0.9.0, execdriver managed containers based on **LXC drivers** and control the container lifespan. After 0.9.0, **native driver** is used



#### libcontainer

The original interntion of the design is to hope that the library can directly access the container-related system calls in the kernel without relying on any other dependencies. Because the existence of libcontainer, Docker could operate the container's namespaces, cgroups, apparmor, network devices and firewall rules. The operations don't rely on LXC or other packages.

Libcontainer provides a complete set of standard interfaces to meet the needs of upper management of containers, it **blocks the direct management of containers form top of Docker**.

#### Docker container

Docker container is the final embodiment of service delivery in the Docker architecture

DockerDaemon management -> libcontainer execution -> Docker Container creation

The functionality of Docker Container is similar to a Virtual Machine, with attributes such like the limitation of resources and isolation. But the implementation is totally different from KVM, Xen

User may configure Docker container in 4 dimensions:

- By specifying a container image, the Docker container can customize file systems such as rootfs. 
- By specifying a quota for physical resources, such as CPU, memory, etc., making Docker containers Use restricted physical resources.
- By configuring the container network and its security policies, Docker containers have an independent and secure network environment 
- By specifying a command for the container, the Docker container performs the specified task.

### Docker command pratice

#### Docker pull

Docker Daemon download specified container image from Docker Registry and save it to local Graph, for the purpose of later creation of the same container, the procedures of docker pull are:

1. Docker Client send an http request to Docker Server, POST: /images/create?imageIdentifier
2. mux.Router determines the specific handler that executes the request by its URL and the type of the request method.
3. The handler that handle "docker pull" is PostImagesCreate
4. The handler will create and initialize a Job called "pull"
5. Job "pull" download the specified Docker Image from Docker Registry via pullRepository
6. Job "pull" deliver the downloaded Docker image to graphdriver
7. Graphdriver is responsible for storing Docker images, on the one hand storing the actual image to the local file system, and on the other hand creating objects for the image, managed by the Docker Daemon.   

#### Docker Run

Docker run will create a new Docker Container and run the specified command in Docker Container.

When Docker Daemon process the user command, there are two parts:

1. Create Docker Container Object, prepare rootfs for the container
2. Create runtime environment for container such as network environment, resource limitations etc. and finally run the user command

So, during the process of "docker run", Docker Client send two http requests to Docker Server. The details are shown:

1. Docker Client send a post request to Docker Server, the URL is containers/create?identifier. 
2. mux.Router determines the specific handler that executes the request by its URL and the type of the request method.
3. The handler that handle "docker pull" is PostContainersCreate
4. The handler will create and initialize a Job called "create"
5. The job named "create" executes the Container.Create operation during the run, which requires the container image to prepare rootfs for the Docker container, done by graphdriver.
6. The graphdriver gets all the images needed to create the Docker container rootfs from the Graph.
7. Graphdriver loads all images of rootfs into the file directory specified by the Docker container through some sort of file system
8. If all of the above operations are performed normally and no error or exception is returned, the Docker Client will initiate a second HTTP request after receiving the Docker Server return status. The request method is "POST", and the request URL is "/containers/"+container ID+"/start". The actual meaning is the container object created at startup, realizing the real operation of the physical container.
9. Docker Server receives the above HTTP request and hands it to mux.Router, mux.Router via URL and the method is requested to determine the specific handler that executed the request.
10. mux.Router distributes the request route to the corresponding handler, specifically PostContainersStart.
11.  In the PostContainersStart handler, create and initialize a job named "start", then touch
    Issue the job.
12. Job execution named "start" needs to complete a series of configuration tasks related to Docker containers, one of which is allocating network resources, such as IP resources, for the Docker container network environment is done by calling networkdriver
13. networkdriver allocates network resources for the specified Docker container, including IP, po, etc.
    Set firewall rules
14. Return the Job named "start". After performing some auxiliary operations, the Job starts executing the user command and calls Execdriver
15. execdriver is called to start initializing the running environment inside the Docker container, such as namespace, resource control system and isolation, as well as the execution of user commands, the corresponding operations are handed over to libcontainer to complete.
16. The libcontainer is called to complete the runtime initialization of the Docker container and finally execute the commands requested by the user.

### Docker Image

Image is a form of file storage. For virtual machines, image contains Operating System, File System, device files while Docker image has show some similarity but is essentially different

- Similarity: both contains file system
- Difference: Docker image doesn't contain operating system(kernel)

There are 4 related concepts: rootfs, union mount, image and layer

#### rootfs

Rootfs represents the **file system perspective** of a Docker container that is visible to its internal processes at startup (rather than after running), or the root directory of the Docker container. The directory contains system files, tools, container files.

Traditionally, when the Linux operating system kernel is started, the kernel first mounts a read-only rootfs.

When detects its integrity, the system would decide whether to switch it to read-write mode, or mount a file system on top of rootfs and ignore rootfs

Instead of setting the file system of the Docker container to read-write mode, Docker Daemon uses the technology of Union Mount to mount a read-write file system on top of this read-only rootfs.

 Docker container's file system could be seen as: a file system with only read-only rootfs and read-write file system

#### Union Mount

Union Mount represents a file system mount method that allows multiple file system overlays to be mounted together at the same time.

In normal circumstances, if we mount content to a mount point through a file system, the original content in the mount point directory will be hidden. But Union Mount does not hide the contents of the mount point directory. Instead, the contents of the mount point directory are merged with the mounted content, and a unified independent file system perspective is provided for the merged content.

(Last update Dec 9, To be continued)



