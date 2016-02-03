# Altering the Environment

Aside from making changes to code directly in their respective repositories, you
may at some point wish to add additional dependencies to the project.

For the most part these dependencies will be related to Drupal, and in
particular the
[docker-livingstone](https://github.com/livingstoneonline/docker-livingstone)
image.

All the Drupal dependencies are defined in Drush Make files in the
[build folder](https://github.com/livingstoneonline/docker-livingstone/tree/dev/build).

They are separated out into a few categories.

* site.make - Includes the files below.
* contrib.make - Contrib Modules.
* dev.make - Only deployed in the development environment.
* features.make - Features.
* islandora.make - Islandora dependencies.
* theme.make - Theme dependencies.

Simply add your required modules / theme libraries in their respective file.

You can find more detailed information on Drush Make [here](http://www.drush.org/en/master/make/).
