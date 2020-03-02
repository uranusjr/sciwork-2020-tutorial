==========================
Distribute a Conda Package
==========================

As with Setuptools, we also need to provide both some *description* and
*build instruction* for a Conda package. More specifically, three files are
needed:

* ``meta.yaml``
* ``build.sh``
* ``blt.bat``

Put them in the project root (alongside with other metadata files such as
``README.md``, ``pyproject.toml``).


Creating ``meta.yaml``
======================

This is used to describe the package.

.. code:: yaml

    package:
      name: sampleproject-YOUR-USERNAME
      version: "0.0.1"
    about:
      home: https://github.com/pypa/sampleproject
      license: MIT
      summary: A small example package
    source:
      fn: sampleproject-YOUR-USERNAME-0.0.1.tar.gz
      url: https://test.pypi.org/packages/source/s/sampleproject-YOUR-USERNAME/sampleproject-YOUR-USERNAME-0.0.1.tar.gz
      md5: "39180d64b5021c5399a2568fe2103cd2"

    requirements:
      build:
        - pip >=19
        - python >=3.6
      run:
        - python >=3.6

.. note::

    Remember to replace ``YOUR-USERNAME`` with your own name.

.. warning::

    Make sure to quote the ``version`` and ``md5`` fields! Otherwise YAML may
    interpret them as numbers. Also, the extension is ``yaml``, not ``yml``.

Here, we instruct Conda about basic project information (``package`` and
``about`` sections), where to download it (``source``), and what other packages
are needed in order to build and run it.

Unlike PyPI, Conda does not allow uploading source code (only built files), so
you need to upload your code somewhere else, and use ``meta.yaml`` to tell
Conda where it is.

Here, we are re-using our data on Test PyPI (or the real PyPI, if you
eventually release the package to the public). The package URL is predictable,
and based on your package name (the first ``/s/`` part is the package name's
first letter).

The MD5 value is used by Conda to make sure it downloads the correct file. It
can be calculated using a local command.

On Windows::

    fciv -md5 dist\sampleproject-YOUR-USERNAME-0.0.1.tar.gz

On macOS::

    md5 dist/sampleproject-YOUR-USERNAME-0.0.1.tar.gz

On Linux::

    md5sum dist/sampleproject-YOUR-USERNAME-0.0.1.tar.gz

Alternatively, you can also view this on your PyPI project page at
https://test.pypi.org/project/sampleproject-YOUR-USERNAME/#files. Click on the
**View** button beside the ``.tar.gz`` file, and copy the hash digest field on
the **MD5** row.


Creating build scripts
======================

Conda packages use two files to build: ``build.sh`` and ``bld.bat``. These two
are basically the same thing, but one for installing on Windows, and one for on
Linux and macOS. It is highly recommended you provide *both* if possible
(unless you really don't want the package to be installed on a platform).

``build.sh``:

.. code:: bash

    "$PYTHON" -m pip install --no-deps .

``bld.bat``:

.. code:: bat

    "%PYTHON%" -m pip install --no-deps .
    exit %errorlevel%


Building the package
====================

In the project root (where ``meta.yaml`` is), use ``conda-build`` to generate a
Conda package::

    conda build .

This will generates a lot of text. When it finished, you should see something
like the following near the end::

    TEST START: ~/miniconda/conda-bld/linux-64/sampleproject-YOUR-USERNAME-0.0.1-py38_0.tar.bz2
    Nothing to test for: ~/miniconda/conda-bld/linux-64/sampleproject-YOUR-USERNAME-0.0.1-py38_0.tar.bz2
    # Automatic uploading is disabled
    # If you want to upload package(s) to anaconda.org later, type:

    anaconda upload ~/miniconda/conda-bld/linux-64/sampleproject-YOUR-USERNAME-0.0.1-py38_0.tar.bz2

This means that the package has been built successfully. The ``TEST START`` and
``anaconda upload`` lines also shows the location of the package; in this case
it is::

    ~/miniconda/conda-bld/linux-64/sampleproject-YOUR-USERNAME-0.0.1-py38_0.tar.bz2

Save this path somewhere; it will be useful in the following (optional)
sections.


Testing the package
===================

You can try installing the newly built package into your Conda environment::

    conda install --use-local sampleproject-YOUR-USERNAME

The ``--use-local`` flag instructs Conda to install the local conda-build
channel on your computer, rather than the default Anaconda or conda-forge.

If installed successfully, the package will be present in ``conda list``.


Optional: Building for a different Python version
=================================================

The package built above was against Python 3.8 (the file name contains a
``py38`` part). Conda by default builds packages for the version of Python
installed in the root environment. To build packages for other versions of
Python, use the ``--python`` flag followed by a version::

    conda build --python 3.6 sampleproject-YOUR-USERNAME

Notice that the file printed at the end of the output would change to reflect
the requested version of Python. When you ``conda install``, it will look in
the package directory for the file that matches your current Python version.


Optional: Converting a package for use on all platforms
=======================================================

Similar to the Python version, Conda by default requires you to build the
package on each platform, to make sure the uploaded files are always correctly
built. We built against ``linux-64`` (Linux, 64-bit) in the above example.
Sometimes, however, you are *very* sure the package works on all platforms.
Conda can convert the package for you in this case::

    conda convert --platform all ~/miniconda/conda-bld/linux-64/sampleproject-YOUR-USERNAME-0.0.1-py38_0.tar.bz2

Replace the final path with your package location saved above.


Optional: Uploading to Anaconda.org
===================================

After converting your files for use on other platforms, you may choose to
upload your files to `Anaconda.org`_. You will need to register an account
(sign up) on the website first.

.. _`Anaconda.org`: https://anaconda.org

Make sure you have the Anaconda Client installed::

    conda install anaconda-client

And log in (sign in) into your registered Anaconda account::

    anaconda login

After that, you can use the command to upload packages::

    anaconda upload ~/miniconda/conda-bld/linux-64/sampleproject-YOUR-USERNAME-0.0.1-py38_0.tar.bz2

Replace the final path with your package location saved above. Packages built
against another Python, or converted by ``conda convert`` can also be uploaded
in the same way, to make your package support multiple Python versions and
platforms.
