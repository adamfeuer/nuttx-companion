# The NuttX Companion


This is the [NuttX Companion](https://nuttx-companion.readthedocs.io), a warm and friendly guide to all 
things [NuttX](https://nuttx.apache.org)– how to install it, configure it, develop on it, debug it, improve 
it, get help from its community, and generally be happy and have fun with this very fast, small, capable, 
POSIX-compatible, internet-connected real-time operating system.

Hopefully this guide will complement the NuttX documentation, filling in gaps when needed, and
providing a way for people to get started with NuttX easily.

You can see the HTML version of this book here: [NuttX Companion](https://nuttx-companion.readthedocs.io).

## Building the Documentation

This book is written in [ReStructured Text (RST)](https://docutils.sourceforge.io/rst.html), and built using 
the excellent [Sphinx](https://www.sphinx-doc.org/) documentation system.

To install it, first install Python, Pip, and Pipenv. Then from the `docs/` directory do:

```
$ pipenv install
$ pipenv shell
$ make html

```

The documentation will be in the `_build/html` directory. You can open `_build/html/index.html`.

## Contributing

If there's anything you would like to improve, send me an email or a pull request!

cheers <br>
adam <br>
-- <br>
Adam Feuer <br>
Seattle, WA, USA <br>
