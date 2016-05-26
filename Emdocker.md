# Emdocker
Build & test environment on docker. Allows to setup fully working development environment in one command.

## Setup

* Install docker.  Please refer to docker official installation instructions.
 * Linux: https://docs.docker.com/linux/step_one/
 * MacOS: https://docs.docker.com/mac/step_one/
 * Windos: https://docs.docker.com/windows/step_one/

* Pull emdocker image
```
$ docker pull embox/emdocker
```

## Using

* Open terminal, change directory to embox project root.
* Start docker container with
```
$ ./scripts/docker/docker_start.sh
```
* Source bash docker utillities
```
$ . ./scripts/docker/docker_rc.sh
```
This mostly defines `dr` (from docker run) alias. Every command prepended with `dr` will be executed in container. Now you're ready to test you new shiny environment, like
```
$ dr echo I am alive!
```
* That's all! Now you can build and test embox in the contaner. Just remember to type `dr`. For example, reassembling main README:
```
$ dr make confload-x86/qemu
$ dr make
$ dr ./scripts/qemu/auto_qemu -s -S
```
### gdb
Few notes on gdb (client). Bare `dr gdb` will not work all the time, because this will handle signal wrong way, closing the container wrapper instead of signaling to gdb. Particullary, `Ctrl+C` will not interrupt application and invoke gdb REPL.

To fix this, `./scripts/docker/gdbhostwrapper` introduced to passthrough singals to gdb running in container. Just use it as gdb starter script on host computer, from any environment like shell or Eclipse.

### Eclipse

Eclipse already have some emdocker support. However, it requires PATH to include embox's `scripts/docker` directory. So recommended way to start Eclipse is from embox root directory like
```
$ PATH=$PATH:$PWD/scripts/docker/ PATH/TO/eclipse &
```

Support includes:

* `docker-run` make build target used to build embox (depends on  `docker_run.sh`)
* `qemu_on_docker` debugging target used to debug embox on qemu, which runs in container. Target have `gdbhostwrapper` specified as a debugger, as Eclipse use gdb as debugger backend and sends signals too (refer to gdb section for details)

### Accessing embox network services

For simple CLI network access to embox one can type `dr bash` and get container's bash session. There embox is accessible as usual (`ping 10.0.2.16`, `curl 10.0.2.16:80`)

To access embox services from host, you should know host running the container. On linux, this is `localhost`. On MacOS/Windows with classic Docker, type `docker-machine ip` and get host's ip. Then use this ip address and port (10000 + embox_port) to access the service. For example `localhost:10080` on linux will be redirected embox's port 80.
