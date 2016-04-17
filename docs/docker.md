# Docker Guide

Here is a quick guide that can get you started but it's recommended you read the
full Docker documentation

## Starting Docker

The can start docker either by opening *Kitematic* or with ```docker-machine```
from the command line.

```bash
docker-machine start default
```

## Stopping Docker

By default if you close *Kitematic* it will turn off Docker, though this can be
disabled in the applications preferences.

If you want to turn off docker from the command line you can use ```docker-machine```:

```bash
docker-machine stop default
```

## Interacting with Docker

After starting docker you can now export the docker environment into your shell:

```bash
eval $(docker-machine env default)
```

This is required so that ```docker``` and ```docker-compose``` know which
machine to communicate with. 

You can add this line at the bottom of your shell start-up script _~/.bashrc_ or
_~/.zshrc_, etc, so you don't need to type it ever again.

**N.B.** If you ever start a new terminal / shell you'll have to enter that again.


## Configuring Livingstone Docker Container

By default when you run the ```./commands/setup``` script in this repository, it
will generate a default *docker-compose.yml* file for you based on the
development environment as well *docker.env* file.

You can modify these files and make changes as you see fit.

| Environment Variable            | Description                          |
|---------------------------------|--------------------------------------|
| MYSQL_ROOT_USER                 | Root user for MySQL.                 |
| MYSQL_ROOT_PASSWORD             | MySQL root user password.            |
| DRUPAL_SITE_NAME                | Name of the Drupal Site.             |
| DRUPAL_SITE_EMAIL               | Site administrator email.            |
| DRUPAL_SITE_LOCALE              | Site locale typically en-us.         |
| DRUPAL_SITE_ACCOUNT_NAME        | Site administrator account name.     |
| DRUPAL_SITE_ACCOUNT_PASSWORD    | Site administrator password.         |
| DRUPAL_SITE_ACCOUNT_EMAIL       | Site administrator email.            |
| DRUPAL_SITE_DB_NAME             | Database name 'livingstone'          |
| DRUPAL_SITE_DB_USER             | Drupal database user.                |
| DRUPAL_SITE_DB_PASSWORD         | Drupal database user password.       |
| DRUPAL_SITE_DB_REPLACE_EXISTING | Replace existing database (yes|no)   |
| DRUPAL_SITE_DB_IMPORT           | Import database from assets (yes|no) |
| TOMCAT_ADMIN_USER               | Tomcat user.                         |
| TOMCAT_ADMIN_PASSWORD           | Tomcat user password.                |
| FEDORA_ADMIN_USER               | Fedora user.                         |
| FEDORA_ADMIN_PASSWORD           | Fedora user password.                |
| FEDORA_INTERNAL_PASSWORD        | Fedora internal password.            |
| FEDORA_IMPORT_DATA              | Import data from assets (yes|no)     |
| FEDORA_REBUILD                  | Rebuild Fedora data from disk        |

## Starting Livingstone Docker Container

Now that we can communicate with Docker, we can run Docker Compose to download
the Docker Containers and run them in our VM (remember to first follow the
directions in [Interacting with Docker](#interacting-with-docker)):

```bash
docker-compose up -d
```

This can take a *very long time* depending on your internet speed. As it will be
downloading roughly 2.5 GB of data. Though once this is setup subsequent updates
are speedy.

Once the box is downloaded and setup you can access the site using the command:

```bash
./commands/open-in-browser
```

Otherwise you can access and monitor the application via *Kitematic*. Please
refer to the *Kitematic* documentation for more information:

https://docs.docker.com/kitematic/userguide/

## Stopping the Livingstone Docker Container 

The following command will stop and remove the Livingstone Docker Container:

```bash
docker-compose stop
```

This won't remove any bound volumes and will allow you to restart the container
without loosing your local data (_database changes etc_).

## Removing the Livingstone Docker Container

The following command will stop and remove the Livingstone Docker Container:

```bash
docker-compose -rmi all -v down
```

**N.B.** This will remove any local changes you made to your database so be
careful!

## Updating the Livingstone Docker Container

To pull down the latest Docker images, run this command:

```bash
docker-compose pull
```

This doesn't automatically deploy the new images, just downloads them.

If you want to run the latest images you must restart the containers:

```bash
docker-compose up -d
```

## Reference

* [Vagrant Docs](https://www.vagrantup.com/docs/)
* [Docker Docs](https://docs.docker.com/)
* [Docker Compose](https://docs.docker.com/compose/)
