======================
Distribute the Project
======================

With the metadata declared, we can now ask Setuptools to generate
*distribution packages*, which are archives containing files to be installed
on the target machine.


Build the distributions
=======================

Use the following command to build distributions::

    py -3 setup.py sdist bdist_wheel

This command should output a lot of text. Once completed, it should generate
two files in the dist directory::

    dist/
        sampleproject_YOUR_USERNAME-0.0.1-py3-non3-any.whl
        sampleproject-YOUR-USERNAME-0.0.1.tar.gz

The ``tar.gz`` file is a *source distribution* (sdist), and the ``.whl`` file
is a *built distribution* in the *wheel* format. Newer pip versions
prefer to install built distributions, but will fall back to sdist if there are
no built distributions compatible with the user's platform. In this case, our
example package is compatible with Python on any platform, so only one built
distribution is needed.

.. warning::

    If you made mistakes in your ``setup.cfg`` and want to change it, make sure
    to *delete previously-generated metadata* before running ``setup.py`` again.

    On Windows::

        rmdir /q /s build dist
        del sampleproject_YOUR_USERNAME.egg-info

    On macOS and Linux::

        rm -rf build dist sampleproject_YOUR_USERNAME.egg-info


Upload the distributions
========================

Now we can upload the files to the package index. For demostration purposes, we
will be uploading to *Test PyPI*. This is a separate instance of the package
index, intended for testing and experimentation. This is great for things like
this tutorial, where we don't necessarily want to upload "for real."

Make sure to :ref:`test-pypi-register` before you continue with the tutorial.

Use the following command to upload the distributions built in the previous
section::

    py -3 -m twine upload --repository-url https://test.pypi.org/legacy/ dist/*

Enter your username and password when prompted.

Once the command finished successfully, your package should be viewable on
Test PyPI at e.g. https://test.pypi.org/project/sampleproject-YOUR-USERNAME.

Congratulations, you have successfully packaged and distributed a Python
project!


Test package installation
=========================

The package uploaded to Test PyPI can be installed with pip, like you would any
other package, by explicitly specifying the "index" to install from::

    py -3 -m pip install --index-url https://test.pypi.org/simple sampleproject-YOUR-USERNAME

Now try to use it by running ``py -3``:

.. code:: pycon

    >>> import sample
    >>> sample.greet()
    Hello!


Optional: Release your package to PyPI.org
==========================================

By uploading the package to PyPI.org (instead of Test PyPI), you are telling
the world the package is ready for download. The steps are simple---Register an
accout on `PyPI.org`_, build the distributions like before, and change the
repository URL in the upload command::

    py -3 -m twine upload --repository-url https://pypi.org/legacy/ dist/*

.. _`PyPI.org`: https://pypi.org

The only difference is to use ``pypi.org`` (removing the ``test.`` part).
That's it! Now people can install your package directly::

    py -3 -m pip install sampleproject-YOUR-USERNAME

There are some caveats though:

* Files uploaded to PyPI are immutable. More especifically, although deletion
  is possible, your cannot *re-upload* a file. So be extra careful before you
  release to PyPI. The only way to override a mistake on PyPI is to release a
  new version.
* Following the previous point, it is usually a good idea to delete the
  ``build``, ``dist``, and ``.egg-info`` directories every time you want to
  release a new version, to make sure the files are all in the newest version.
* Accounts and packages on Test PyPI and (real) PyPI are all distinct. You do
  not automatically own a package on PyPI by uploading it to Test PyPI, and
  vice versa.
