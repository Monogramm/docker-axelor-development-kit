[![Build Status](https://travis-ci.org/Monogramm/docker-axelor-development-kit.svg)](https://travis-ci.org/Monogramm/docker-axelor-development-kit)
[![Docker Automated buid](https://img.shields.io/docker/build/monogramm/docker-axelor-development-kit.svg)](https://hub.docker.com/r/monogramm/docker-axelor-development-kit/)
[![Docker Pulls](https://img.shields.io/docker/pulls/monogramm/docker-axelor-development-kit.svg)](https://hub.docker.com/r/monogramm/docker-axelor-development-kit/)

**This container is still in development and shouldn't be considered production ready!**

# Axelor Development Kit on Docker

Docker image for Axelor Development Kit.

Provides full database configuration, production mode, HTTPS enforcer (SSL must be provided by reverse proxy), handles upgrades, and so on...

## What is Axelor Development Kit  ?

Axelor Development Kit (ADK) is an open source Java framework to create modern business applications.

> [More informations](https://github.com/axelor/axelor-development-kit)

## Supported tags

https://hub.docker.com/r/monogramm/docker-axelor-development-kit/

* `5.0.11` `5.0` `5` `latest`
* `4.1.8` `4.1` `4`

## How to use this image ?

This image is based on the [official Gradle repository](https://hub.docker.com/_/gradle/).

This image is designed to be used as a base container for building Axelor applications.

# Building an Axelor application
You can build your own Dockerfile on top of this one and build your application inside the docker.

```yaml
FROM monogramm/docker-axelor-development-kit

# Lost from previous image but mandatory for ADK
ENV AXELOR_HOME /opt/adk

COPY ./app .
RUN axelor build

```

Alternatively, you can run this from the directory of the Axelor application you want to build.
**Not tested yet!**

```console
$ docker run --rm -v "$PWD":/home/gradle/project -w /home/gradle/project monogramm/docker-axelor-development-kit axelor <axelor-task>
```

# Adding Features
If the image does not include the packages you need, you can easily build your own image on top of it.
Start your derived image with the `FROM` statement and add whatever you like.

```yaml
FROM monogramm/docker-axelor-development-kit

RUN ...

```

You can also clone this repository and use the [update.sh](update.sh) shell script to generate a new Dockerfile based on your own needs.

For instance, you could build a container based on Axelor master branch by setting the `update.sh` versions like this:
```bash
latests=( "master" )
```
Then simply call [update.sh](update.sh) script.

```console
bash update.sh
```
Your Dockerfile(s) will be generated in the `images/master` folder.

**Updating** your own derived image is also very simple. When a new version of the Axelor image is available run:

```console
docker build -t your-name --pull . 
docker run -d your-name
```

or for docker-compose:
```console
docker-compose build --pull
docker-compose up -d
```

The `--pull` option tells docker to look for new versions of the base image. Then the build instructions inside your `Dockerfile` are run on top of the new image.

# Questions / Issues
If you got any questions or problems using the image, please visit our [Github Repository](https://github.com/Monogramm/docker-axelor-development-kit) and write an issue.  
