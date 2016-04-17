# Development Workflow

## Development Environment

Basically after setting you have
[Setup your Development Environment!](installation.md), you should have some
code locally in your *./code* folder. Here you can manipulate the code and perform
commits, branches, pulls, and pushes, as is typical in a Git repository; making
changes as you see fit to the *dev* branch of your repositories.

Though it would be wise at least once a day to pull down the latest work others
have performed as well.

I would recommend performing a the following commands once a day, perhaps in the
evening so it will be ready for you when you wish to start in the morning.

```bash
./commands/pull
./commands/cleanup
```

## Sharing your work with others.

You can leverage the [Vagrant Share](https://www.vagrantup.com/docs/share/), to
share a URL to your development environment so that others can browse the site
and comment on it before pushing it to stage.

You'll first have to setup and account with
[HashiCorp's Atlas](https://atlas.hashicorp.com/) (don't worry it's free).

Follow the instructions here to login:

[Login](https://atlas.hashicorp.com/help/vagrant/shares/create)

After logging in, for convenience you can use the share command to share your
development environment:

```bash
./commands/share
``` 

If successful it will printout a URL where anyone can access your development
environment:

> ==> default: Your Vagrant Share is running! Name: soaring-porpoise-9145
> ==> default: URL: http://soaring-porpoise-9145.vagrantshare.com

## Dev Environment

Every time you do a push up to *dev* on any of the relevant repositories.

* [livingstone_online_theme](https://github.com/livingstoneonline/livingstone_online_theme)
* [livingstone_online_features](https://github.com/livingstoneonline/livingstone_online_features)

Docker Hub will start building a new image. You do not need to wait for this, or
reset your environment and download the new image, as it essentially contains
the exact same info you have locally.

If you want to build your development environment locally rather than waiting
for the server to build a fresh version. You can run:

```bash
docker-compose -f docker-compose.dev.yml build
```

Generally this is only needed if you added a new Contrib module, or made some
other change to the **./build** folder.

## Stage Environment

Once your ready to push your new feature or improvement to stage you simply push
the relevant topic branch (containing your feature or improvement), into the
*stage* branch of the relevant repository.

* [livingstone_online_theme](https://github.com/livingstoneonline/livingstone_online_theme)
* [livingstone_online_features](https://github.com/livingstoneonline/livingstone_online_features)

Also double check that any relevant changes you made to the **./build/dev**
directory (added Contrib modules for example), is also added to the
**./build/stage** Drupal make files as well.

This will trigger the Docker Hub to build the images. Once the images are build,
the stage server will be notified, and it will pull down the latest images and
restart the appropriate services.

After some time we can check in on stage and test to make sure everything is
working correctly and the recent changes have not broken anything.

## Prod Environment

Is pretty much exactly the same process as updating *stage*, except you should
wait for approval of your changes (by Adrian & Megan) in *stage* before updating
the *prod* branch. 
