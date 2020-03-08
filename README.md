# The NuttX Companion

This is the [NuttX Companion](https://nuttx-companion.readthedocs.io), a warm and friendly guide to all 
things [NuttX](https://nuttx.apache.org)– how to install it, configure it, develop on it, debug it, improve 
it, get help from its community, and generally have fun with this very capable, configurable,
fast, POSIX-compatible, internet-connected real-time operating system.

Hopefully this guide will complement the NuttX documentation, filling in gaps when needed, and
providing more help for people interested in learning about NuttX.

You can see the HTML version of this book here: [NuttX Companion](https://nuttx-companion.readthedocs.io).

## Building the Documentation

This book is written in [ReStructured Text (RST)](https://docutils.sourceforge.io/rst.html), and built using 
the excellent [Sphinx](https://www.sphinx-doc.org/) documentation system.

To install it, first install Python 3.8 or later and [Pipenv](https://pipenv-fork.readthedocs.io/en/latest/). 
Then from the `docs/` directory do:

```
$ pipenv install
$ pipenv shell
$ cd docs
$ make html

```

The documentation will be in the `_build/html` directory. You can open `_build/html/index.html`.

## Contributing

If there's anything you would like to improve, send me an email or a pull request! See
[Contributing to the NuttX Companion](https://nuttx-companion.readthedocs.io/en/latest/user/contributing.html) 
for more information.

cheers <br>
adam <br>
-- <br>
Adam Feuer <br>
Seattle, WA, USA <br>
