#Dockerizing your Applications : Building Images and Working with Registries

In the previous session, we learnt about various container operations such as running containers from
pre built images, port mapping, inspecting and updating containers, limiting resources etc. In this
chapter, we are going to learn about how to build containers for your individual applications, as well
as how to work with docker hub registry to host and distribute the images.  

### Building Docker - A manual approach

Before we start building automated images, we are going to create a docker image by hand. We have already
used the pre built image from the registry in the last session. In this session, however, we are going to
create our own image with ghost installed. Since Ghost is a node.js based application, we will base our
work on existing offical image for **node**

##### Types of Images  

  * Slim  
  * Complete  

To search an image from the registry we could use,  

``` docker search node ```

You could find the same results when you search using the UI

TODO: Add a screenshot which shows searching for node image on docker hub

Lets launch a intermediate container using the image above. We will use this container to install and configure ghost and its dependencies.

``` docker run -it --name intermediate node:4-slim bash ```

``` docker ps  ```

``` docker exec -it intermediate bash ```

##### Install and Configure Ghost on a debian/ubuntu system

install pre-requisites

```
apt-get update && apt-get install -y gcc make python unzip vim

```
download and install ghost

```
mkdir /usr/src/ghost
cd /usr/src/ghost/
wget -c https://ghost.org/archives/ghost-0.10.1.zip
unzip ghost-0.10.1.zip
npm install --production

```

Create configuration for ghost

```
cd /usr/src/ghost; mv config.example.js config.js
```

Edit config.js

``` vim config.js ```


scroll to development block and change the server config to use 0.0.0.0 instead of 127.0.0.1
e.g.
```
            host: '0.0.0.0',
```

cleanup

```

apt-get purge -y --auto-remove gcc make python unzip vim
rm -rf /var/lib/apt/lists/*
rm ghost-0.10.1.zip
npm cache clean
rm -rf /tmp/npm*

```

Validate

To launch a container with the above images in a development mode, use


```
docker run -d -w /usr/src/ghost  -p 2368 schoolofdevops/ghost:0.1.0 npm start

```

Find out the port mapping, connect to http://host:port and validate your image.
