Environment variables or ENVs basically define the behavior of the environment. They can affect the ongoing processes or programs executed in the environment. Every Linux process has an associated set of environment variables that influence its behavior and interactions with other processes.

## Accessing Environment Variables

In Linux, environment variables are typically accessed through the shell. The shell is a command-line interface that interprets and executes commands entered by the user. It provides a way to set, modify, and retrieve environment variables. The most common shell in Linux is the Bash shell (Bourne Again SHell), which is the default shell for many distributions.
Scope of an environment variable

The scope of any variable is the region from which it can be accessed or over which it is defined. An environment variable in Linux can have global or local scope.  

# Global

A globally scoped ENV that is defined in a terminal can be accessed from anywhere in that particular environment that exists in the terminal. That means it can be used in all kinds of scripts, programs, or processes running in the environment bound by that terminal. 

# Local

A locally scoped ENV that is defined in a terminal cannot be accessed by any program or process running in the terminal. It can only be accessed by the terminal (in which it was defined) itself. 

## How to access ENVs?
Syntax:
```bash
 $NAME
```
NOTE: Both local and global environment variables are accessed in the same way.  

## How to display ENVs?
#### To display any ENV

Syntax:
```bash
 $ echo $NAME 
```
To display all the Linux ENVs

```bash
$ printenv //displays all the global ENVs
or
$ set //display all the ENVs(global as well as local)
or
$ env //display all the global ENVs
```
### Example: 

![Logo](https://media.geeksforgeeks.org/wp-content/uploads/screenshot-from-2018-12-17-22-.png)

![Logo](https://media.geeksforgeeks.org/wp-content/uploads/screenshot-from-2018-12-17-21-2-1024x537.png)

## How to set environment variables?

### To set a global ENV  
Syntax:
```bash
$ export NAME=Value
or
$ set NAME=Value
```
### Example: 
![Logo](https://media.geeksforgeeks.org/wp-content/uploads/Screenshot-from-2018-12-17-20-46-46.png)

## To set a local ENV

Syntax:  
```bash
$ NAME=Value
```

### Example: 
![Logo](https://media.geeksforgeeks.org/wp-content/uploads/Screenshot-from-2018-12-17-20-47-05.png)

### To set user wide ENVs

These variables are set and configured in ~/.bashrc, ~/.bash_profile, ~/.bash_login, ~/.profile 
files according to the requirement. These variables can be accessed by a particular user and persist through power offs. 

Following steps can be followed to do so: 

Step 1: Open the terminal. 

Step 2: 

```bash
$ sudo vi ~/.bashrc
```

Step 3: Enter password. 

Step 4: Add variable in the file opened.  
```bash
export NAME=Value
```

Step 5: Save and close the file. 

Step 6:  

```bash
$ source ~/.bashrc 
```

### Example:

![Logo](https://media.geeksforgeeks.org/wp-content/uploads/screenshot-from-2018-12-17-21-1.png)

## To set system wide ENVs

These variables are set and configured in /etc/environment, /etc/profile, /etc/profile.d/, /etc/bash.bashrc files according to the requirement. These variables can be accessed by any user and persist through power offs. 

Following steps can be followed to do so: 

Step 1: Open the terminal. 

Step 2: 

```bash
$ sudo -H vi /etc/environment
```
Step 3: Enter password. 

Step 4: Add variable in the file opened. 

```bash
NAME=Value
```
Step 5: Save and close the file. 

Step 6: Logout and Login again. 

## How to unset environment variables?

Syntax: 

```bash
$ unset NAME
or
$ NAME=''
```
## Example:  
![Logo](https://media.geeksforgeeks.org/wp-content/uploads/screenshot-from-2018-12-17-21-1.png)

Note: To unset permanent ENVs, you need to re-edit the files and remove the lines that were added while defining them.  

| Enviroment variables | Second Header |
| ---------------------|-------------- |
| $USER                |Gives search path for commands.               |
| $PATH                |Gives search path for commands.|
| $HOME                |Gives path of home directory.| 
| $PWD                 |Gives the path of present working directory.|
| $HOSTNAME            |Gives name of the host.|
| $LANG                |Gives the default system language.|
| $EDITOR              |Gives default file editor.|
| $UID                 |Gives user ID of current user.|
| $SHELL               |Gives location of current user’s shell program.|
