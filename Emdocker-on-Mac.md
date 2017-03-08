# Running Emdocker on Mac

## Setup

The following instructions were tested with Docker v. 1.13.1 and VirtualBox v. 5.1.14.

1. Clone [Embox](https://github.com/embox/embox) locally.

2. Install [Docker.app](https://docs.docker.com/engine/getstarted/step_one/#docker-for-mac) following the instructions.
   * Note that Docker Toolbox should **not** be installed, as it conflicts with Docker for Mac. If you have it installed, [uninstall it cleanly](https://forums.docker.com/t/solved-how-to-cleanly-uninstall-docker-toolbox/13411)).


3. Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads).

4. Launch Docker.app.

5. Unless you already have set up a default Docker machine, run:

        docker-machine create --driver virtualbox default

6. Run

        docker-machine start default

   It will pull the Emdocker image.

7. You might want to add this to your `.bash_profile`:

        alias dr="[PATH_TO_embox]/scripts/docker/docker_run.sh"

   This is a convenience alias for running commands in Docker.

## Run

### Start Emdocker

* Make sure that you Docker machine is up and running:

        docker-machine ls
        docker-machine start default

* Launch Docker.app. From your default Embox location run

        ./scripts/docker/docker_start.sh

  It's better not to have any other Docker containers launched (`docker ps -a` to check).

* To test your environment, you may run

        dr echo 1

* Docker now accepts any commands preceded with `dr`.

### Stop Emdocker

* Show active Docker containers:

        docker ps

* Kill and remove your container (will not delete the image):

        docker rm -f YOUR_CONTAINER_ID # will

* Stop the Docker machine:

        docker-machine stop default
