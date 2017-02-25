# Criu and P.Haul on the Raspberry Pi 2

Step 1:
Arch Linux is not supported with Criu due to the lack of checkpoint and restore functionality within the Kernel. Therefore a custom kernel needs to be built.
My version of the customer config can be pulled from this repo.

Else, if you would like to do this yourself, taken from the Criu installation page (https://criu.org/Installation). 
These will be under different headings in the config file:
* General setup options
    * CONFIG_CHECKPOINT_RESTORE=y (Checkpoint/restore support)
    * CONFIG_NAMESPACES=y (Namespaces support)
    * CONFIG_UTS_NS=y (Namespaces support -> UTS namespace)
    * CONFIG_IPC_NS=y (Namespaces support -> IPC namespace)
    * CONFIG_PID_NS=y (Namespaces support -> PID namespaces)
    * CONFIG_NET_NS=y (Namespaces support -> Network namespace)
    * CONFIG_FHANDLE=y (Open by fhandle syscalls)
    * CONFIG_EVENTFD=y (Enable eventfd() system call)
    * CONFIG_EPOLL=y (Enable eventpoll support)
* Networking support -> Networking options options for sock-diag subsystem
    * CONFIG_UNIX_DIAG=y (Unix domain sockets -> UNIX: socket monitoring interface)
    * CONFIG_INET_DIAG=y (TCP/IP networking -> INET: socket monitoring interface)
    * CONFIG_INET_UDP_DIAG=y (TCP/IP networking -> INET: socket monitoring interface -> UDP: socket monitoring interface)
    * CONFIG_PACKET_DIAG=y (Packet socket -> Packet: sockets monitoring interface)
    * CONFIG_NETLINK_DIAG=y (Netlink socket -> Netlink: sockets monitoring interface)
* Other options
    * CONFIG_INOTIFY_USER=y (File systems -> Inotify support for userspace)


Once the config has been created, full kernel needs to be built cross-compiled for ARM including modules and firmware.

Custom images from the kernel and custom modules need to be put onto the Raspberry Pi, then rebooted to the new Kernel.

Step 2:
Download and install criu:
As root: getCriuDeps
Then
As standard user: getCriu
(This will clone the criu and p.haul repo and install)

Finally,
edit p.haul/service and p.haul/wrap
and change #!/usr/bin/env python
to #!/usr/bin/env python2



