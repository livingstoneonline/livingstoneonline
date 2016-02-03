# Development Workflow


## Development Enviroment

Basically after setting you have
[Setup your Development Environment!](docs/development_enviroment.md), you
should have some code locally in your *sites* folder. Here you can manipulate
the code and perform commits, branches, pulls, and pushs, as is typical in a Git
repository; making changes as you see fit to the *dev* branch of your
repositories.

Everytime you do a push up to *dev* Docker Hub will start building a new image.
You do not need to wait for this, or reset your enviroment and download the new
image, as it essentally contains the exact same info you have locally.

Though it would be wise at least once a day to pull down the latest work others
have performed as well.

I would recommend performing a the following commands once a day, perhaps in the
evening so it will be ready for you when you wish to start in the morning.

```bash
$ docker-compose pull && docker-compose up
```

### Previewing Work with others.

You can leverage the
[Vagrant Share!](docs/development_enviroment.md#sharing-your-enviroment), to
share a URL to your development enviroment so that others can browse the site
and comment on it before pushing it to stage.

## Stage Enviroment

Once your ready to push your new feature or improvement to stage you simply push
the relevant topic branch (containing your feature or improvement), into the
*stage* branch of the repository. That will trigger the Docker Hub to build
the images. 

Once the images are build, the stage server will be notified, and it will pull
down the latest images and restart the appropriate services.

After some time we can check in on stage and *test* to make sure everything is
working correctly and the recent changes have not broken anything.

## Prod Enviroment

Is pretty much exactly the same process as updating *stage*, except you should
wait for approval of your changes (by Adrian & Megan) in *stage* before updating
the *prod* branch. 
