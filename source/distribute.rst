======================
Distribute the Project
======================

With the metadata declared, we can now ask Setuptools to generate
*distribution packages*, which are archives containing files to be installed
on the target machine.


Build the distributions
=======================

Use the following command to build distributions::

    python3 setup.py sdist bdist_wheel

This command should output a lot of text. Once completed, it should generate
two files in the dist directory::

    dist/
        sampleproject_YOUR_USERNAME-0.0.1-py3-non3-any.whl
        sampleproject_YOUR_USERNAME-0.0.1.tar.gz

The ``tar.gz`` file is a *source distribution* (sdist), and the ``.whl`` file
is a *built distribution* in the *wheel* format. Newer pip versions
prefer to install built distributions, but will fall back to sdist if there are
no built distributions compatible with the user's platform. In this case, our
example package is compatible with Python on any platform, so only one built
distribution is needed.


Upload the distributions
========================

Now we can upload the files to the package index. For demostration purposes, we
will be uploading to *Test PyPI*. This is a separate instance of the package
index, intended for testing and experimentation. This is great for things like
this tutorial, where we don't necessarily want to upload "for real."

Make sure to :ref:`test-pypi-register` before you continue with the tutorial.

.. note::

    All of the instructions below will assume you are using Test PyPI.
    Substitute ``test.pypi.org`` with ``pypi.org`` (i.e. remove the ``test.``
    part) when you want to actually upload an package to the public.

Use the following command to upload the distributions built in the previous
section::

    python3 -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*

Enter your username and password when prompted.

Once the command finished successfully, your package should be viewable on
Test PyPI at e.g. https://test.pypi.org/project/sampleproject-YOUR-USERNAME.
