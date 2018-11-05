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
1. 

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
