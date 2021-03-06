=================================================================================================================
Website for the `University of Michigan's <https://www.umich.edu/>`_ CHE 696: Data Science for Chemical Engineers
=================================================================================================================

The class's site is published here: https://team-mayes.github.io/che_696/

Setup
-----

The site is built with `Sphinx <http://www.sphinx-doc.org/en/master/index.html>`_, so you will need to
`install it <http://www.sphinx-doc.org/en/master/usage/installation.html>`_ in order to build the site.

Next, be sure that your Python environment has all of the libraries used by the Sphinx extensions employed
on this site:

::

    $ pip install -r source/requirements.txt

You may need to use ``sudo`` in order to install the modules for your Python environment.  It is also important
that you are updating the same Python environment as the one used by your Sphinx installation.  Here is one way
to determine which interpreter is being used:

::

    $ head -1 $(which sphinx-quickstart)
    #!/usr/bin/python3

In this case, we will need to install the packages using ``pip3`` since that's the pip command for the ``python3``
installation on my Linux machine.

::

    $ sudo pip3 install -r source/requirements.txt

Mac OSX
+++++++

If the above directions did not allow a successful build (next step), this alternate install may work. First,
install Xcode (via the App Store). Then, in the terminal:

::

    $ xcode-select --install

If problems remain with ipython, it may help to load:

::

    $ brew install ipython

Linux
+++++

Note that you will also need the ``make`` command installed on your machine.  For Debian-based Linux distributions,
this will work:

::

    $ sudo apt install make

Build
-----

To create the class's HTML site in the ``docs`` directory, run this command from the base directory of the project
(i.e. where the ``Makefile`` lives):

::

    $ make html

This will write your changes in the ``source`` directory to the ``docs`` directory.

Deploy
------

In order to deploy your changes to the `published site <https://team-mayes.github.io/che_696/>`_, check in your work
and push it to the ``master`` branch of the project.

::

    $ git add .
    $ git commit -m "Website changes"
    $ git push

If all goes well, you will see your changes on the site.

Clean
-----

If you are moving or removing resources for the site, you may want to run this command from the base of the project:

::

    $ make clean

This will effectively delete the contents of the ``docs`` directory.  You can clean and rebuild the site in a single
command by specifying multiple ``make`` targets:

::

    $ make clean html

Note that you will need to restore two files that are not auto-generated by Sphinx.  Run this ``git`` command to
restore these files:

::

    $ git checkout docs/.nojekyll docs/index.html

The first file tells the `GitHub Pages publisher <https://pages.github.com/>`_ to skip the
`Jekyll <https://jekyllrb.com/>`_ interpretation step, which allows directories that start with ``_`` to be copied
unchanged to the published site.  Since Sphinx makes use of the ``_`` convention extensively, this is an important
flag.  If you notice that your stylesheets, images, etc., are missing from the published site, it may be that the
``docs/.jekyll`` file is missing.  Note that the file itself is empty, so just creating an empty file suffices.

::

    $ touch docs/.nojekyll

The ``docs/index.html`` page is a simple redirect to the ``docs/html/index.html`` page.  Here are the full contents:

::

    <meta http-equiv="refresh" content="0; url=./html/index.html" />



