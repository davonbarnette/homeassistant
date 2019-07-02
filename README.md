#HomeAssistant Automation

This repo is a for-the-bois repository to help you all leverage docker and docker-compose to create a home automation server.
For the most part, this is just a device registry, but we'll be adding more things as we go along. Please read all of this before continuing or trying on your own.

###What is Docker?
Docker is a platform that allows you to create Docker containers. You can think of a **Docker container** as a mini-computer that is isolated from all the noise and restrictions on the host OS.
That probably sounds like complicated bullshit, but let's take a look at a practical example.

Let's say you need to build an application that uses `npm v6` and runs on your home computer (host OS), so you install it and easily create the app. No problem.
But then, you need to create another application that runs on the same computer (host OS), however, now you need `npm v10`.
Unfortunately, when you install `npm v10`, your other application no longer works because it required `npm v6`.

This is where Docker brings value. It creates a separate "mini-computer" that runs on top of your host OS, but with its own isolated configuration.
So now, you can wrap Application 1 in a Docker container that has `npm v6`, and then wrap Application 2 in a different Docker container that has
`npm v10`, and both applications can run in tandem.

But Docker's value doesn't stop there. Docker containers are actually built from a set of *instructions* called a **Docker image**.
In our example above, under normal circumstances, you'd need to get into that first container or "mini-computer" and install `npm v6`, and the same for the other container.
However, using Docker images, we can essentially build blueprints of how we want our Docker container to look when it starts.

So we can create our *Docker image* `npm-container-v6` to automatically install `npm v6` on container creation. Then run something like `docker run npm-container-v6`, and we
have a mini-computer with `npm v6` installed!

### Why is this useful for Home Assistant?

For our Home Assistant build, we're going to use what's called **docker-compose**. If Docker spawns mini-computers, then you can think
of docker-compose as a "computer warehouse" of sorts. docker-compose allows us to spawn multiple containers at the same time, with their
own internal network. So, instead of executing `docker run` 6 times in a row in our command line, we can just add our Docker images to our
docker-compose file, and it will automatically spawn all of our mini-computers with one line (`docker-compose up`).

This allows us to spawn multiple home automation services like Hue, August Smart Lock, Home Security Cameras, and much more, each wrapped
in their own Docker container, and all with one line -- `docker-compose up`.

## Setup the project
You'll notice that we have a `docker-compose.yaml` in our upper-most directory level. This `.yaml` file is our docker-compose
instructions, and let's us control which applications we want to run when we say `docker-compose up`. Right now, all it's doing is
running Home Assistant, but once we get more applications in here, we can start running more.

## Actually, right now there really is no setup.
All you have to do is:
1. Open up your terminal (this is assuming MacOS or Linux distribution). If you're using Windows, this will look at a *little* different, but I'm
too lazy to actually write up the documentation to do so.
2. `cd` into the directory containing the `docker-compose.yaml`. For me, I have to do `cd $HOME/Users/davonbarnette/Documents/Development/homeassistant`.
3. Run this one line `docker-compose up`.
4. Navigate to `localhost:8123` in the browser of your choice
5. Setup your account.
6. If you want to hook up your Hue lights, open the file: `config/configuration.yaml` and change the Hue bridge internal IP address.
Afterwards, you should be able to just see your lights when you log into your account on HomeAssistant.
 
## What now?
At this point, there are a lot of tutorials that will help you configure separate home automation things. Navigate to
https://www.home-assistant.io/components/ to figure out if any of the home automation devices you're using are compatible with
Home Assistant. If they are, just go ahead and try and throw them in the `configuration.yaml`.
