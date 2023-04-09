## Alias
#alias
- Alias are shortcuts to repeatedly running commands
- to list all alias run `alias` command
- To create a new alias `alias alias_name='command to add'` example `alias lt='ls -lts'`.
- Alias will not persist outside session.
- To persist an alias at it to `bash_profile` or `.bashrc`
- To remove an alias in current session use `unalias <alias_name>` to remove permanent remove it from `.bashrc` or `bash_profile`

## What is shell?
#shell
- A command interpreter or an interface interface between user and kernel
- Shell gets started when a user logs in and starts a terminal.
- To identify the shell you are working on `echo $0` or `echo $SHELL`
- To see list of shells available for a user `cat /etc/shells`
- To change the default shell for a user `chsh -s /bin/bash`
- To identify the shell for a user `cat /etc/passwd`

## What is shell script?
#shell_script
- An executable text file containing shell commands which are executed in order.
- Generally used for automating repeated tasks.
- Common tasks that are done with shell scripts
	- Monitoring system
	- Data backup and restoring
	- Creating an alert system
	- User administration
	- Security Auditing

**Example Shell Script:**
- create a folder to create all the scripts.
- We can create a shell scripts as `vim first_script.sh` this will open a vi editor
- add the following by clicking `i` for inserting.

```sh
mkdir -p dir-001
echo "Initial text from a shellscript" > dir-001/file.txt
tree .
cat dir-001/file.txt
```

- To exist out of vi press escape then `:wq!` and hit enter
- Add execution permission by using `chmod 700 first_script.sh`
- To execute the script `./first_script.sh`
- To give execution permission to all users use `chmod +x firat_script.sh`

- To allow all the execution of the scripts in ~/scripts folder. Add it to path.
- For adding the path to scripts follow the below steps
	- Add `export PATH="$PATH:~/scripts"` at end of the `.bashrc` folder
	- To reload the file use `source ~/.bashrc`
	- Now the scripts in `~/scripts` folder can be executed with just the name without prepending `~/` at the start.

### Adding the interpreter
- To add an interpreter to any script `#!` 
- Default interpreter is bash, so if non of the interpreter is mentioned bash will take over
- To explicitly mention the interpreter add the path to interpreter

Example:
```sh
#!/bin/bash
mkdir -p dir-001
echo "Initial text from a shellscript" > dir-001/file.txt
tree .
cat dir-001/file.txt
```

To add python for example 
```sh
#!/usr/bin/python3
import sys
print(sys.version)
```

> For adding comment in shell scripts add `#` at the start of line
> For multiline comments add single line comment one after another. 

In vim editor to display line numbers use `:set nu` to remove them `:set nonu`. To make this setting permanent add a `set nu` to `~/vimrc`.  #vimrc

### Different ways to execute shell script
- `./script_name.sh`
- `. script_name.sh`
- `source script_name.sh`
- `bash script_name.sh`

Except source command, all other ways will open a secondary shell to execute the commands.

## Variables
- A variable is a memory location where a value is store, it can be manipulated later, example `IP="10.90.90.90"`
- No data types in shell, only integers and string
	- age=30
	- message="this is a message"
- To get the value use `$` at the beginning of the variable name eg: `echo $age`
- To see all variables run `set`, to check for a specify variable `set | grep age`
- To remove a variable `unset <variable_name>`
- To set a variable as read-only `declare -r varibale_name=variable_value` eg: `declare -r LOGDIR=/var/log`,  the value can be used in other scripts like `ls $LOGDIR` #read-only-variables

### variable naming conventions
- use lowercase or `__` alone in variable names
- Use capital case letter and `__` for environment vars and constants
- Variable names should be descriptive
- Variable names cannot start with numbers or special characters
- The only allowed special character is `__`

### Assigning and expansion or substitution
- Once after assigning a variable we can us it by wrapping a curly brace, when substitution is required. Eg: 
```sh
os=windows
echo ${os}11
# prints windows11
echo $os11 # will not print anything to it
```

**Quoting:**
- single quote is used to remove the  special meaning on special characters
- Double quotes are used when multi word strings are used including special characters and variable substitution.
- To use special characters such a coma, forward slash `\` is used as escape character. 

```sh
echo 'alpha\\beta'
echo "alpha\\beta"
age=10
echo "alpha is $age"
```

<!-- Learning: Zerotomastery -Bash Scripting Learn Shell Scripting: lesson 12>