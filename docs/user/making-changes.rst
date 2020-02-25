.. include:: /substitutions.rst
.. _making-changes:

Making Changes To NuttX
=======================

If you want to make changes to NuttX, for your own personal use, or to submit them back to project to improve NuttX,
that's easy. For the purposes of this guide, you'll need a `GitHub <https://www.github.com>`_ account, since
the Apache NuttX team uses GitHub. (You could also use git locally, or save your changes to other sites like
`GitLab <https://about.gitlab.com/>`_ or `BitBucket <https://bitbucket.org>`_, but that's beyond the scope of this
guide).

Here's how to do it:


#. Sign in to GitHub

   If you don't have a `GitHub <https://www.github.com>`_ account, it's free to
   sign up.
   |br|
   |br|


#. Fork the Project

   Visit both these links and hit the Fork button in the upper right of the page:

   * `NuttX <https://github.com/apache/incubator-nuttx/>`_
   * `NuttX Apps <https://github.com/apache/incubator-nuttx-apps/>`_


#. Change the Git Remotes

   The git repositories in your project are currently connected to the official NuttX repositories, but you don't
   have permission to push software there. But you can push them to your forks, and from there create Pull Requests
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

       $ cd ../apps
       $ git remote rm origin
       $ git remote add origin <your forked incubator-nuttx-apps project clone url>
       $ git remote add upstream https://github.com/apache/incubator-nuttx-apps.git


#. Create a Local Git Branch

   Now you can create local git branches and push them to GitHub:

    .. code-block:: bash

       $ git checkout -b test/my-new-branch
       $ git push


Git Workflow With an Upstream
-----------------------------

Working with an upstream repo is a bit more complex, but it's worth it since you can submit fixes and features
to the main NuttX repos. One of the things you need to do regularly is keep your local repo in sync
with the upstream. I work with a local branch, make changes, pull new software from the upstream and merge it in,
maybe doing that several times. Then when everything works, I get my branch ready to do a Pull Request. Here's how:

#. Fetch upstream changes and merge into my local master:

    .. code-block:: bash

       $ git checkout master
       $ git fetch upstream
       $ git merge upstream/master

#. Merge my local master with my local branch:

    .. code-block:: bash

       $ git checkout my-local-branch
       $ git merge master

#. Make changes and push them to my fork

    .. code-block:: bash

       $ vim my-file.c
       $ git add my-file.c
       $ git commit my-file.c
       $ git push

#. Repeat 1-3 as necessary

#. Run the ``tools/checkpatch.sh`` script on your files

   When your code runs, then you're almost ready to submit it. But first you need to check the code to ensure
   that it conforms to the `NuttX Coding Standard <https://cwiki.apache.org/confluence/display/NUTTX/Coding+Standard>`_.
   The ``tools/checkpatch.sh`` script will do that. Here's the usage info:

    .. code-block:: bash

       $ ./tools/checkpatch.sh -h
       USAGE: ./tools/checkpatch.sh [options] [list|-]

       Options:
       -h
       -c spell check with codespell(install with: pip install codespell
       -r range check only (used with -p and -g)
       -p <patch list> (default)
       -g <commit list>
       -f <file list>
       -  read standard input mainly used by git pre-commit hook as below:
          git diff --cached | ./tools/checkpatch.sh -

   Run it against your files and correct all the errors, so that ``tools/checkpatch.sh`` reports no errors. Then commit the result.
   For example:

    .. code-block:: bash

       $ ./tools/checkpatch.sh -f my-file.c
       arch/arm/src/sama5/hardware/my-file.c:876:82: warning: Long line found
       $ # fix errors
       $ vim my-file.c
       $ # run again
       $ ./tools/checkpatch.sh -f my-file.c

#. Commit the fixed files

    .. code-block:: bash

       $ git add my-file.c
       $ git commit my-file.c
       $ git push


Submitting Your Changes to NuttX
--------------------------------

The NuttX team wants all the changes you made in your branch "squashed" into a single commit, so that when they merge
your changes to master, there's a clean view of the history– each Pull Request is in a single commit. Here's the
easiest way I found to do that:

#. Check out my branch

    .. code-block:: bash

       $ git checkout my-branch

#. Rename it to ``my-branch-old`` to save it, because we're going to create new clean branch to push:

    .. code-block:: bash

       $ git branch -m my-branch-old

#. Create a new clean branch with the same name you were using before the last step:

    .. code-block:: bash

       $ git checkout master
       $ git checkout -b my-branch

#. Merge your saved old branch into the new one, telling git to "squash" all your commits into one:

    .. code-block:: bash

       $ git merge --squash my-branch-old

#. Commit the result

    .. code-block:: bash

       $ git commit

#. Force-push your new clean branch to the remote- this will overwrite all your previous changes in that branch:

    .. code-block:: bash

       $ git push -f

#. Create a GitHub Pull Request

   A Pull Request is how you ask your upstream to review and merge your changes.

   Here's `GitHub's instructions for creating a Pull Request <https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request>`_.

Git Resources
-------------

* `Git Cheat Sheet (by GitHub) <https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf>`_
* `Git Book (online) <https://git-scm.com/book/en/v2>`_
