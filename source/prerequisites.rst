================================
Set up a Development Environment
================================

Please have the followings ready before you start:

* Any Python installation with either virtualenv or venv available.
* Conda from either Miniconda_ or Anaconda.

.. _Miniconda: https://conda.io/en/latest/miniconda.html

Please arrive early to the tutorial if you are not sure whether you have all
things set up. The lecturer will help get things ready.


Put code in a directory
=======================

This tutorial uses a simple project named ``sampleproject``. The complete source
is available at https://github.com/pypa/sampleproject.git. We will be creating
the project from scratch, but you can use the repository as a reference if
anything is not working.

If you already have a project that you want to package up, *and feel confident*
to do so, simply replace the ``sample`` directory with the one you want to use,
and replace the metadata as appropriate.

We start with the following file structure::

    sampleproject/
        sample/
            __init__.py
