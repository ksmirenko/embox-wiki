## 2015/07/04 v0.3.10

  * Cleaned source code
  * Added demo "IP phone on STM32F407 board"
  * Supported USB-NET
  * Supported STM32F3discovery board
  * Added a new VFS
  * Added a new flash file system for configuration

## 2015/04/12 v0.3.9

  * Enabled a new annotation for public headers
  * Supported protocol !ModBus with libmodbus library
  * Replaces Lisp500 with schema language
  * Supported mruby language
  * Fixed some errors in TCP, during incorrect treatment closes the socket
  * Replaced Softirq by ligth_threads
  * Fixed nanosleep() for a short time periods
  * Improved FAT implementation  
  * Supported SD card for STM32F4Discovery  

## 2014/09/28 v0.3.8

  * Reworked MMU platform (supported  MMU on: x86, Microblaze, SPARC (leon3))
  * Improve TCP/IP stack
  * Added PacketDrill framework for network testing
  * Embox ported to STM32F407
  * Ported pjsip library for SIP stack support
  * Enable cgi in httpd (c and lua)

## 2014/06/01 v0.3.7

  * Reworked memory subsystem (Own heap for each task)
  * Added vfork()
  * Added easier way to porting third party application with GNU build system (configure, make)
  * Added TCL support
  * Added regression testing
  * Fixed many errors in IP stack and file system

## 2014/02/01 v0.3.6

  * Reworked 'index descriptor' subsystem
  * Supported file systems (Ext4, CIFS)
  * Added new type user module (applications)
  * Added Virtio-net network card
  * Supported USB
  * Added SysLink framework for Davinci chip
  * Reworked 'task' module

## 2013/09/15 v0.3.5

  * Supported MSP430 cpu architecture
  * Supported file systems (Ext3, jffs2)
  * Added jornal and cache for block devices
  * Supported Greth network card
  * Reworked 'scheduler' module
  * Improved IP stack

## 2013/06/01 v0.3.4

  * Supported PowerPC architecture
  * Supported multiuser mode
  * Supported jvm (MontyVM)
  * Supported video card drivers (framebuffer)
  * Supported Qt embedded  
  * Supported Ext2
  * Reworked terminal subsystem
  * Reworked scheduler
  * Added lightweight threads for kernel using (workers)

## 2012/10/23 v0.3.3

  * Added MIPS architecture support
  * Added virtual mode for x86 architecture

### Network

  * Improved telnet server
  * Added rlogin
  * Added NTP client

### File System

  * Added FS ISO9660 (CDROM)

### Others

  * Added stacktrace for x86 and SPARC architectures
  * Added pipes 
  * Added Network card E1000 support

## 2012/07/09 v0.3.2

### Network

  * Added telnetd server
  * Added RPC implementation
  * Added protocol NFS

### File system

  * Improve structure
  * Added NFS client

### Other

  * Reworked time subsystems
  * Add template for STM32vl discovery
  * Improve biuld system Mybuild

## 2012/04/15 v0.3.1

### Network

  * Added TCP protocol
  * Added simple httpd sever
  * Improved socket interface

### File system

  * Added FAT format
  * Added RAM-disk support

### Examples

  * Network using (sockets, TCP, ..)
  * Dynamic memory allocation

### Others

  * Fixed some another bugs
  * Cleared code a little

## 2012/02/26 v0.3.0

_Dedicated to Sikmir's children (Timur and Eugene)_

### Development

  * Add [http://www.lua.org/about.html Lua 5.1] scripting support

### Drivers

  * Added RTL8139 Network Chip driver

### Build System

  * Complete migrating Embox build scripts to Mybuild files (no more Makefiles in the source tree)

## 2011/12/01 v0.2.3

  * Added new dynamic allocation (bitmask for page allocation and boundary markers for malloc)
  * Started Lua porting
  * Started *pnet* stack research

## 2011/09/25 v0.2.2

### Build Systems

  * Possibility of different interfaces header files
  * New types of modules (services and examples)

### Development

  * Redesigned timers subsystems
  * Implemented a single OBJALLOC interface
  * Add POSIX subset
  * Development of the terminal
  * Tasks

### Platforms and architectures

  * Code clean up for ARM, x86, Microblaze
  * Add examples and code clean up for Lego

## 2011/07/04 v0.2.1

## x86

  * Support ne2000 board on PCI bus

### Network

  * Loopback support

## 2011/05/15 v0.2.0

### Build System

  * Added opportunity to specify system interfaces and their implementation
  * New interface of test definition
 
### Kernel

  * Refactoring scheduler with priority
  * Added message dispatcher
  * New multy instance console 

## 2011/03/11 v0.1.11

### Lego NXT

  * Support bluetooth comunication
  * Support color sensor
  * Desing some examples

### x86

  * Support QEMU platform
  * Support PCI bus

## 2010/10/25 v0.1.8

### Lego Mindstorms NXT 2.0
  * ARM7 bootstrap and proper AVR initialization
  * Display and Sound
  * Snake ported to the Lego brick

### File System

  * Logical FS
  * initfs

## 2010/10/25 v0.1.8

### Lego Mindstorms NXT 2.0

  * ARM7 bootstrap and proper AVR initialization
  * Display and Sound
  * Snake ported to the Lego brick

### File System

  * Logical FS
  * initfs

## 2010/10/01 v0.1.7

  * Code clean up
  * Check the results
  * Build system improvements

## 2010/07/23 v0.1.6

 Lanit-Tercom Summer School results presentation.

## 2010/06/28 v0.1.5

 Starting Lanit-Tercom Summer School.

### Threading

  * The scheduler supports state of threads: RUN, READY, SLEEP
  * The scheduler manages the queues of same state threads.
  * Thread synchronization primitives: mutex and conditional variables
  * All above functionality is demonstrated by tests.

### Memory

  * Code review of previous results (Page_alloc, virtual memory, malloc).
  * Written wiki pages with the justification what is a virtual memory for, and why it's bad to use the method of boundary markers.
  * Virtual memory tests are written.

## 2010/05/19 v0.1.4

The presentation of results of the student project. 

## 2010/05/01 v0.1.3

### Threading

* Trivial scheduler is working.
* A test (or command), which runs 2 threads, one of them wrote to the console "-" other "+". At the console displays a sequence of alternating somehow "+" and "-". 

### Manager of memory

* Allocation of memory pages.
* A test: look amount of memory, allocate, look, release and so on. 

### Virtual memory

* Context switching is working.
* A test for virtual memory is implemented: e.g., 2 functions of the different contexts in turn something written in one virtual address and then verify the correctness of records. 

### User applications

* Written application in C, which parses the ELF header file and displays its contents to the console. The result of processing coincides with the objdump.
* That application is integrated into Embox as a module.
* readelf: displays information about ELF format object files. 

### Network

* supported for loopback
* supported for ICMP
* implemented ioctl interface for sockets

## 2010/04/16 v0.1.2

All tasks are distributed to the participants of Lanit-Tercom 2010 spring student project. 

## 2010/04/02 v0.1.1

The presentation of hardware testing tools. 

## 2010/03/13 v0.1 

Time beginning. 