# Livingstone Online

## Introduction 

This git repository is focused on documenting all the technical aspects relating
to work-flow and deployment of the Livingstone Online project, as well as
providing a local development environment based on Docker.

The work-flow for Livingstone Online is comprised of three environments:
_development_, _stage_, and _production_.

The _production_ environment is currently hosted on a commercial server provided by 
[So You Start](https://www.soyoustart.com/us/). 

As it currently stands, both of these boxes run *RHEL 7* and the software is
deployed via Docker.

## For Non-Developers

Download and install the latest version of
[Docker Toolbox](https://docs.docker.com/mac/step_one).

Then download the
[Livingstone Online App](https://github.com/livingstoneonline/livingstoneonline/releases/download/1.0/Livingstone.Online.zip).

Just unzip and open the application to get started! 

## For Developers

Please read though our in-depth documentation:

* [Setup Development Environment](docs/installation.md)
* [Project Structure](docs/project_structure.md)
* [Automated Build System](docs/automated_build_system.md)
* [Docker Quick Guide](docs/docker.md)
* [Development Work-flow](docs/development_workflow.md)
* [Altering the Environment](docs/altering_environment.md)

## Commands

For convenience a number of commands are provided in the [commands](/commands) directory.

| Command                   | Notes                                                                         |
|---------------------------|-------------------------------------------------------------------------------|
| bash                      | Attaches a bash shell to the container.                                       |
| build                     | Builds all the [images](/images).                                             |
| cache-clear               | Fixes sync issues with docker and vagrant shared folders. (boot2docker only). |
| cleanup                   | Tries to free as much space as possible.                                      |
| download-assets           | Downloads required assets.                                                    |
| drush                     | Runs drush in the container with the given arguments.                         |
| exec                      | Runs the given command in the container.                                      |
| generate-env-files        | Generates the required environment files to run ```docker-compose```.         |
| mysql                     | Runs mysql client in the container.                                           |
| open-in-browser           | Opens the webpage in your default browser.                                    |
| pull                      | Pulls down the latest version of all images.                                  |
| remove-inactive-volumes   | Deletes volumes not associated with running or stopped container.             |
| remove-stopped-containers | Removes stopped containers.                                                   |
| remove-untagged-images    | Removes un-tagged images.                                                     |
| setup                     | Setups up the repository for development.                                     |
| share                     | Start Vagrant Share, sharing your development environment over the internet.  |
| zsh                       | Attaches a zsh shell to the container.                                        |
