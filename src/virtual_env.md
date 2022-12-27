# Using a Virtual Environment

Virtual environments are a common tool in Python development for dependency management.  The developer community uses a plethora of user-defined packages to provide functionality and options that extend beyond those in the standard library.  By default Python installs these third-party libraries into the same site-packages directory.  As summarized in [Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/), installing all third-party packages into a common directory can lead to the following issues:

- Reproducibility
  - A package may require specific versions of support libraries to run, and the same combination of libraries installed with different versions on a new machine may be unable to run the package.
- System Pollution
  - Linux and MacOS systems come with a version of Python pre-installed, and third-party packages can cause unexpected side-effects on the operating system's normal behavior.
- Dependency Conflicts
  - Packages installed for unrelated projects can rely on different versions of third-party packages as dependencies.  There may not be a single version of the required library that can support and run both packages, creating a dependency conflict.

## Creating a Virtual Environment

The use of virtual environments in Python is so ubiquitous that Python now includes virtual environment support in its standard library through the `venv` package.  While there are third-party libraries such as `virtualenv` and `conda` that can create virtual environments, and may be desirable for certain use applications, we recommend using the built-in support of the `venv` package, and this is the method we have used in developing the Python packages in the Grants Pass code repository.

The command to create a virtual environment from the command-line prompt is:

```{PS}
python -m venv {name}
```

Substitute {name} for the desired name of the virtual environment.  For example, I have a generic test environment on my machine creatively named 'test':

```{PS}
python -m venv test
```

I could also name the environment after a specific project or my job title:

```{PS}
python -m venv my_project
python -m venv technician
```

If you wish to overwrite an old test environment (deleting any packages installed into it), add the flag '--clear':

```{PS}
python -m venv test --clear
```

The computer stores the information related to the virtual environment in an eponymous folder located in the working directory.  Some users prefer to create the virtual environment in the working directory of specific projects, while other users prefer to create a dedicated folder for various virtual environments.  You can delete a virtual environment from your system by deleting this folder.

Note that the system path needs to include the location of the Python executable for these commands to work on your machine.  When installing Python, you can check the box to automatically add the Python executable to your system path, or you can manually add it by modifying the path in the system environmental variables.  On a Windows machine, you can type the Windows key and enter 'environmental variables' into the search bar, and select 'Edit the system environmental variables' from the Control Panel.  Select the 'path' variable and click on 'Edit'.  Unless you have specified a different installation directory, the path to the Python executable should be 'C:/Users/username/AppData/Local/Programs/Python/Python310/'.  On my machine the path looks like this: 'C:\Users\erose\AppData\Local\Programs\Python\Python310\'.  If the Python executable is not in your system path, you can create a virtual environment by specifying the path manually, so on my machine I could enter:

```{PS}
C:\Users\erose\AppData\Local\Programs\Python\Python310\python -m venv test
```

