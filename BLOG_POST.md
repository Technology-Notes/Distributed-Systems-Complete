# Virtual machine VS Containers: Which one is the best fit?
- Author: Runyu Pan

## Introduction to virtual machines
### Concept
  Virtual machines are completely isolated fully functional computer hardware pieces simulated by a software, which we usually call the virtual machine monitor. The virtual machine looks just like a physical machine when the guest operating systems is running, and this is where this technology gets its name. A virtual machine includes a full operating system, optentially with a large number of drivers and middlewares, and may also be packed with some applications. In traditional virtual machine technology, if different operating systems or operating system distros are needed, a different virtual machine is required.  

### Abstraction level
  The abstraction layer lies between the physical hardware and the guest operating systems. The interface exposed is identical to, or very similar to that of the underlying physical machine. Some architectures also provide hardware support for virtualization, which drastically improves performance.  

- Full virtualization  
  Full virtualization provides the OS with an interface that is 100% same with the underlying hardware. This guarantees 100% compatibility with all software on the given architecture, and can run unmodified operating system binaries out of the box. If the VMM hides itself even better, there is no sign that the guest OS can detect to know whether itself is being virtualized.  

- Paravirtualization  
  Paravirtualization, on the other hand, supplies a slightly modified interface called hypercalls. These hypercalls are typically used to replace priviledged instructions that are hard to fully virtualize with efficiency. This requires explicitly modifying the operating system source, and can only be applied to open-source operating systems. Some proprietary operating systems also have paravirtualized ports for famous paravirtualizing hypervisors like Xen, but this is not the common case.  

### Types
- Simulator  
  This type of VMM simply reads the system image binary, interprets them, and step forward instruction by instruction. These hypervisors have virtually no speed and is only useful for operating system engineers and driver developers. If you need to run stuff on a completely different architecture from what it was compiled for, this is probably your only choice. Currently there are some VMMs like Qemu that are capable of running x86 binaries on ARM-powered android phones and can boot Windows.  

- Type 1  
  This type of hypervisor directly targets the underlying physical hardware, and hosts guest OSes. This type of hypervisor need a priviledged Dom0 to manage its resources, provide (some) drivers, and have a higher efficiency. Yet, they is slightly more difficult to configure and maintain than Type 2 for personal users.  

- Type 2  
  This type of hypervisor must be installed on a host OS thus shares resource with it. Products like VMWare workstation and Virtualbox come just out of the box, have a fabulous graphical user interface, are super easy to install, configure and use, but have a little more overhead than Type 1.  
  
### Distinct idiosyncrasies
- Strengths  
  - The interface simulated is identical to (full-virtualization) or very close to (paravirtualization) hardware, which leverages many vintage software repos.  
  - Highly isolated and secure - the trojans and viruses must break the VMM, which is simple and realtively hard to compromize, to defect the whole system.  
  - Can make snapshots - save and restore your whole machine state.  
  - Can use different kernels - run windows alongside your linux applications.  

- Weaknesses  
  - Relatively high overhead, both in space and time: full OS and lots of low-level configurations.  
  - Heavy weight: OS have a big image, and typically on the order of GBs. If you strip them down really hard, you may be able to get a image on 100MBs magnitude.  
  - There are some image standards, but are far from really converged - if you export virtual box images then import them in VMWare, you are likely to be stuck somewhere.  

## Introduction to containers
### Concept
  The word "Container" previously referred to large cargo boxes that can be easily packed, lifted and moved. The Container technology, in the computer science realm, was implemented in 2008 to solve a similar software stack packing problem. It can be regarded as a very light-weight virtualization that only happens on the middleware and application layer. To date, this technology have been made possible on many operating systems, Windows included, yet the Linux variant is more prevalent. Linux containers (LXC) are implemented mainly by leveraging "cgroups" and namespacing.  

  By using this technology, we can separate different software stacks, and we only need to share the kernel itself. This makes it possible to run different distributions of the same operating system kernel together without complicated software compatibility tuning. Of all the Linux container variants, Docker is the most pronounced and can be regarded as a synonym of container technology, at least to some extent.  

### Abstraction level
  The abstraction layer lies between the operating system kernel and the middleware. The applications and the middlewares are the only stuff that are distinct between different distros; thus it is possible to run different distros on the same kernel. Because we do not need to simulate a full physical machine, this technology is significantly lighter-weight, and are less resource-hungry. All systems calls are just plain system calls; no extra overhead of any kind is imposed. Additionlly, networking is easy to configure, and no complex bridging (virtual driver, etc.) is required. A container only carries the needed binaries and are expremely small; when packed, they can be deployed anywhere; if the binaries and creation procedures are all standard, a description file which is kBs only will suffice specifying it. Containers are also easier to scale than VMs which makes them a perfect fit for microservices.  

  However, these containers must share the same kernel, thus this will not help kernel developers at all. To make things worse, if you want a container to include some kernel modules, you are probably out of luck - the whole stack must be at user-level! You will have to install the kernel module or driver on the host machine instead. This also implies that it is (almost) impossible to host Windows containers on Linux without some serious work.  

### Use cases
  Many tech corps are now switching to containers for many reasons. Some of these companies focus on containerizing traditional applications to boost their security and lower maintence costs. This transitions usually makes service expansion easier. Some other companies leverage docker as a delivery package, and places their software product inside it. This speeds up the whole development process and encourages the agile development approach.  

  More complex use cases includes microservicing the server-side model, and thus boosting the utilization of IT infrastructure. Microservices are known to scale better than their monolithic counterparts. Different portions of the services may have different number of replicas, which is more flexible, and also does better in fault tolerance and security as these small modules require less priviledge.  

### Distinct idiosyncrasies
- Strengths  
  - Lightweight - only include what you need.  
  - Fast - milliseconds to boot a instance.  
  - Easy to maintain - easily upgradeable by commits.  
  - Immensely scalable - perfect for microservices.  
- Weaknesses  
  - Bad security - shared kernel; if there is one malicious kernel module or a kernel-compromizing virus, no containers are safe.  
  - No kernel deviations - shared kernel; all applications assume the same system call interface.  
  - Difficult to configure drivers and kernel modules - container stack is completely user-level.  

## PK: VMs vs. Containers
### Key differences
  From the discussions above we can see that the distinct difference between containers and VMs are the abstraction layer position. For containers, the abstraction layer is at the middleware level, while for VMs the abstraction layer is at hardware level. We can easily see that the hardware interface is simpler than the system call layer, yet system call layer have richer functionality than the hardware abstraction layer. The less complex the interface, the less code it takes to virtualize it; the farther from the application, the more overhead it will incur. Thus, the containers are inherently lighter-weight than virtual machines, yet virtual machines are more secure than containers. Moreover, virtual machines have a much lower level interface, thus have more compatibility between different operating systems; containers, on the other hand, cannot use different kernels but are more efficient.  

  There are also other subtle differents: containers have a open standard that many manufacturers adhere to. Virtual machine formats are practically never unified and cannot be converted to each other easily.  

## Which one is the best choice?
  From all the analysis above we can see that there is no obvious "better" one. If more security and flexibility is desired, choose VMs; if speed and space is at a premium, go for containers. Last but not least, the container technology and the virtual machine technology are completely orthogonal. If desired, you can deploy containers in virtual machines as well, which gets the best of both worlds at the cost of a little added complexity.  

