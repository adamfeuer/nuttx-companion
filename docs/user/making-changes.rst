.. include:: /substitutions.rst
.. _making-changes:

Making Changes To NuttX
=======================

If you want to make changes to NuttX, for your own personal use, or to submit them back to project to improve NuttX,
that's easy. You'll need a `GitHub <https://www.github.com>`_ account. Here's how:

#. Sign in to GitHub

   If you don't have a `GitHub <https://www.github.com>`_ account, it's free to sign up.


#. Fork the project on GitHub

   Visit both these links and hit the Fork button in the upper right of the page:

   * `NuttX <https://github.com/apache/incubator-nuttx/>`_
   * `NuttX Apps <https://github.com/apache/incubator-nuttx-apps/>`_


#. Change the Git Remotes

   The git repositories in your project are currently connected to the official NuttX repositories, but you don't
   have permission to submit software there. But you can submit them to your forks, and from there create Pull Requests
   if you want to send them to the NuttX project.

   First, remove the current remote, ``origin`` (we'll add it back later):

    .. code-block:: bash

       $ cd nuttx/
       $ # display the remote
       $ git remote -v

   You should see something like this:

    .. code-block:: bash

       origin	https://github.com/apache/incubator-nuttx.git

   Now, on the GitHub web page for your forked ``incubator-nuttx`` project, copy the clone url – get it by hitting the
   green ``Clone or Download`` button in the upper right. Then do this:

    .. code-block:: bash

       $ git remote rm origin
       $ git remote add origin <your forked incubator-nuttx project clone url>
       $ git remote add upstream https://github.com/apache/incubator-nuttx.git

   Do the same for your forked ``incubator-nuttx-apps`` project:

    .. code-block:: bash

       $ git remote rm origin
       $ git remote add origin <your forked incubator-nuttx-apps project clone url>
       $ git remote add upstream https://github.com/apache/incubator-nuttx-apps.git


#. Create a Local Git Branch

   Now you can create local git branches and push them to GitHub:

    .. code-block:: bash

       $ git checkout -b test/my-new-branch
       $ git push

