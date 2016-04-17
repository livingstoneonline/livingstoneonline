# Automated Build System

## Introduction

There are a two main tools at play for our automated build system.

1. [Github](https://github.com/livingstoneonline)
2. [Docker Hub](https://hub.docker.com/r/livingstoneonline/)

Github houses the code for running everything on the site (themes, module code,
etc) as well as what's needed to generate our Docker Images (Dockerfiles).

Docker Hub generates the Docker Images from the code in Github and houses them
as well. After they are generated we can then download and use them or deploy
them to either stage or production.

## Triggering Builds from Docker Github Repositories 

Each of the Github repositories that correspond to Docker images (listed below),
are set to trigger a build in Docker Hub the second any change is made to them:

| Name        | Description                         | GitHub                                                  | Docker Hub                                             |
|-------------|-------------------------------------|---------------------------------------------------------|--------------------------------------------------------|
| Base        | Essentials                          | https://github.com/livingstoneonline/docker-base        | https://hub.docker.com/r/livingstoneonline/base        |
| MySQL       | Database for Drupal / Fedora        | https://github.com/livingstoneonline/docker-base        | https://hub.docker.com/r/livingstoneonline/base        |
| Tomcat      | Server for Fedora, etc              | https://github.com/livingstoneonline/docker-tomcat      | https://hub.docker.com/r/livingstoneonline/tomcat      |
| Drupal      | Web Server                          | https://github.com/livingstoneonline/docker-drupal      | https://hub.docker.com/r/livingstoneonline/drupal      |
| Livingstone | Livingstone Customization's         | https://github.com/livingstoneonline/docker-livingstone | https://hub.docker.com/r/livingstoneonline/livingstone |
| FTP         | Hosts Deployment files              | https://github.com/livingstoneonline/docker-ftp         | https://hub.docker.com/r/livingstoneonline/ftp         |
| Auto-Deploy | Auto deploy updates to stage & prod | https://github.com/livingstoneonline/docker-auto-deploy | https://hub.docker.com/r/livingstoneonline/auto-deploy |

Since we have such a large number of nested Docker Images, we also propagate the
trigger to all dependent images in the order of their dependencies so they are
updated as well. So if **livingstoneonline/mysql** is changed, it will then cause
**livingstoneonline/tomcat** to be rebuild which in turn will trigger
**livingstone/drupal** to be built, and so on.

## Triggering builds from changes to Source Code

In addition we also monitor a few other Github repositories and trigger builds
if they are changed. In Particular:

1. [livingstone_online_theme](https://github.com/livingstoneonline/livingstone_online_theme)
2. [livingstone_online_features](https://github.com/livingstoneonline/livingstone_online_features)

So if one where to add a new CSS file to the theme, Docker Hub will start to
build out a new **livingstoneonline/livingstone** Docker image.

## Stage & Production

For the most part all the Docker Images have only one version, which is shared
across all environments, so we can safely ignore them.

The exception being
[docker-livingstone](https://github.com/livingstoneonline/docker-livingstone),
which only has one branch, but a different **Dockerfile** for each environment.
This allows us to run different code locally, and to test out features and
components on stage before deploying them to production.

For each corresponding branch, a different Docker Image is build.

1. docker-livingstone:dev
2. docker-livingstone:stage
3. docker-livingstone:prod
4. docker-livingstone:latest (_Same as dev, but includes sample data_)

Each of these different images are destined for our different environments.
