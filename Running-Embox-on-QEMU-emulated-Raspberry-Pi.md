## Prerequisites
In order to emulate the Raspberry Pi on QEMU you need a patched version of the emulator that supports the RPi machine. This patched version has been developed by Torlus and can be downloaded and installed with the following commands:

    git clone -b rpi https://github.com/Torlus/qemu.git
    cd qemu
    git submodule update --init pixman
    git submodule update --init dtc
    ./configure --target-list=arm-softmmu,arm-linux-user,armeb-linux-user --enable-sdl
    make && sudo make install

Of course you are free to use `configure` options to install QEMU wherever you want in your filesystem.

More information on the patched version of QEMU for emulating RPi can be found at the following links:
* [QEMU patches for RPi emulation - Initial release](https://www.raspberrypi.org/forums/viewtopic.php?t=26561&p=725758)
* [QEMU branches - rpi (Raspberry Pi) - firebee](https://github.com/Torlus/qemu/tree/rpi)
* [Raspberry Pi Bare Bones - Testing your operating system (QEMU)](http://wiki.osdev.org/Raspberry_Pi_Bare_Bones#Testing_your_operating_system_.28QEMU.29)

## Building Embox for QEMU
There is a special `arm/raspi` configuration template for Raspberry Pi. So first of all, preload it with:

    make confload-arm/raspi

One thing to notice about running Embox on QEMU is that, unfortunately, the `raspi` emulation may incorrectly load the kernel binaries at 0x10000 instead of 0x8000. In fact, you try to compile the kernel and run it you will see no output. What you have to do it to modify the `conf/lds.conf` file to use 0x10000 instead of 0x8000.

After that build the kernel using the following command:

    make

## Running Embox on QEMU
Once you have built the kernel you are ready to run it on QEMU. Just type on the command line:

    qemu-system-arm -kernel your-embox-dir/build/base/bin/embox -cpu arm1176 -M raspi -m 256 -no-reboot -serial stdio