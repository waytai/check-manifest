check-manifest
==============

|buildstatus|_ |coverage|_

Are you a Python developer?  Have you uploaded packages to the Python Package
Index?  Have you accidentally uploaded *broken* packages with some files
missing?  If so, check-manifest is for you.

Quick start
-----------

::

    $ pip install check-manifest

    $ cd ~/src/mygreatpackage
    $ check-manifest

You can ask the script to help you update your MANIFEST.in::

    $ check-manifest -u
    listing source files under version control: 6 files and directories
    building an sdist: check-manifest-0.7.tar.gz: 4 files and directories
    files in version control do not match the sdist!
    missing from sdist:
      tests.py
      tox.ini
    suggested MANIFEST.in rules:
      include *.py
      include tox.ini
    updating MANIFEST.in

    $ cat MANIFEST.in
    include *.rst

    # added by check_manifest.py
    include *.py
    include tox.ini


Command-line reference
----------------------

::

    $ check-manifest --help
    usage: check-manifest [-h] [--version] [-c] [-u] [-p PYTHON]
                          [--ignore patterns]
                          [source_tree]

    Check a Python MANIFEST.in file for completeness

    positional arguments:
      source_tree           location for the source tree (default: .)

    optional arguments:
      -h, --help            show this help message and exit
      --version             show program's version number and exit
      -c, --create          create a MANIFEST.in if missing (default: False)
      -u, --update          append suggestions to MANIFEST.in (implies --create)
                            (default: False)
      -p PYTHON, --python PYTHON
                            use this Python interpreter for running setup.py sdist
                            (default: /home/mg/.venv/bin/python)
      --ignore patterns     ignore files/directories matching these comma-
                            separated patterns (default: None)


Configuration
-------------

You can tell check-manifest to ignore certain file patterns by adding a
``check-manifest`` section to your package's ``setup.cfg``.  Example::

    [check-manifest]
    ignore =
        .travis.yml

The following options are recognized:

ignore
    A list of newline separated filename patterns that will be ignored by
    check-manifest.  Use this if you want to keep files in your version
    control system that shouldn't be included in your source distributions.
    The default ignore list is ::

        PKG-INFO
        *.egg-info
        *.egg-info/*
        setup.cfg
        .hgtags
        .hgignore
        .gitignore
        .bzrignore
        *.mo

ignore-default-rules
    If set to ``true``, your ``ignore`` patterns will replace the default
    ignore list instead of adding to it.


.. |buildstatus| image:: https://api.travis-ci.org/mgedmin/check-manifest.png?branch=master
.. _buildstatus: https://travis-ci.org/mgedmin/check-manifest

.. |coverage| image:: https://coveralls.io/repos/mgedmin/check-manifest/badge.png?branch=master
.. _coverage: https://coveralls.io/r/mgedmin/check-manifest

