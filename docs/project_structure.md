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
3. Mariadb aka MySQL

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

We provide those three major components via three Drupal Containers (by the
same names).

These three Drupal containers are composed of many Docker images, splitting them
out like this ensures faster build times and makes automated deployment easier.

Here is a list of each Container and all the images that comprise it, ordered
start to finish.

### Mariadb Images

1. Docker Hub:[mariadb](https://hub.docker.com/r/livingstoneonline/mariadb) 
   Github: [docker-mariadb](https://github.com/livingstoneonline/docker-mariadb)

### Drupal Images

1. Docker Hub:[drupal](https://hub.docker.com/r/livingstoneonline/drupal) 
   Github: [docker-drupal](https://github.com/livingstoneonline/docker-drupal)
2. Docker Hub:[islandora](https://hub.docker.com/r/livingstoneonline/islandora) 
   Github: [docker-islandora](https://github.com/livingstoneonline/docker-islandora)
3. Docker Hub:[livingstone](https://hub.docker.com/r/livingstoneonline/livingstone) 
   Github: [docker-livingstone](https://github.com/livingstoneonline/docker-livingstone)

### Tomcat Images

1. Docker Hub:[java](https://hub.docker.com/r/livingstoneonline/java) 
   Github: [docker-java](https://github.com/livingstoneonline/docker-java)
2. Docker Hub:[tomcat](https://hub.docker.com/r/livingstoneonline/tomcat) 
   Github: [docker-tomcat](https://github.com/livingstoneonline/docker-tomcat)
3. Docker Hub:[djatoka](https://hub.docker.com/r/livingstoneonline/djatoka) 
   Github: [docker-djatoka](https://github.com/livingstoneonline/docker-djatoka)
4. Docker Hub:[fedora](https://hub.docker.com/r/livingstoneonline/fedora) 
   Github: [docker-fedora](https://github.com/livingstoneonline/docker-fedora)
5. Docker Hub:[gsearch](https://hub.docker.com/r/livingstoneonline/docker) 
   Github: [docker-gsearch](https://github.com/livingstoneonline/docker-gsearch)

#### Additional Test Image

We also have an additional test image that contains a few thousand objects in
the Fedora Repository for testing purposes.

6. Docker Hub:[fedora-sample-data](https://hub.docker.com/r/livingstoneonline/docker) 
   Github: [docker-fedora-sample-data](https://github.com/livingstoneonline/docker-fedora-sample-data)


## Stability

After the initial setup the vast majority of this images are unlikely to change,
as most development will be focused on the Drupal front end and how it interacts
with the various components.

As such typically only the *livingstoneonline/livingstone* image is expected to change on a regular basis.

It takes about 30 minutes for Docker Hub to build the image, although it can be much quicker.
