================================
Set up a Development Environment
================================

Please have the followings ready before you start:

* Any Python installation with pip available.
* Conda from either Miniconda_ or Anaconda.

.. _Miniconda: https://conda.io/en/latest/miniconda.html

Please arrive early to the tutorial if you are not sure whether you have all
things set up. The lecturer will help get things ready.


Install development tools
=========================

Run the following command to install/update the needed development tools.

Anaconda::

    conda install conda-build

On Windows::

    py -3 -m pip install --upgrade pip setuptools wheel twine

On Mac or Linux::

    python3 -m pip install --upgrade pip setuptools wheel twine

.. note::

    For brevity, we will use ``py -3`` from here on. Please substitute it to
    ``python3`` yourself as needed, if you used ``python3`` for the above
    command.


.. _test-pypi-register:

Register an account on Test PyPI
================================

Register an account at https://test.pypi.org/account/register/.

Follow the steps to complete registration. You will also need to
**verify your email address** to be able to upload packages.


Put code in a directory
=======================

This tutorial uses a simple project named ``sampleproject``. The complete
source is available at https://github.com/pypa/sampleproject.git. We will be
creating the project from scratch, but you can use the repository as a
reference if anything is not working.

If you already have a project that you want to package up, *and feel confident*
to do so, simply replace the ``sample`` directory with the one you want to use,
and replace the metadata as appropriate.

We start with the following file structure::

    sampleproject/
        sample/
            __init__.py

All of the commands in this tutorial will need to be run within the top-level
directory just created. Be sure to ``cd sampleproject`` into the project
directory to run following commands successfully.
