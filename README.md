# Distributed Systems Practice
Notes from learning about distributed systems in [GW CS 6421](https://gwdistsys18.github.io/) with [Prof. Wood](https://faculty.cs.gwu.edu/timwood/)

## Area 1: SDN and NFV
### SDN model
- A series of applications that decide how to forward the packets
- A networking operating system capable of coordinating forwarding devices
- A network of forwarding devices performing the required operations on the packets.

### SDN actions
- Modifying a packet
- Dropping a packet
- Tunnel the packet somewhere else

### Regular optimizations
- Future packets of the same type can take a fast path, don't need to consult the SDN controller.
- Flow entries will be cached to speed up processing.

### SDN Controller
- Topology service - how forwarding devices are connected with each other.
- Inventory service - track information about all SDN enabled devices.
- Statistics service - how many packets. etc, statistical information.
- Host tracking - IP and MAC addresses of the host.

### Applications:
- Java API
- Northbound (RESTConf)

### Other aspects
- Logically Centralized
- Not Physically Centralized
- Can have network operating systems
- Can have multiple ones
- Can have hierachy

### Advantages
- Logically centralizaed and have a global view of all SDN controllers.
- Applications are easier to program due to global view.
- SDN contoller and all devices exhibit themselves as a large switch.

### OpenNetVM
- Make network functions run as fast as possible.
- Process individual packets.

### ONVM: Run inside virtual machines
- More flexible in software
- Isolates functionality, easy to deploy and manage
- Slower than hardware

### Convergence of the research areas
- Operating systems
- Networking
- Security
- Modeling
- Real-time computing
- Stream processing

### OpenNetVM
- Platform for efficient packet processing in VMs and lightweight containers
- Highly optimized to reach ~70Gbps
- NF Manager -> Host's user space
- NFs run inside docker containers
- NUMA-aware processing
- Zero-copy data transfer between NFs
- No interrupts using DPDK poll-mode driver
- Scalable RX and TX threads in manager and NFs
- SDN-enabled NF Manager directs flows to NFs
- Fast enough to run software-based router, 38Gbps

### Packet processing in linux
- Lots of extra layers
- We in fact just need packet data
- Handle 14 million interrupts per second

### DPDK
- DMA to copy to user buffer.
- Polling for packet arrival.
- Regular function to transmit packets.
- Don't have native support for virtualization.

### Fast I/O
- Zero-copy packet forwarding
- Amortized system call overhead
- Compatible with libpcap and other standard libraries
- Much faster than linux native technology stacks

### Experiments:
1. List all devices using the ip command  
![1](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/1.List%20all%20devices%20using%20the%20ip%20command.png)
  
2. Configure the network interface  
![2](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/2.sudo%20dhclient%20ens38.png)

3. Check the IP address assigned to this interface  
![3](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/3.%20check%20the%20ip%20address%20assigned%20to%20ens38.png)

4. Edit the configuration file  
![4](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/4.edit%20configuration%20file.png)

5. Log into linux on windows using ssh  
![5](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/5.Windows%20logged%20into%20linux%20using%20ssh.png)

6.  Install the jre
![6](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/6.installing%20jre.png)

7.  Making up Java environment variable
![7](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/7.java%20env.png)

8.  Uncompressing ODL
![8](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/8.uncompressed%20opennetvm.png)

9.  Java 11 does not support this anymore :( switching to java 8
![8](https://raw.githubusercontent.com/hungry-foolish/dist-sys-practice/master/experiment/9.switching%20to%20java%208%20because%20java%2011%20no%20longer%20supports%20this.png)

10.  

11.  

12.  

13.  

14.  

15.  

16.  


## Area 2: Cloud Web Applications
### Launch an VM
- Launch an instance in the EC2 console.
- Configure and create the virtual machine instance.
- Connect to the instance
- Terminate the instance

### Storage
- Create a bucket
- Upload the file to a bucket
- Make the object public
- Create a bucket policy
- Upload a newer version and explore versioning


should be ovsk.
putty + Xming also works.
sudo mn --topo linear,3 --mac --controller=remote,ip=192.168.111.128,port=6633 --switch ovsk, protocols=OpenFlow13
