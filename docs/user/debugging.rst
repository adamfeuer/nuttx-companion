.. include:: /substitutions.rst
.. _debugging:

Debugging
=========

Finding and fixing bugs is an important part of the hardware and software development process. Sometimes you also need
to use debugging techniques to understand how the system works. Two tools that are helpful are debug logging and
debugging using the Gnu Debugger (gdb).

Debug Logging
-------------

NuttX has a powerful logging facility with ``info``, ``warn``, and ``error`` levels. You can enable debugging for your
build by puttting the follwing lines in your ``.config`` file:

    .. code-block::

       CONFIG_DEBUG_ALERT=y
       CONFIG_DEBUG_FEATURES=y
       CONFIG_DEBUG_ERROR=y
       CONFIG_DEBUG_WARN=y
       CONFIG_DEBUG_INFO=y
       CONFIG_DEBUG_ASSERTIONS=y
       CONFIG_DEBUG_NET=y
       CONFIG_DEBUG_NET_ERROR=y
       CONFIG_DEBUG_NET_WARN=y
       CONFIG_DEBUG_NET_INFO=y
       CONFIG_DEBUG_SYMBOLS=y
       CONFIG_DEBUG_NOOPT=y
       CONFIG_SYSLOG_TIMESTAMP=y

Note that turning all these to ``y`` will produce an incredible amount of logging output. Set the level you want and
the area you're interested in to ``y``, and the rest to ``n``, and then recompile. You can see the full list of
areas in the file `debug.h <https://github.com/apache/incubator-nuttx/blob/master/include/debug.h>`_.

Timestamps can be enabled by setting ``CONFIG_SYSLOG_TIMESTAMP=y``.

You may need to do a little bit of experimenting to find the combination of logging settings that work for the problem
you're trying to solve.

There are also subsystems that enable USB trace debugging, and you can log to memory too, if you need the logging to be
faster than what the console can output

Custom Debug Logging
--------------------

Sometimes you need to see debug logs specific to your feature, and you don't want the rest of the built-in logs
because they're either not relevant or have too much information. You can add your own custom debug logging by
adding the following lines to `debug.h <https://github.com/apache/incubator-nuttx/blob/master/include/debug.h>`_:


    .. code-block:: c

       /* after the CONFIG_DEBUG_WATCHDOG_INFO block near line 716 */
       #ifdef CONFIG_DEBUG_CUSTOM_INFO
       #  define custinfo(format, ...)   _info(format, ##__VA_ARGS__)
       #else
       #  define custinfo(x...)
       #endif


       /* after the CONFIG_DEBUG_WATCHDOG_INFO block near line 1314 */
       #ifdef CONFIG_DEBUG_CUSTOM_INFO
       #  define custinfo      _info
       #else
       #  define custinfo      (void)
       #endif

You would use it like this:

    .. code-block:: c

       /* Custom debug logging */
       custinfo("This is a custom log message.");
       custinfo("Custom log data: %d", my-integer-variable);


JTAG Debugging
--------------

`JTAG <https://en.wikipedia.org/wiki/JTAG>`_ is a set of standards that specify a way to attach a hardware device to
your embedded board, and then remotely control the CPU. You can load code, start, stop, step through the program, and
examine variables and memory.

This guide assumes your board has a JTAG connector, and you have a JTAG hardware debugger like a
`Segger J-Link <https://www.segger.com/products/debug-probes/j-link/>`_ or `OpenOCD <http://openocd.org/doc-release/html/index.html>`_.

The NuttX operating system uses `threads <https://en.wikipedia.org/wiki/Thread_(computing)>`_, so you need a
thread-aware debugger to do more than load code, start, and stop it. A thread-aware debugger will allow you to switch
threads to the one that is running the code you're interested in, for instance your application, or an operating system
network thread. So far, OpenOCD is the only supported NuttX thread-aware debugger.

You will need an OpenOCD-compatible hardware adapter, ideally a fast one (USB 2.0 High Speed). This guide assumes you
are using the `Olimex ARM USB TINY H <https://www.olimex.com/Products/ARM/JTAG/ARM-USB-TINY-H/>`_.
(`Olimex ARM USB TINY H on Amazon <https://smile.amazon.com/Olimex-ARM-USB-TINY-H-Arm-Jtag/dp/B009UED630/>`_.) Other
adapters may work, follow the OpenOCD instructions and the instructions that came with your adapter.

You'll need to use the `Sony fork of OpenOCD <https://github.com/sony/openocd-nuttx>`_. Download and install it
according to the OpenOCD instructions.

See this article for more info:
`Debugging a NuttX target with GDB and OpenOCD <https://micro-ros.github.io/docs/tutorials/advanced/debugging_gdb_openocd/>`_.


