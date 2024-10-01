# Using a Virtual Environment

Virtual environments are a common tool in Python development for dependency management.  
The developer community uses a plethora of user-defined packages to provide functionality and options that extend beyond those in the standard library.  
By default Python installs these third-party libraries into the same site-packages directory.  
As summarized in [Python Virtual Environments: A Primer](https://realpython.com/python-virtual-environments-a-primer/), installing all third-party packages into a common directory can lead to the following issues:

- Reproducibility
  - A package may require specific versions of support libraries to run, and the same combination of libraries installed with different versions on a new machine may be unable to run the package.
- System Pollution
  - Linux and MacOS systems come with a version of Python pre-installed, and third-party packages can cause unexpected side-effects on the operating system's normal behavior.
- Dependency Conflicts
  - Packages installed for unrelated projects can rely on different versions of third-party packages as dependencies. There may not be a single version of the required library that can support and run both packages, creating a dependency conflict.

The `arcgis` package for Python caused a particularly problematic system pollution problem for me at my previous job in county government.
I had tried and failed to install the package on my machine, where the error message informed me there was a problem with the `ca-certificates` package.
The problem is that the system used `ca-certificates` to perform any and all Python operations, and this package had become corrupted by my attempted install of `arcgis`.
I could no longer use Python at all on this machine.
I did not have administrative privileges to install programs on this machine, and so IT had to send staff over to my building to help me uninstall and reinstall Python, which did not resolve the issue, much to our surprise.
At the county, our IT staff did not have experience developing in Python, and the situation is no different here at Grants Pass.
I ended up having to switch to a different (and less performant) machine.
With a virtual environment, the problem is contained to the virtual environment, so when I encountered this problem again on my new machine (and I did), I could simply delete the corrupted environment and start again.
Take a lesson from my hard-earned experience and use virtual environments for Python development like you would a crash helmet on a motorcycle.

## Creating a Virtual Environment

The use of virtual environments in Python is so ubiquitous that Python now includes virtual environment support in its standard library through the `venv` package. While there are third-party libraries such as `virtualenv` and `conda` that can create virtual environments, and may be desirable for certain use applications, we recommend using the built-in support of the `venv` package, and this is the method we have used in developing the Python packages in the Grants Pass code repository.

The command to create a virtual environment from the command-line prompt is:

```{bash}
python -m venv {name}
```

Substitute {name} for the desired name of the virtual environment. For example, I have a generic test environment on my machine creatively named 'test':

```{bash}
python -m venv test
```

I could also name the environment after a specific project or my job title:

```{bash}
python -m venv my_project
python -m venv technician
```

If you wish to overwrite an old virtual environment (deleting any packages installed into it), add the flag '--clear':

```{bash}
python -m venv test --clear
```

The computer stores the information related to the virtual environment in an eponymous folder located in the working directory. Some users prefer to create the virtual environment in the working directory of specific projects, while other users prefer to create a dedicated folder for various virtual environments. You can delete a virtual environment from your system by deleting this folder.

Note that the system path needs to include the location of the Python executable for these commands to work on your machine.
When installing Python, you can check the box to automatically add the Python executable to your system path, or you can manually add it by modifying the path in the system environmental variables.
On a Windows machine, you can type the Windows key and enter 'environmental variables' into the search bar, and select 'Edit the system environmental variables' from the Control Panel.
Select the 'path' variable and click on 'Edit'.
Unless you have specified a different installation directory, the path to the Python executable should be 'C:/Users/username/AppData/Local/Programs/Python/Python310/'.
On my machine the path looks like this: 'C:\Users\erose\AppData\Local\Programs\Python\Python310\'.
If the Python executable is not in your system path, you can create a virtual environment by specifying the path manually, so on my machine I could enter:

```{bash}
C:\Users\erose\AppData\Local\Programs\Python\Python310\python -m venv test
```

## Activating the Virtual Environment

You can create multiple virtual environments on your machine, but before you begin installing packages, you have to direct the processor to spool up the virtual environment that you want to use.
Inside the folder named after your environment, there is a sub-folder called `Scripts` that contain a number of executables, and a pair of files called `activate` and `deactivate`.
To start up a virtual environment, you call the activate script.
If your working directory contains the virtual environment folder, you can use the relative path to call this script, using the command:

```{bash}
{name}/Scripts/activate
```

So if the virtual environment is called 'test', and your working directory contains the folder 'test' where the virtual environment is stored on your machine, then you can run the command:

```{bash}
test/Scripts/activate
```

I keep my repository code in a 'repos' folder, and my virtual environments in an 'envs' folder, so I can activate the environment from my home directory and navigate to the repo of interest:

```{bash}
cd c:/users/erose
envs/test/Scripts/activate
cd repos/webmap
```

Or I can activate the environment from within the code directory using a relative path:

```{bash}
cd c:/users/erose/repos/webmap
../../envs/test/Scripts/activate
```

Declaring the full path does not work on my Windows machine from Powershell. I could not say why.

```{bash}
# does not work
cd p:/repos/webmap
c:/users/erose/envs/test/Scripts/activate
```

Note that many online tutorials will direct you to use the `source` keyword to call the activation script, but this only applies to Linux and MacOS development environments. Using Powershell on Windows, this will not work:

```{bash}
# does not work
cd c:/users/erose/envs
source test/Scripts/activate
```

Calling `source` on Windows in Powershell produces the following error: _"The term 'source' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again."_

When the virtual environment is active, the name of the environment will appear in parenthesis before the `PS` in the prompt:

```{bash}
# virtual environment not active
PS c:\> cd c:/users/erose/envs
PS c:\users\erose\envs> test/Scripts/activate
# virtual environment active
(test) PS c:\users\erose\envs>
```

To leave the virtual environment, you can call the deactivate script:

```{bash}
{name}/Scripts/deactivate
```

Using the previous example:

```{bash}
# virtual environment active
(test) PS c:\users\erose\envs> test/Scripts/deactivate
# virtual environment not active
PS c:\users\erose\envs>
```

The virtual environment will also deactivate if you close the terminal, stopping the running instance of Powershell. So feel free to simply exit or shutdown when you are done.
