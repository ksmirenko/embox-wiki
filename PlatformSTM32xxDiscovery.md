The board has integrated debugger that allows to program it with single USB-A-USB-mini-B wire. You can run and test Embox after few quite simple steps. Please, read it all before doing anything.
 * Install OpenOCD v0.6.0 or later.
 * Configure and compile with *arm/stm32xx* template. Now supported:
    * arm/stm32f4cube for stm32f4discovery
    * arm/stm32f3cube for stm32f3discovery
    * arm/stm32_vl for stm32vldiscovery
 * In command line run

 ```
 $ sudo openocd -f /usr/share/openocd/scripts/board/stm32XXdiscovery.cfg
 ```

 where XX is 'vl', 'f3', 'f4'
 * Load Embox with usual gdb commands

 ```
 $ gdb build/base/bin/embox
 (gdb) target extended-remote :3333
 (gdb) monitor halt
 (gdb) load
 (gdb) monitor reset
 ```

N.B. Invoking host `gdb` should be enough for loading embox firmware but for real debuging `gdb-multiarch` (Ubuntu) or `arm-none-eabi-gdb` (Debian, Arch) are required.