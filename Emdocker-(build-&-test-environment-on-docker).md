# Emdocker
Build & test environment on docker. Allows (or should allow :-)) to setup fully working development environment in one command.

## Linux
* Install docke`. For instructions for ubuntu refer to https://docs.docker.com/installation/ubuntulinux/
* Open terminal, change directory to embox project root.
* Start docker container with 
```
$ docker run -d -v $PWD:/embox -P --privileged embox/emdocker
```
* Try to execute command in container
```     
$ ./scripts/docker/docker_run.sh echo "Im alive"
```     
* You could make handy alias and start using it
```
$ alias dr="$PWD/scripts/docker/docker_run.sh"
$ dr make confload-x86/qemu
$ dr make
...
```

## Mac OS X
* Install docker https://docs.docker.com/installation/mac/
* Open Docker CLI and change directory to embox project root
* ... are identical to Linux
