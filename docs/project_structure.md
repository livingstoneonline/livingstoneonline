# Project Structure

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
* Drupal: Theme and Drupal Content.
* Islandora: Bridge between Drupal and Fedora

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

| Name        | Description                         | GitHub                                                  | Docker Hub                                             |
|-------------|-------------------------------------|---------------------------------------------------------|--------------------------------------------------------|
| Base        | Essentials                          | https://github.com/livingstoneonline/docker-base        | https://hub.docker.com/r/livingstoneonline/base        |
| MySQL       | Database for Drupal / Fedora        | https://github.com/livingstoneonline/docker-base        | https://hub.docker.com/r/livingstoneonline/base        |
| Tomcat      | Server for Fedora, etc              | https://github.com/livingstoneonline/docker-tomcat      | https://hub.docker.com/r/livingstoneonline/tomcat      |
| Drupal      | Web Server                          | https://github.com/livingstoneonline/docker-drupal      | https://hub.docker.com/r/livingstoneonline/drupal      |
| Livingstone | Livingstone Customization's         | https://github.com/livingstoneonline/docker-livingstone | https://hub.docker.com/r/livingstoneonline/livingstone |
| FTP         | Hosts Deployment files              | https://github.com/livingstoneonline/docker-ftp         | https://hub.docker.com/r/livingstoneonline/ftp         |
| Auto-Deploy | Auto deploy updates to stage & prod | https://github.com/livingstoneonline/docker-auto-deploy | https://hub.docker.com/r/livingstoneonline/auto-deploy |

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
