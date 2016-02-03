# Livingstone Online

## Introduction 

This git repository is focused on documenting all the technical aspects relating
to work-flow and deployment of the Livingstone Online project, as well as
providing a local development environment based on Docker.

The work-flow for Livingstone Online is comprised of three environments:
_development_, _stage_, and _production_.

The _development_ environment has no fixed location, it's provided by this
repository along with a number of Docker Images that comprise all its
components.

Both the _stage_ and _production_ environments are hosted at
[University of Maryland](http://www.umd.edu/). 

* [Stage](livingstonestage.lib.umd.edu)
* [Production](livingstone.lib.umd.edu)

As it currently stands, both of these boxes run *RHEL 7* and the software is
deployed via Docker.

## Table of Contents

* [Setup Development Environment!](docs/development_enviroment.md)
* [Project Structure!](docs/project_structure.md)
* [Automated Build System!](docs/automated_build_system.md)
* [Altering the Environment!](docs/altering_enviroment.md)
* [Development Work-flow!](docs/development_workflow.md)
