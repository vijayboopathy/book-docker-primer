# Managing Containers - Learning about Common Container Operations

In the previous chapter we learnt about container lifecycle management including how to create, launch, connect to, stop and remove containers. In this chapter, we are going to learn how to launch a container with a pre built app image and how to access the app with published ports. We will also learn about common  container operations such as inspecting container information, checking logs and performance stats, renaming and updating the properties of a container, limiting resources etc.  


As part of the tutorial, we are going to setup a shiny new blogging/publishing site. To set it up we will use a node.js based framework called **ghost**, a simple, fast, and SEO friendly alternative to more sophisticated publishing platforms such as wordpress. However, its purely gives us a blogging platform.

### Launching a container with a pre built app image


``` docker run -d -P ghost:0.10.1 ```
``` docker ps ```


Check the ip address of docker host.
If using docker-machine,  

``` docker-machine ip default ```

Find out the port mapping

```
docker port ghost  
2368/tcp -> 0.0.0.0:32769
```

Connect to http://IP_ADDRESS:PORT

TODO: add ghost welcome screen screenshot

### Configure blog and add some content

Admin console is at
 http://HOST:PORT/ghost

TODO: add instructions to setup ghost, create account and publish first post. provide some sample markdown content in the code/chap5 dir which they could copy and paste.

### Finding Everything about the running  container

TODO: add some description

#### Inspecting

``` docker inspect ghost ```

#### Checking the Stats

``` docker stats --no-stream=true ghost```

``` docker top```

### Examine Logs

``` docker logs ghost```
``` docker logs -f ghost ```

TODO: hit the URL a few times while tailing the log so that it gets updated.

Get Event Stream from the Docker Daemon

``` docker events ```

[Tip: keep one windows open with docker events command running. Open another windows and
do some operations such as run, stop rm to see event stream updated live]

Also keep the event stream on in one terminal and start executing rest of the commands in a new terminal.


### Attach to the container

``` docker attach ```

try ctrl=p ctrl=q to detach
learn how to pverride detach sequence with  --detach-keys
https://docs.docker.com/engine/reference/commandline/attach/


### Copying files between container and client host

``` touch srcfile ```  

``` docker cp srcfile ghost:/opt  ```

``` docker cp ghost:/usr/src/ghost . ```


### Rename a  container

 ``` docker rename ```

### Controlling Resources


#### Putting limits on Running Containers

``` docker update ```

```
docker inspect ghost | grep -i memory
           "Memory": 0,
           "KernelMemory": 0,
           "MemoryReservation": 0,
           "MemorySwap": 0,
           "MemorySwappiness": -1,

docker update -m 400M ghost
ghost

docker inspect ghost | grep -i memory
           "Memory": 419430400,
           "KernelMemory": 0,
           "MemoryReservation": 0,
           "MemorySwap": 0,
           "MemorySwappiness": -1,
```

#### Limiting Resources while launching new containers

What can be limited
  * CPU
  * Memory
  * Disk IO
  * Capabilities

Open two terminals, lets call them T1, and T2

In T1, start monitoring the stats   
``` docker stats  ```

From T2, launch two containers with different CPU shares. Default CPU shares are set to 1024. This is a relative weight.  

```
docker run -d --name st-01  schoolofdevops/stresstest stress --cpu 1

docker run -d --name st-02 -c 512  schoolofdevops/stresstest stress --cpu 1

```

Observe stats in T1

Launch a couple more nodes with different cpu shares, observe how T2 stats change

```
docker run -d --name st-03 -c 512  schoolofdevops/stresstest stress --cpu 1

docker run -d --name st-04  schoolofdevops/stresstest stress --cpu 1


```

Exercises
  * Put a memory limit
  * Set disk iops

### Launching Containers with Elevated  Privileges

``` docker run --privileged ```

Example: Running a sysdig container to monitor docker

```
docker run -itd --name=sysdig --privileged=true \
           --volume=/var/run/docker.sock:/host/var/run/docker.sock \
           --volume=/dev:/host/dev \
           --volume=/proc:/host/proc:ro \
           --volume=/boot:/host/boot:ro \
           --volume=/lib/modules:/host/lib/modules:ro \
           --volume=/usr:/host/usr:ro \
           sysdig/sysdig:0.11.0 sysdig
```

``` docker exec -it sysdig bash

csysdig
```

TODO: after launching csysdig, select F2, select Containers and monitor those.


##### References

[Resource Management in Docker by Marek Goldmann] (https://goldmann.pl/blog/2014/09/11/resource-management-in-docker/)
