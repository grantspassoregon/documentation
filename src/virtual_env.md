# Using a Virtual Environment

Virtual environments are a common tool in Python development for dependency management.  The developer community uses a plethora of user-defined packages to provide functionality and options that extend beyond those in the standard library.  By default Python installs these third-party libraries into the same site-packages directory.  As summarized in [Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/), installing all third-party packages into a common directory can lead to the following issues:

- Reproducibility
  - A package may require specific versions of support libraries to run, and the same combination of libraries installed with different versions on a new machine may be unable to run the package.
- System Pollution
  - Linux and MacOS systems come with a version of Python pre-installed, and third-party packages can cause unexpected side-effects on the operating system's normal behavior.
- Dependency Conflicts
  - Packages installed for unrelated projects can rely on different versions of third-party packages as dependencies.  There may not be a single version of the required library that can support and run both packages, creating a dependency conflict.

The use of virtual environments in Python is so ubiquitous that Python now includes virtual environment support in its standard library through the `venv` package.
