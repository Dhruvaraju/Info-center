## Python workspace setup
- [ ] Install Python
- [ ] Add requirments.txt
- [ ] Create a virtual Environment
- [ ] Open Virtual Environment
- [ ] Install packages in virtual env

### Python
- Navigate to https://www.python.org/downloads/
- Download and double click on executable.
- Choose defaults and install.
- Copy the location where python is installed

### Project Packages
- Create a folder with the name of project you prefer.
- Add a text document called `requirements.txt`
- List all the packages you need as strings one after another.

### Installing pyenv-win

-   pyenv is used to manage multiple versions of python in same machine
-   installation command via command prompt `pip install pyenv-win --target %USERPROFILE%\.pyenv`

**Add System Settings**

It's a easy way to use PowerShell here

Adding PYENV, PYENV_HOME and PYENV_ROOT to your Environment Variables

```
[System.Environment]::SetEnvironmentVariable('PYENV',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_ROOT',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
[System.Environment]::SetEnvironmentVariable('PYENV_HOME',$env:USERPROFILE + "\.pyenv\pyenv-win\","User")
```

Now adding the following paths to your USER PATH variable in order to access the pyenv command

```
[System.Environment]::SetEnvironmentVariable('path', $env:USERPROFILE + "\.pyenv\pyenv-win\bin;" + $env:USERPROFILE + "\.pyenv\pyenv-win\shims;" + [System.Environment]::GetEnvironmentVariable('path', "User"),"User")
```

### [](https://github.com/Dhruvaraju/python-alpha#pyenv-list-of-commands)

### pyenv list of commands

```
   commands     List all available pyenv commands
   local        Set or show the local application-specific Python version
   global       Set or show the global Python version
   shell        Set or show the shell-specific Python version
   install      Install 1 or more versions of Python
   uninstall    Uninstall 1 or more versions of Python
   update       Update the cached version DB
   rehash       Rehash pyenv shims (run this after switching Python versions)
   vname        Show the current Python version
   version      Show the current Python version and its origin
   version-name Show the current Python version
   versions     List all Python versions available to pyenv
   exec         Runs an executable by first preparing PATH so that the selected Python
   which        Display the full path to an executable
   whence       List all Python versions that contain the given executable
```

-   To set a global version of python we use `pyenv global <<version number>>` example `pyenv global 3.9.6`
-   To get list of available installations we use `pyenv install --list`

### [](https://github.com/Dhruvaraju/python-alpha#virtual-environments)

### Virtual environments

-   Used to isolate a python app with its dependencies
-   Basically binding an app with specific version of python.
-   to do it `<<complete path to python exe>> -m venv .venv`
-   example `c:/programfiles/python/python.exe -m venv .venv`
-   Or when using pyenv `pyenv exec python -m venv .venv`

### Open Virtual-environment
-   After setting virtual environment we have to activate it by using command

```
source .venv/Scripts/activate #on a linux or mac or
.venv/Scripts/activate.bat #On a windows
```

-   Now the command line will have a (.venv) before the prompt on each line.
-   with this every package that is installed will be installed in the `.venv` folder

> Additional information on virtual environments: [https://www.youtube.com/watch?v=KxvKCSwlUv8](https://www.youtube.com/watch?v=KxvKCSwlUv8)

### Installing Packages
-   Generally when we want o install dependencies we use a requirements.txt and mention the dependencies
-   For dev dependencies we use requirements-dev.txt
-   For installing those dependencies use
    -   Activate virtual environment
    -   `pip install -r requirements.txt`

**Example requirments.txt**

```
flask==1.0.1
requests>=1.1.2,<2.0.0
gunicorn
```