# Project Structure

## Table of Contents

* [Overview](#overview)
  * [Drupal](#drupal)
  * [Tomcat](#tomcat)
  * [MySQL](#mysql)
* [Docker](#docker)
  * [MySQL Images](#mysql-images)
  * [Drupal Images](#drupal-images)
  * [Tomcat Images](#tomcat-images)
    * [Additional Test Image](#additional-test-image)
* [Stability](#stability)

## Overview

Livingstone Online is composed of three major components which in turn are
comprised of many smaller tools.

1. Drupal
2. Tomcat
3. MySQL

### Drupal

Drupal represents the most visible layer, it is the glue that all other
components are stuck to.

* Apache: Web-server, takes request and serves responses
* Islandora: Bridge between Drupal and Fedora
$ Theme and Drupal Content.

### Tomcat

Tomcat is a Java servlet server, it hosts Fedora, Adore-Djatoka, Solr and Saxon.

* Fedora: Data Store for the Livingstone Online Repository
* Adore-Djatoka: jp2000 Image Server (Used in the Manuscript Viewer)
* Solr: Indexed Search, it populates the "Browse By" Pages
* Saxon: Provides XSLT transformations for TEI -> HTML (Used in the Manuscript Viewer)

### MySQL

MySQL is leveraged by both Drupal and Fedora to store persistent information. 

## Docker

We provide those three major components via a single Docker Container. 

This container is composed of many Docker images. Splitting them out like this
ensures faster build times and makes automated deployment easier.

Here is a list of each Docker image, ordered start to finish.

1. Docker Hub:[base](https://hub.docker.com/r/livingstoneonline/base) 
   Github: [docker-base](https://github.com/livingstoneonline/docker-base)
2. Docker Hub:[MySQL](https://hub.docker.com/r/livingstoneonline/mysql) 
   Github: [docker-mysql](https://github.com/livingstoneonline/docker-mysql)
3. Docker Hub:[tomcat](https://hub.docker.com/r/livingstoneonline/tomcat) 
   Github: [docker-tomcat](https://github.com/livingstoneonline/docker-tomcat)
4. Docker Hub:[drupal](https://hub.docker.com/r/livingstoneonline/drupal) 
   Github: [docker-drupal](https://github.com/livingstoneonline/docker-drupal)
5. Docker Hub:[livingstone](https://hub.docker.com/r/livingstoneonline/livingstone) 
   Github: [docker-livingstone](https://github.com/livingstoneonline/docker-livingstone)
   
In addition to the main application there are two more Docker containers which
are used to manage deployment.

* Docker Hub:[ftp](https://hub.docker.com/r/livingstoneonline/ftp) 
  Github: [docker-ftp](https://github.com/livingstoneonline/docker-ftp)
* Docker Hub:[auto-deploy](https://hub.docker.com/r/livingstoneonline/auto-deploy) 
  Github: [docker-auto-deploy](https://github.com/livingstoneonline/docker-auto-deploy)
 
FTP is used to run an FTP server on the production server which allows us to
host large files for use in deployment.

Auto-deploy is used to listen for updates made in Docker Hub; when a Docker
Image is updated it will pull down the latest version of it and restart the
server with the most recent version of the application.


## Stability

After the initial setup the vast majority of this images are unlikely to change,
as most development will be focused on the Drupal front end and how it interacts
with the various components.

As such typically only the *livingstoneonline/livingstone* image is expected to change on a regular basis.

It takes about 30 minutes for Docker Hub to build the image, although it can be much quicker.
