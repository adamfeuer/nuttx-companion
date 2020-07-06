.. include:: /substitutions.rst
.. _drivers:

Drivers
=======

Some NuttX boards don't have full support for all the on-chip peripherals. If you need support for this hardware,
you will either need to port a driver from another chip, or write one yourself. This section discusses how to do that.

Porting a Driver
----------------

Often support for on-chip peripherals exists in a closely related chip, or even a different family or from a different
manufacturer. Many chips are made up of different Intellectual Property (IP) blocks that are licensed from vendors like
Cadence, Synopsys, and others. The IP blocks may be similar enough to use another chip's driver with little
modification.

* Find a similar driver in NuttX source code

  * many SoC peripherals use the same IP blocks from tools vendors (Cadence etc.)
  * How to do it:

     * Look at register names listed in the datasheet for the peripheral
     * Search the NuttX codebase for the names (try several different ones)

* Find a similar driver in U-Boot source code

  * Only for inspiration, can't borrow code because of license incompatibility
  * But can debug to see how it works.
  * U-Boot drivers are often simple enough to understand easier than BSD Unix drivers

* Find a similar driver in BSD Unix (OpenBSD, FreeBSD, NetBSD)

  * Can borrow code directly (Apache 2.0 and BSD licenses are compatible)

* printf debugging

  * custinfo()
  * debug settings file and easy cat after menuconfig
  * interrupts
  * stack frame printf
  * thread printf

* GDB

  * awesome tool
  * add xxd command to examine memory
  * memset buffers to '-' for easy reading
  * maybe also recompile for python 3??

* General

  * datasheets are your friend
  * How to read / use a datasheet
  * Logic analyzer is your friend

    * How to use

* DMA debugging

  * dump registers before, during, and after transfer
  * sample






