====================
Describe the project
====================

Create some additional files in the project root directory, alongside the
``sample`` directory. You should end up with the following structure::

    sampleproject-YOUR-USERNAME/
        sample/
            __init__.py
        pyproject.toml
        README.md
        setup.cfg
        setup.py


Creating README.md
==================

A README file is essential for people (including yourself in the future) to
understand what the project is doing. You can put some text inside this file to
describe the project, using the `GitHub-flavored Markdown`_ syntax. Put in the
following content if you are not sure what to write:

.. code:: markdown

    # Example Package

    This is a simple example package. You can use
    GitHub-flavored Markdown to write your content.


.. _`GitHub-flavored Markdown`: https://guides.github.com/features/mastering-markdown/


Creating pyproject.toml
=======================

Add the following content:

.. code:: toml

    [build-system]
    requires = ["setuptools", "wheel"]
    build-backend = "setuptools.build_meta"

This file describes how we want to package the project. We will be using
Setuptools_, a packaging tool maintained by the Python Packaging Authority
(PyPA).

.. _Setuptools: https://setuptools.readthedocs.io/en/latest/


Creating setup.cfg
==================

This file tells Setuptools about the project (such as the name and version), as
well as which code files to include.

Change the ``name`` value to include your username (for example,
``sampleproject-uranusjr``), to make the proejct name unique, and does not
conflict with other people when you upload it. Or you can use any name you like
(as long as it is not already registered---search on the PyPI_ to find out).

.. _PyPI: https://pypi.org/

.. code:: ini

    [metadata]
    name = sampleproject-YOUR-USERNAME
    version = 0.0.1
    author = Example Author
    author_email = author@example.com
    description = A small example package
    long_description = file: README.md
    long_description_content_type = text/markdown
    url = https://github.com/pypa/sampleproject
    license = MIT
    classifier =
        Programming Language :: Python :: 3
        License :: OSI Approved :: MIT License
        Operating System :: OS Independent

    [options]
    packages = find:
    python_requires = >=3.6

Here is a run-down of the configuration:

* ``name`` is the distribution name of your package. This can be any name as
  long as only contains letters, numbers, ``_``, and ``-``. It also must not
  already be taken on the PyPI. **Be sure to update this with your username**,
  as this ensures you won’t try to upload a package with the same name as one
  which already exists when you upload the package.
* ``version`` is the package version. See `PEP 440`_ for more details on
  versions.
* ``author`` and ``author_email`` are used to identify the author of the
  package.
* ``description`` is a short, one-sentence summary of the package.
* ``long_description`` is a detailed description of the package. This is
  shown on the package detail package on the PyPI. Here, we tell Setuptools to
  use the content of ``README.md``, which is a common pattern.
* ``long_description_content_type`` tells the index what type of markup is
  used for the long description. In this case, it's Markdown.
* ``url`` is the URL for the homepage of the project. For many projects, this
  will just be a link to GitHub, GitLab, Bitbucket, or similar code hosting
  service.
* ``license`` describes what license this project uses---Here we use MIT, but
  there are many more choices available. Omit this field if you do not intend
  your code to be open source.
* ``classifiers`` gives the index and pip some additional metadata about your
  package. In this case, the package described as

    - Only compatible with Python 3
    - Uses the MIT license
    - Does not care about operating systems

  A complete list of classifiers can be found at https://pypi.org/classifiers/.
* ``packages`` is a list of all Python code that should be included in the
  *distribution package*. Instead of listing each package manually, we can use
  the *find derivative* to automatically discover all packages and
  subpackages. This is also a common pattern unless you have an uncommon
  project layout.
* ``python_requires`` descibes what versions of Python this project is
  compatible with. Here, we only allow the project to be installed on Python
  3.6 or later.

The keys listed above is a relatively minimal set, and there a a few more you
can specify. Visit the `documentation on setup.cfg`_ to find a comprehensive
list of available configurations.

.. _`PEP 440`: https://www.python.org/dev/peps/pep-0440/
.. _`documentation on setup.cfg`: https://setuptools.readthedocs.io/en/latest/setuptools.html#configuring-setup-using-setup-cfg-files


Creating setup.py
=================

``setup.py`` is a script to call Setuptools. It can be used to include custom
logic to build the project, but we are using all defaults here. Simply put:

.. code:: python

    import setuptools
    setuptools.setup()
