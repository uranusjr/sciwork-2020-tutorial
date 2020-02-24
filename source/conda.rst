==========================
Distribute a Conda Package
==========================

Like how a Setuptools package is described by ``setup.cfg``, a Conda package
is described by a ``meta.yaml``. Create this file in the project root
(alongside with other files like ``README.md``, ``pyproject.toml``, etc.):

.. code:: yaml

    package:
      name: "sampleproject-YOUR-USERNAME"
      version: "0.0.1"
    requirements:
      build:
        - python
        - setuptools
      run:
        - python
    about:
      home: https://github.com/pypa/sampleproject

Conda packages use two files to build.

``build.sh`` (for Mac and Linux):

.. code:: bash

    $PYTHON setup.py install

``bld.bat`` (for Windows):

.. code:: bat

    "%PYTHON%" setup.py install
    if errorlevel 1 exit 1
