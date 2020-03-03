===========================
Distribute Private Projects
===========================

We have been talking about how to release your package to the public, and it is
a common misconception that package publishing is only for open source.

While it is true that Python package managers are more focused on working with
open source (because they are part of it), they are also used by a lot of
people to publish packages in private settings, so various projects in a
company can easily share code, deploy software, and manage version upgrades.


Custom Conda channels
=====================

In Conda, you can choose to install packages from a specific *channel*, which
means Conda will look at that location for the package.
`Anaconda for Enterprise`_ offers a private channel service (i.e. publish
packages that only authorised people can download), but it is also easy to
run a channel server yourself, either with HTTP(S), or even with a shared disk
that's accessible with ``file://``.

.. _`Anaconda for Enterprise`: https://www.anaconda.com/enterprise/

A Conda channel is structured like this::

     channel/
        linux-64/
            ... packages
        linux-32/
            ... packages
        osx-64/
            ... packages
        win-64/
            ... packages
        win-32/
            ... packages

The root directory can be any directory on disk, and can take any name, but
here we use ``channel`` as an example. Each directory inside root represents
a platform to support; you can omit any you do not plan to support. Package
files (like our previous ``sampleproject-YOUR-USERNAME-0.0.1-py38_0.tar.bz2``)
are put inside each directory to make them downloadable.

Run the following command to generate a repository listing::

    conda index channel/

This will generate a file ``repodata.json`` in each repository directory, which
Conda uses to get the metadata for the packages in the channel.

.. note::

    Re-run ``conda index`` each time you add or modify anything in the channel
    (e.g. release a new package version), to keep the metadata up-to-date.

To install from the custom index, use the following syntax::

    conda install --channel=file://path/to/channel/ sampleproject-YOUR-USERNAME

You can also set up the channel in your |condarc|_ to avoid specifying the
channel every time.

.. |condarc| replace:: ``.condarc``
.. _condarc: https://docs.conda.io/projects/conda/en/latest/user-guide/configuration/use-condarc.html


"Find-links" pages
==================

TODO...


devpi
=====

TODO...
