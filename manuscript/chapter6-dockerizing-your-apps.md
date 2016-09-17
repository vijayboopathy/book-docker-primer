#Dockerizing your Applications : Building Images and Working with Registries

In the previous session, we learnt about various container operations such as running containers from
pre built images, port mapping, inspecting and updating containers, limiting resources etc. In this
chapter, we are going to learn about how to build containers for your individual applications, as well
as how to work with docker hub registry to host and distribute the images.  


### Registering with the Registry : Creating an Account on DockerHub
Since we are going to start working with the registry, build and push images to it later, its essential to have our own account on the registry. For the purpose of this tutorial, we are going to use the hosted registry i.e.  Dockerhub.  

Steps to create Dockerhub account

TODO: Add steps to create dockerhub account with screenshots


### Building Docker Images - A manual approach

Before we start building automated images, we are going to create a docker image by hand. We have already
used the pre built image from the registry in the last session. In this session, however, we are going to
create our own image with ghost installed. Since Ghost is a node.js based application, we will base our
work on existing offical image for **node**

##### Types of Images  

  * Slim  
  * Complete  

To search an image from the registry we could use,  

```
docker search node
```

You could find the same results when you search using the UI

TODO: Add a screenshot which shows searching for node image on docker hub

Lets launch a intermediate container using the image above. We will use this container to install and configure ghost and its dependencies.

```
docker run -it --name intermediate node:4-slim bash
```

```
docker ps  
```

```
docker exec -it intermediate bash
```

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

```
vim config.js
```


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

Exit from the container.


Note down the container id for the container you just modified and exited from.

```
docker ps -l

```
To create a image by taking a snasnapshot of the container use the following command,

```
docker commit -a "Firstname Lastname" -m "commit message" CONTAINER HUB_USERNAME/REPO:TAG  

e.g. docker commit -a "John Doe" -m "creating custom ghost image" c082972f66d6 mydockerhubid/ghost:0.1.0
```
Validate

To launch a container with the above images in a development mode, use


```
docker run -d -w /usr/src/ghost  -p 2368 mydockerhubid/ghost:0.1.0 npm start

```

Find out the port mapping, connect to http://host:port and validate your image.


### Dockerfiles - Automating Image Builds

Earlier, we created image by launching a intermediate container and manually installing and configuring ghost app. This time we are going to use a Dockerfile,  write the
specification to build image, and use it to automate the proces of building image.


#### Setting up a ghostapp repo on github.

We are going to setup a git repository where we create the configurations to automate the build process of our image. Later in this chatper, we will also integrate it with dockerhub to create automated builds. For this purpose its essential to have a github account.

  * Create and Account on gihub if you do not already have it
  * For the ghostapp repo  https://github.com/schoolofdevops/ghostapp
  * Clone the forked repo

```

git clone https://github.com/YOUR_GITHUB_ID/ghostapp.git
cd ghostapp

```

Examine  Dockerfile in ghostapp directory.

#### Building and Image with Dockerfile

```
docker build -t USERNAME/REPO:TAG  .   

e.g.  docker build -t mydockerhubid/ghost:0.2.0 .
```

TODO: add output of build


Verify the image is been created
```
docker images

```


Validate the image is working by launching it

```
docker run --name ghost2 -P  -itd mydockerhubid/ghost:0.3.1

docker ps
docker port ghost2

```

verify  http://HOST:PORT shows up ghost page.


### Dockerfile Primer


| INSTRUCTION     | DESCRIPTION    |
| :------------- | :------------- |
| FROM       | TODO      |
| MAINTAINER       | TODO      |
| RUN       | TODO      |
| LABEL       | TODO      |
| ENV       | TODO      |
| COPY       | TODO      |
| ADD       | TODO      |
| VOLUME       | TODO      |
| USER       | TODO      |
| CMD       | TODO      |
| ENTRYPOINT       | TODO      |
| ONBUILD       | TODO      |
| STOPSIGNAL       | TODO      |
| HEALTHCHECK       | TODO      |
| SHELL       | TODO      |
| WORKDIR       | TODO      |
| ARG | TODO |


### Inefficient RUN Instructions

As used in the reference Dockerfile you built ghost image, its useful to combine multiple commands into a single RUN instruction. This is because each of the instructions are going to create a layer.

Lets see what happens if you have inefficient RUN instructions.

In the app directory that you downloaded earlier, examine Dockerfile.inef, and see if you could spot the difference between this and previous Dockerfile that you used.

Now, lets attempt building an image with Dockerfile.inef.

```
docker build -t mydockerhubid/ghost:inef -f Dockerfile.inef .
```

Now examine the difference between the images created with two different Dockerfiles

docker images | grep ghost

### Tagging Images

```
docker tag IMAGE HUB_USERNAME/REPO:TAG

```

e.g.

```
docker tag 20ebdc62d89b mydockerhubid/ghost:latest

```

Exercise: Find out the id of 0.2.0 image you build with dockerfile and tag it as latest.


### Pushing Images to Registry

```
docker login

docker push mydockerhubid/ghost:0.2.0
docker push mydockerhubid/ghost:latest

```

Validate on Dockerhub
TODO: Add instructions and screenshots.

### Create Automated Builds

After having published our   images to Dockerhub, we are also going to setup a process to create automated builds.

TODO: add instructions with screenshot to create automated builds by integrating dockerhub with github. Refer to https://docs.docker.com/docker-hub/builds
