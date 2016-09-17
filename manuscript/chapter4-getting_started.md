# Getting Started with Docker

In this chapter, we are going to learn about docker shell, the command line utility and how to use it to
launch containers. We will also learn what it means to run a container, its lifecycle and perform basic
operations such as creating, starting, stopping, removing, pausing containers and checking the status etc.


### Using docker cli  
We can use docker cli to interact with docker daemon. Various functions of docker command is given below. Try this yourself by runnig **$sudo docker** command  

```
sudo docker
```  

[Output]  
```
Usage: docker [OPTIONS] COMMAND [arg...]
       docker [ --help | -v | --version ]

A self-sufficient runtime for containers.

Options:

  --config=~/.docker              Location of client config files
  -D, --debug                     Enable debug mode
  -H, --host=[]                   Daemon socket(s) to connect to
  -h, --help                      Print usage
  -l, --log-level=info            Set the logging level
  --tls                           Use TLS; implied by --tlsverify
  --tlscacert=~/.docker/ca.pem    Trust certs signed only by this CA
  --tlscert=~/.docker/cert.pem    Path to TLS certificate file
  --tlskey=~/.docker/key.pem      Path to TLS key file
  --tlsverify                     Use TLS and verify the remote
  -v, --version                   Print version information and quit

Commands:
    attach    Attach to a running container
    build     Build an image from a Dockerfile
    commit    Create a new image from a container's changes
    cp        Copy files/folders between a container and the local filesystem
    create    Create a new container
    diff      Inspect changes on a container's filesystem
    events    Get real time events from the server
    exec      Run a command in a running container
    export    Export a container's filesystem as a tar archive
    history   Show the history of an image
    images    List images
    import    Import the contents from a tarball to create a filesystem image
    info      Display system-wide information
    inspect   Return low-level information on a container, image or task
    kill      Kill one or more running containers
    load      Load an image from a tar archive or STDIN
    login     Log in to a Docker registry.
    logout    Log out from a Docker registry.
    logs      Fetch the logs of a container
    network   Manage Docker networks
    node      Manage Docker Swarm nodes
    pause     Pause all processes within one or more containers
    port      List port mappings or a specific mapping for the container
    ps        List containers
    pull      Pull an image or a repository from a registry
    push      Push an image or a repository to a registry
    rename    Rename a container
    restart   Restart a container
    rm        Remove one or more containers
    rmi       Remove one or more images
    run       Run a command in a new container
    save      Save one or more images to a tar archive (streamed to STDOUT by default)
    search    Search the Docker Hub for images
    service   Manage Docker services
    start     Start one or more stopped containers
    stats     Display a live stream of container(s) resource usage statistics
    stop      Stop one or more running containers
    swarm     Manage Docker Swarm
    tag       Tag an image into a repository
    top       Display the running processes of a container
    unpause   Unpause all processes within one or more containers
    update    Update configuration of one or more containers
    version   Show the Docker version information
    volume    Manage Docker volumes
    wait      Block until a container stops, then print its exit code

```

#### Getting Information about Docker Setup  
We can get the information about our Docker setup in several ways. Namely,  

```
docker -v  

docker version  

docker info  
```  

[Output of **docker -v**]  

```
Docker version 1.12.1, build 23cf638
```  

[Output of **docker version**]  

```
Client:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   23cf638
 Built:
 OS/Arch:      linux/amd64

Server:
 Version:      1.12.1
 API version:  1.24
 Go version:   go1.6.3
 Git commit:   23cf638
 Built:
 OS/Arch:      linux/amd64
```  

[Output of **docker info**]  
```
Containers: 10
 Running: 0
 Paused: 0
 Stopped: 10
Images: 8
Server Version: 1.12.1
Storage Driver: devicemapper
 Pool Name: docker-253:0-135975386-pool
 Pool Blocksize: 65.54 kB
 Base Device Size: 10.74 GB
 Backing Filesystem: xfs
 Data file: /dev/loop0
 Metadata file: /dev/loop1
 Data Space Used: 1.084 GB
 Data Space Total: 107.4 GB
 Data Space Available: 42.22 GB
 Metadata Space Used: 2.052 MB
 Metadata Space Total: 2.147 GB
 Metadata Space Available: 2.145 GB
 Thin Pool Minimum Free Space: 10.74 GB
 Udev Sync Supported: true
 Deferred Removal Enabled: false
 Deferred Deletion Enabled: false
 Deferred Deleted Device Count: 0
 Data loop file: /var/lib/docker/devicemapper/devicemapper/data
 WARNING: Usage of loopback devices is strongly discouraged for production use. Use `--storage-opt dm.thinpooldev` to specify a custom block storage device.
 Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
 Library Version: 1.02.107-RHEL7 (2016-06-09)
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins:
 Volume: local
 Network: bridge host null overlay
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Security Options: seccomp
Kernel Version: 3.10.0-327.28.3.el7.x86_64
Operating System: CentOS Linux 7 (Core)
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 1.797 GiB
Name: dockerserver
ID: QV4Z:HQZP:6ANK:PU5X:554Y:JA2Z:TZ54:ODDN:2HYJ:N4LW:WVZF:AG3L
Docker Root Dir: /var/lib/docker
Debug Mode (client): false
Debug Mode (server): false
Registry: https://index.docker.io/v1/
Insecure Registries:
 127.0.0.0/8

```  
The **docker info** command gives a lot of useful information like total number of containers and images along with information about host resource utilization  

### Launching our first container  
Now we have a basic understanding of docker command and sub commands, let us dive straight into launching our very first **container**  

```
docker run hello-world
```  

[Output]  
```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world

c04b14da8d14: Pull complete
Digest: sha256:0256e8a36e2070f7bf2d0b0763dbabdd67798512411de4cdcf9431a1feb60fd9
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker Hub account:
 https://hub.docker.com

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/

```  

**What happened?**  
This command will  
  * Pull the image file from **docker hub**, a cloud registry, about which we will explain in forthcoming chapters  
  * Create a container using that image  
  * Run an executable (called **hello-world**) inside that container  
  * Put that output to the terminal  
  * Exit out of the container  

**Where did my container go?**  

The point here to remember is that, when that executable stops running inside the container, the container itself will stop  
This process will further be explained under the **lifecycle of a container** topic. So don't bang your head by dwelling deep into this  

Let's see what happens when we run that command again,  

[Output]  
```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:

 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker Hub account:
 https://hub.docker.com

For more examples and ideas, visit:
 https://docs.docker.com/engine/userguide/

```  

Now docker no longer pulls the image again from registry, because **it has stored the image locally** from the previous run  
So once an image is pulled, we can make use of that image to create and run as many container as we want without the need of downloading the image again and again  

### Checking Status of the containers  

We have understood how docker run commands works. But what if you want to see list of running containers and history of containers that had run and exited? This can be done by executing the following commands  

```
docker ps
```  

[Output]  

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```  
This command doesn't give us any information. Because, **docker ps** command will only show list of container(s) which are **running**  

```
docker ps -l
```  

[Output]  

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
e2c4890c78da        hello-world         "/hello"            8 minutes ago       Exited (0) 8 minutes ago                       boring_jennings
```  
the **-l** flag shows the last run container along with other details like image it used, command it executed, return code of that command, etc.,  

```
docker ps -n 2
```  
[Output]  
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
adf9e6d80c13        busybox             "sh"                38 seconds ago      Exited (0) 37 seconds ago                       romantic_nobel
e2c4890c78da        hello-world         "/hello"            14 minutes ago      Exited (0) 14 minutes ago                       boring_jennings

```  
Docker gives us the flexibility to show the desirable number of last run containers. This can be achieved by using **-n #no_of_results** flag  

```
docker ps -a
```  

[Output]  

```
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS                      PORTS               NAMES
d2c3c5c52067        nginx               "nginx -g 'daemon off"   About a minute ago   Exited (0) 8 seconds ago                        modest_hodgkin
adf9e6d80c13        busybox             "sh"                     5 minutes ago        Exited (0) 5 minutes ago                        romantic_nobel
e2c4890c78da        hello-world         "/hello"                 18 minutes ago       Exited (0) 18 minutes ago                       boring_jennings
53d0b6c2f6c8        hello-world         "/hello"                 30 minutes ago       Exited (0) 30 minutes ago                       naughty_brattain

```  
This command will show all the container we have run so far.  

### Running Containers in Interactive Mode
We can interact with docker containers by giving -it flags at the run time. These flags stand for  
  * i - Interactive  
  * t - tty

```
docker run -it alpine:3.4 sh
```  

[Output]  

```
Unable to find image 'alpine:3.4' locally
3.4: Pulling from library/alpine

e110a4a17941: Pull complete
Digest: sha256:3dcdb92d7432d56604d4545cbd324b14e647b313626d99b889d0626de158f73a
Status: Downloaded newer image for alpine:3.4
/ #
```  

As you see, we have landed straight into **sh** shell of that container. This is the result of using **-it** flags and mentioning that container to run the **sh** shell. Don't try to exit that container yet. We have to execute some other commands in it to understand the next topic  

Namespaced:

Like a full fledged OS, Docker container has its own namespaces  
This enables Docker container to isolate itself from the host as well as other containers  

Run the following commands and see that alpine container has its own namespaces and not inheriting much from **host OS**  

[Command]  
```
cat /etc/issue
```  

[Output]  

```
Welcome to Alpine Linux 3.4
Kernel \r on an \m (\l)
```  

[Command]  
```
ps aux
```  

[Output]  

```
PID   USER     TIME   COMMAND
    1 root       0:00 sh
    6 root       0:00 ps aux
```  

[Command]  
```
ifconfig
```  

[Output]  

```
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02
          inet addr:172.17.0.2  Bcast:0.0.0.0  Mask:255.255.0.0
          inet6 addr: fe80::42:acff:fe11:2%32640/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:8 errors:0 dropped:0 overruns:0 frame:0
          TX packets:8 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:648 (648.0 B)  TX bytes:648 (648.0 B)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1%32640/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0
          RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
```  

[Command]  
```
hostname
```  

[Output]   

```
ae84d253ecb5
```  

Shared:  
We have understood that containers have their own namespaces. But will they share something to some extent? the answer is **YES**. Let's run the following commands on both the container and the host machine  

[Command]  
```
uname -a
```  

[Output - **container**]  

```
Linux ae84d253ecb5 3.10.0-327.28.3.el7.x86_64 #1 SMP Thu Aug 18 19:05:49 UTC 2016 x86_64 Linux

```

[Output - **hostmachine**]  

```
Linux dockerserver 3.10.0-327.28.3.el7.x86_64 #1 SMP Thu Aug 18 19:05:49 UTC 2016 x86_64 x86_64 x86_64 GNU/Linux
```  

As you can see, the container uses the same Linux Kernel from the host machine. Just like **uname** command, the following commands share the same information as well. In order to avoid repetition, we will see the output of container alone.

[Command]  
```
date  
```  

[Output]    

```
Wed Sep 14 18:21:25 UTC 2016
```  

[Command]  
```
cat /proc/cpuinfo
```  

[Output]    

```
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 94
model name      : Intel(R) Core(TM) i7-6700HQ CPU @ 2.60GHz
stepping        : 3
cpu MHz         : 2592.002
cache size      : 6144 KB
physical id     : 0
siblings        : 1
core id         : 0
cpu cores       : 1
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 22
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 syscall nx rdtscp lm constant_tsc rep_good nopl xtopology nonstop_tsc pni pclmulqdq monitor ssse3 cx16 sse4_1 sse4_2 movbe popcnt aes xsave avx rdrand hypervisor lahf_lm abm 3dnowprefetch rdseed clflushopt
bogomips        : 5184.00
clflush size    : 64
cache_alignment : 64
address sizes   : 39 bits physical, 48 bits virtual
power management:
```

[Command]  
```
free
```  

[Output]  

```
total       used       free     shared    buffers     cached
Mem:       1884176     650660    1233516          0       1860     473248
-/+ buffers/cache:     175552    1708624
Swap:      1048572          0    1048572

```  

Now exit out of that container by running **exit** or by pressing **ctrl+d**  


### Making Containers Persist  
#### Running Containers in Detached Mode  
So far, we have run the containers interactively. But this is not always the case. Sometimes you may want to start a container  without interacting with it. This can be achieved by using **"detached mode"** (**-d**) flag. Hence the container will launch the deafault application inside and run in the background. This saves a lot of time, we don't have to wait till the applications launches successfully. It will happen behind the screen. Let us run the following command to see this in action  

[Command]  

```
docker run -d schoolofdevops/loop program
```  

-d , --detach : detached mode  

[Output]  

```
2533adf280ac4838b446e4ee1151f52793e6ac499d2e631b2c752459bb18ad5f
```  
This will run the container in detached mode. We are only given with full container id as the output  

Let us check whether this container is running or not  
[Command]  
```
docker ps
```  

[Output]  

```
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS               NAMES
2533adf280ac        schoolofdevops/loop   "program"           37 seconds ago      Up 36 seconds                           prickly_bose
```  
As we can see in the output, the container is running in the background  

#### Connecting to running container to execute commands
We can connect to the containers which are running in detached mode by using these following commands  
[Command]  
```
docker exec -it 2533adf280ac sh
```  

[Output]  

```
/ #
```  
Now exit the container.  

#### Pausing Running Container  
Just like in a video, it is easy to pause and unpause the running container  
[Command]  

```
docker pause 2533adf280ac
```  

After running pause command, run docker ps again to check the container status  

[Output]  

```
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS                  PORTS               NAMES
2533adf280ac        schoolofdevops/loop   "program"           2 minutes ago       Up 2 minutes (Paused)                       prickly_bose
```  

#### Unpausing the paused container  
This can be achieved by executing following command  

[Command]  
```
docker unpause
```  

Run docker ps to verify the changes  

[Output]  

```
CONTAINER ID        IMAGE                 COMMAND             CREATED             STATUS              PORTS               NAMES
2533adf280ac        schoolofdevops/loop   "program"           6 minutes ago       Up 6 minutes                            prickly_bose
```  

### Creating and Starting a Container instead of Running  
docker **run** command will create a container and start that container simultaneously. However docker gives you the granularity to create a container and not to run it at the time of creation. However, This container can be started by using **start** command  

[Command]  

```
docker create alpine:3.4 sh
```  

Run **docker ps -l** to see the status of the container  

[Output]  

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
22146d15eb71        alpine:3.4          "sh"                31 seconds ago      Created                                 grave_leavitt
```  

If you do **docker ps -l**, you will find that container status to be **Created**. Now lets start this container by executing,   

[Command]  

```
docker start 22146d15eb71
```  
Run docker ps -l again to see the status change  

[Output]  

```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
22146d15eb71        alpine:3.4          "sh"                3 minutes ago       Exited (0) 2 minutes ago                      grave_leavitt
```  
This command will start the container and exit right away we have not specified interactive mode in the command  

### Creating Pretty Reports with Formatters
```
docker ps --format "{{.ID}}: {{.Status}}"
```

[Output]  

```
2533adf280ac: Up 12 minutes
```  

### Stopping and Removing Containers
We have learnt about interacting with a container, running a container, pausing and unpausing a container, creating and starting a container. But what if you want to stop the container or remove the container itself  

#### Stop a container  
A container can be stopped using **stop** command. This command will stop the application inside that container hence the container itself will be stopped. This command basically sends a **SIGTERM** signal to the container (graceful shutdown)  

[Command]  

```
docker stop 2533adf280ac
```  
[Output]  

```
2533adf280ac
```  
#### Kill a container  
This command will send **SIGKILL** signal and kills the container ungracefully  

[Command]  

```
docker kill 590e7060743a
```  

[Output]  

```
590e7060743a
```  
If you want to remove a container, then execute the following command. Before running this command, run docker ps -a to see the list of pre run containers. Choose a container of your wish and then execute docker rm command. Then run docker ps -a again to check the removed container list or not  

[Command]  

```
docker rm 590e7060743a
```  

[Output]  

```
590e7060743a
```  
