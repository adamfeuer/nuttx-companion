.. include:: /substitutions.rst
.. _quickstart:

Quickstart
==========

Here's the quick version of getting things going. This is a bare-bones outline for experienced developers– if it's going too quickly, dive into the other 
sections of the Companion.

#. Download NuttX

    .. code-block:: bash

       $ mkdir nuttx
       $ cd nuttx
       $ git clone https://github.com/apache/incubator-nuttx.git nuttx
       $ git clone https://github.com/apache/incubator-nuttx-apps apps

#. List Possible NuttX Base Configurations

   Find your hardware and a good starting application in the list of base configurations. In the application list,
   ``nsh`` is the NuttX Shell, an interactive commandline that's a good starting place if you're new.

    .. code-block:: bash

       $ cd nuttx
       $ ./tools/configure.sh list | less

#. Configure NuttX Using a Base Configuration

   Pick one of the board:application configuration pairs from the list, and feed it to the configuration script. 
   The ``-l`` tells use that we're on Linux. macOS and Windows builds are possible, this Companion doesn't cover them
   yet.

    .. code-block:: bash

       $ cd nuttx
       $ ./tools/configure.sh -l <board-name>:<config-dir>
    
#. Customize Your Configuration

   There are a lot of options. We'll cover a few of them here. Don't worry about the complexity– you don't have to use most of the options.

    .. code-block:: bash

       $ make menuconfig


#. Compile NuttX

    .. code-block:: bash

       $ make clean; make

