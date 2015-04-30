Agendaess-Deploy Fork
---------------------

Changes: put "python" links in /usr/local/bin, don't try to build 2.4 (doesn't
build on Ubuntu 14.04), make sure we get pypy and pypy3 on Ubuntu.  The changes
I've made to the pypy and pypy3 configs mean this will actually only work on
Ubuntu.

Introduction
------------

This buildout is a collection of configurations to make it easy to compile
various Python versions with or without the necessary dependencies.

The default ``buildout.cfg`` configuration is for Mac OS X Leopard, because that's
what this buildout was initially created for.

Installation
------------

See ``docs/INSTALL.txt``

Upgrade
-------

See ``docs/UPGRADE.txt``

Advanced Usage
--------------

The buildout is split up to make it easy to mix and match the parts you need.

If the ``links.cfg`` is used, then a script ``install-links`` is created in the
``bin`` directory. That script makes it easy to create symbolic links to all
the binaries and scripts in this buildout. You should set the destination for
those links by creating a ``local.cfg`` with the following content and run it
with ``bin/buildout -c local.cfg`` after modifying the ``prefix`` setting to your
needs::

    [buildout]
    extends = buildout.cfg

    [install-links]
    prefix = /path/for/the/links

The buildout is built in a way that you can easily extend it with your own
configuration.

Just get a Git clone::

    git clone git://github.com/collective/buildout.python.git python

And use a custom ``buildout.cfg`` like this::

    [buildout]
    extends = python/src/base.cfg python/src/python27.cfg
    python-buildout-root = ${buildout:directory}/python/src

If you want just one python version but all dependencies, then use something
like this::

    [buildout]
    extends =
      src/base.cfg
      src/readline.cfg
      src/libjpeg.cfg
      src/python25.cfg
      src/links.cfg

    python-buildout-root = ${buildout:directory}/src

    parts =
        ${buildout:base-parts}
        ${buildout:readline-parts}
        ${buildout:libjpeg-parts}
        ${buildout:python25-parts}
        ${buildout:links-parts}

The ``python-buildout-root`` setting is important, otherwise the whole buildout
doesn't work.
