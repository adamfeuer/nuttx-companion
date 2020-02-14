.. include:: /substitutions.rst
.. _install:

Installing NuttX
================

To start developing on NuttX, we need to get the source code, configure it, compile it, and get it loaded onto an embedded computing
board.

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

