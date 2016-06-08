## Play1 Dockerfile for testing


This repository contains a **Dockerfile** with requirements for [Play1](https://www.playframework.com/documentation/1.4.x/home) in an ubuntu image.
It adds groovy support for testing and test setup scripts.
It contains not play. You should provide your own play through the host on `/data/play`.


### Base Docker Image

* [ubuntu:14.04](https://hub.docker.com/_/ubuntu/)


### Installation

1. Install [Docker](https://www.docker.com/).

2. Build the image from Dockerfile: `docker build -t="MY_BASE_NAME/MY_NAME[:MY_TAG]" https://raw.githubusercontent.com/synapplix/dockerfiles/master/play1testing/Dockerfile`

#### Example image build

    docker build -t="play1testing" https://raw.githubusercontent.com/synapplix/dockerfiles/master/play1testing/Dockerfile

### Usage

    docker run -it --rm MY_BASE_NAME/MY_NAME
