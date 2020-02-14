.. include:: /substitutions.rst
.. _install:

Installing NuttX
================

To start developing on NuttX, we need to get the source code, configure it, compile it, and get it uploaded onto an
embedded computing board.

Install a Cross-Compiler Toolchain
----------------------------------

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


Get the Source Code
-------------------

NuttX is `actively developed on GitHub <https://github.com/apache/incubator-nuttx/>`_. If you want
to use it, modify it or help develop it, you'll need the source code.

You can either clone the public repositories:

    .. code-block:: bash

       $ mkdir nuttx
       $ cd nuttx
       $ git clone https://github.com/apache/incubator-nuttx.git
       $ git clone https://github.com/apache/incubator-nuttx-apps

Or, download the `tarball <https://github.com/apache/incubator-nuttx/tarball/master>`_:

    .. code-block:: bash

       $ curl -OL https://github.com/apache/incubator-nuttx/tarball/master
       $ curl -OL https://github.com/apache/incubator-nuttx-apps/tarball/master
       # optionally, zipball is also available (for Windows users).

Later if we want to make modifications (for instance, to improve NuttX and save them in our own branch,
or submit them back to the project), we can do that easily. It's covered in the section
:ref:`Making Changes <making-changes>`.