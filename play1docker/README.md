## Play1 Dockerfile


This repository contains a **Dockerfile** with requirements for [Play1](https://www.playframework.com/documentation/1.4.x/home) in an ubuntu image.
It contains not play. You should provide your own play through the host on `/data/play`.


### Base Docker Image

* [ubuntu:14.04](https://hub.docker.com/_/ubuntu/)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Build the image from Dockerfile: `docker build -t="MY_BASE_NAME/MY_NAME[:MY_TAG]" https://raw.githubusercontent.com/synapplix/dockerfiles/master/play1docker/Dockerfile`

#### Example image build

    docker build -t="play1docker" https://raw.githubusercontent.com/synapplix/dockerfiles/master/play1docker/Dockerfile

### Usage

    docker run -it --rm MY_BASE_NAME/MY_NAME

#### Run `RICA`

For a RICA System it is common to have a directory layout like:

    .
    +-- play
    +-- play-modules
    +-- rica
    
Create a rica volume container and copy the play, application dependend modules and application into it

    docker create --volume /data --name rica play1docker /bin/true
    docker cp $HOME/git/play rica:/data
    docker cp $HOME/git/play-modules rica:/data
    docker cp $HOME/git/rica rica:/data
    
Execute some Play!1 maintanance scripts  on the volume container

    docker run -it --rm --volumes-from rica play1docker clean rica
    docker run -it --rm --volumes-from rica play1docker deps rica
        optional:
    docker run -it --rm --volumes-from rica play1docker precompile rica

Run/Start the application

    docker run -it --rm --volumes-from rica play1docker run rica
        optional:
    docker run -it --rm --volumes-from rica play1docker run rica -Dprecompiled=true
        or as daemon:
    docker run --detach=true --volumes-from rica play1docker start rica

### Link with database

Please see the 'yabe-with-db' example in directory 'samples'.