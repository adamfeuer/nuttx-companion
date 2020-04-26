.. include:: /substitutions.rst
.. _quickstart:

Quickstart
==========

Here's the quick version of getting things going. This is a bare-bones outline for experienced developers– if it's
going too quickly, dive into the other sections of the Companion. This Quickstart guide assumes you're on a Linux
computer, you're using an ARM processor on your embedded board, and you're familiar with using the command line.

#. Install a Cross-Compiler Toolchain

   With NuttX, you compile the operating system and your application on your desktop or laptop computer, then install the
   binary file on your embedded computer. This guide assumes your computer is an
   `ARM <https://en.wikipedia.org/wiki/ARM_architecture>`_ CPU. If it isn't, you'll need a different tool chain.

   Download the right flavor of the
   `ARM Embedded Gnu Toolchain <https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm>`_
   for your embedded processor's CPU.

   Unpack it into ``/opt/gcc`` and add the bin directory to your path. For instance:

    .. code-block:: bash

       $ sudo mkdir /opt/gcc
       $ sudo chgrp -R users /opt/gcc
       $ cd /opt/gcc
       $ wget https://developer.arm.com/-/media/Files/downloads/gnu-rm/9-2019q4/gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2?revision=108bd959-44bd-4619-9c19-26187abf5225&la=en&hash=E788CE92E5DFD64B2A8C246BBA91A249CB8E2D2D
       $ tar xf gcc-arm-none-eabi-9-2019-q4-major-x86_64-linux.tar.bz2
       $ # add the toolchain bin/ dir to your path...
       $ # you can edit your shell's rc files if you don't use bash
       $ echo "export PATH=/opt/gcc/gcc-arm-none-eabi-9-2019-q4-major/bin:$PATH" >> ~/.bashrc


#. Download Apache NuttX

    .. code-block:: bash

       $ mkdir nuttx
       $ cd nuttx
       $ git clone https://github.com/apache/incubator-nuttx.git nuttx
       $ git clone https://github.com/apache/incubator-nuttx-apps apps

#. List Possible Apache NuttX Base Configurations

   Find your hardware and a good starting application in the list of base configurations. In the application list,
   ``nsh`` is the Apache NuttX Shell, an interactive commandline that's a good starting place if you're new.

    .. code-block:: bash

       $ cd nuttx
       $ ./tools/configure.sh list | less

#. Initialize Configuration

   Pick one of the board:application base configuration pairs from the list, and feed it to
   the configuration script. The ``-l`` tells us that we're on Linux. macOS and Windows builds
   are possible, this Companion doesn't cover them yet.

    .. code-block:: bash

       $ cd nuttx
       $ ./tools/configure.sh -l <board-name>:<config-dir>
    
#. Customize Your Configuration (Optional)

   This step is optional. Right now, this is mainly to get familiar with how it works– you don't need to change
   any of the options now, but knowing how to do this will come in handy later.

   There are a lot of options. We'll cover a few of them here. Don't worry about the complexity– you don't have to use most of the options.

    .. code-block:: bash

       $ make menuconfig


#. Compile Apache NuttX

    .. code-block:: bash

       $ make clean; make

#. Install the Executable Program on Your Board

   This step is a bit more complicated, depending on your board. It's covered in the section
   :ref:`Running Apache NuttX <running>`.
