# Linux Commands Quick Reference

**date** : Display the system date and time

**cal** : Displays a calendar

**df** : Report file system disk space usage

**free** : Display amount of free and used memory in the system

**exit** : End a terminal session

## Navigation Commands

**pwd** : Print working directory

**cd directory_name** : Change to the specified directory **directory_name**

**cd** : Changes the working directory to your home directory
  
**cd -** : Changes the working directory to the previous working directory

**cd ~user_name** : Changes the working directory to the home directory of user_name

## Exploring The System

**file file_name** : Determine file type of **file_name**

**less file_name** : View contents of file **file_name** 

***

**ls** : List files and subdirectories contained in the current working directory

**ls directory_name** : List files and subdirectories contained in the specified **directory_name**

**ls -l** : List directory contents in long format

**ls -lt** : List directory contents in long format and sort the result by the file's modification time

**ls -lt** : List directory contents in long format and sort the result by the file's modification time in reverse order

**ls -ld */** : list directory in long format with directories only

**ls -lF** : list directory in long format, append an indicator character to the end of each listed name. For example, a “/” if the name is a directory.

**ls -lh** : list directory in long format, display file sizes in human readable format rather than in bytes.

**ls -lhS** : list directory in long format, sort by file size

**ls -lhSr** : list directory in long format, sort by file size in reverse order

**ls -l *** : list all the files

**ls -l o*** : Any file beginning with "o"

**ls -l t*.csv** : Any file beginning with “t” followed by any characters and ending with ".csv"

**ls -l AIG_???.dat** : Any file beginning with “AIG_” followed by exactly three characters

**ls -l [At3]*** : Any file beginning with either an “A”, “t”, or  “3”

**ls -l AIG_[0-9][0-9][0-9].DAT** : 	Any file beginning with “AIG_” followed by exactly three numerals and ending with “.dat”

**ls -l [[:upper:]]*** :  	Any file beginning with an uppercase letter

**ls -l [![:digit:]]*** : Any file not beginning with a numeral

**s -l [[:digit:]]*** :  Any file beginning with a numeral

**ls -l *[[:lower:]0123]** :  	Any file ending with a lowercase letter or the numerals “0” or “1” or “2” or “3”


***

## Manipulating Files And Directories


***

**mkdir** : Create directories

***

**mkdir zikzak_dir_01** : Make directory zikzak_dir_01

**mkdir zikzak_dir_01 zikzak_dir_02 zikzak_dir_03** : Make multiple directories

**mkdir -m 777 zikzak_dir_04** : Make directory and Set file permissions

**mkdir -p letscodeit/zikzak_dir_06/data/in** : Make entire hierarchy of directories


***

**cp** : Copy files and directories

***

**cp item1 item2** : Copy the single file or directory “item1” to file or directory “item2”

**cp file1 file2 file3 dir1** " Copy file1, file2, file3 into directory dir1

**cp file1 file2** : Copy file1 to file2. If file2 exists, it is overwritten with the contents of file1. If file2 does not exist, it is created.

**cp -i file1 file2** : Same as above, except that if file2 exists, the user is prompted before it is overwritten.

**cp dir1/* dir2** : Using a wildcard, all the files in dir1 are copied into dir2. dir2 must already exist.

**cp -r dir1 dir2** : Copy the contents of directory dir1 to directory dir2.

***

**mv** : Move/rename files and directories

***

**mv file1 file2** : Rename file1 as file2. If file2 already exists, it will be overwritten

**mv -i file1 file2** : Same as above, except that if file2 exists, the user is prompted before it is overwritten

**mv file1 file2 dir1** : Move file1 and file2 into directory dir1. dir1 must already exist.

**mv dir1 dir2** : Rename dir1 as dir2. If dir2 already exists, move dir1 into dir2


***

**rm** : Remove files and directories

***

**rm file1** : Delete file1 

**rm -i file1** : Delete file1 in interactive mode

**rm -r file1 dir1** : Delete file1 and dir1 and its contents recursively

**rm -rf file1 dir1** : Same as above, except that if either file1 or dir1 do not exist, rm will continue silently.

***

**ln** : Create hard and symbolic links

***

**ln file link** : Create hard link

**ln -s file link** : Create symbolic link

Note :

1. A hard link cannot reference a file outside its own file system. i.e., hard links cannot span physical devices

2. A hard link may not reference a directory.

3. A symbolic link may reference a directory or a file.

4. If you write some something to the symbolic link, the referenced file is also written to

5. In symbolic links most file operations are carried out on the link's target, not the link itself. rm is an exception.

6. When you delete a symbolic link, only the link is deleted, not the file itself

7. If the file is deleted before the symbolic link, the link will continue to exist, but will point to nothing

***

## Working with Commands

***

**type** – Indicate how a command name is interpreted

***

Command can be one of the four different things. 

1. An executable program

2. A command built in to shell

3. A shell function

4. An alias


The type command is a shell builtin that displays the kind of command the shell will execute, given a particular command name.


$ **type cd**

cd is a shell builtin

$ **type alias**

alias is a shell builtin

$ **type ls**

ls is /bin/ls

***

**which** – Display which executable program will be executed

***

$ **which ls**

/bin/ls

which only works for executable programs, not shell builtins not aliases

***
##### Getting A Command's Documentation
***

**help command_name** : Display the built-in help for the given command

**man command_name** – Display a command's manual page

**apropos search_term** – Display a list of appropriate commands whose man pages contain the **search_term**

**info** – Display a command's info entry

**whatis command_name** – Display a very brief description of a command

***

**alias alias_name='command_string'** – Create an alias **alias_name** for a command **command_string**

**unalias alias_name** – Remove an alias **alias_name**

**alias** : See all the alias defined in that environment

***

## I/O Re-direction

***

cat - Concatenate files

sort - Sort lines of text

uniq - Report or omit repeated lines

grep - Print lines matching a pattern

wc - Print newline, word, and byte counts for each file

head - Output the first part of a file

tail - Output the last part of a file

tee - Read from standard input and write to standard output and files

***

	file descriptor for standard input stream : 0>

	file descriptor for standard output stream : 1>

	file descriptor for standard error stream : 2>

**Redirecting Standard Output to a File :** ls -l /bin/usr > ls-output.txt *(overwrites if the file is already present)*

**Redirecting Standard Output to a File :** ls -l /bin/usr >> ls-output.txt *(appends if the file is already present)*

**Redirecting Standard Error to a File :** ls -l /bin/usr 2> ls-error.txt *(overwrites if the file is already present)*

**Redirecting Standard Error to a File :** ls -l /bin/usr 2>> ls-error.txt *(appends if the file is already present)*

**Redirecting both Standard Output And Standard Error To One File example 1 :** ls -l /bin/usr > ls-output.txt 2>&1

- First we redirect standard output to the file ls-output.txt

- then we redirect file descriptor two (standard error) to file descriptor one (standard output) using the notation 2>&1

**Redirecting both Standard Output And Standard Error To One File example 2 :** ls -l /bin/usr &> ls-output.txt

**Suppressing error messages :** ls -l /bin/usr 2> /dev/null

**Redirecting Standard Input from keyboard to File :** cat < lazy_dog.txt

***

## Command line interpretation at Shell

***

**Expansion** : With expansion, you type something and it is expanded into something else before the shell acts upon it

**Pathname Expansion** : The mechanism by which wildcards work is called pathname expansion

**Tilde Expansion** : When used at the beginning of a word, it expands into the home directory of current user

**Arithmetic Expansion** : The shell allows arithmetic to be performed by expansion. e.g., echo $((2 + 2))

**Brace Expansion** : you can create multiple text strings from a pattern containing braces

	$ echo Front-{A,B,C}-Back
	Front-A-Back Front-B-Back Front-C-Back
	
	$ echo Number_{1..5}
	Number_1 Number_2 Number_3 Number_4 Number_5
	
	$ echo {Z..A}
	Z Y X W V U T S R Q P O N M L K J I H G F E D C B A
	
**Parameter Expansion** : Shell will expand the variable in the Command line before the command execution.

	$ echo $USER
	zikzak

**Command Substitution** : Command substitution allows us to use the output of a command as an expansion:

	$ ls -l $(which cp)
	-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp

**Quoting** : The shell provides a mechanism called quoting to selectively suppress unwanted expansions

**Double Quotes** : all the special characters used by the shell lose their special meaning and are treated as ordinary characters. The exceptions are “$”, “\” (backslash), and “`” (backquote). This means that word-splitting, pathname expansion, tilde expansion, and brace expansion are suppressed, but parameter expansion, arithmetic expansion, and command substitution are still carried out.

**Single Quotes**: If we need to suppress all expansions, we use single quotes.

***

## Permissions

***

**id** – Display user identity

**chmod** – Change a file's mode

**umask** – Set the default file permissions

**su** – Run a shell as another user

**sudo** – Execute a command as another user

**chown** – Change a file's owner

**chgrp** – Change a file's group ownership

**passwd** – Change a user's password

***

## Processes

***

**ps** – Report a snapshot of current processes

**top** – Display tasks

**jobs** – List active jobs

**bg** – Place a job in the background

**fg** – Place a job in the foreground

**kill** – Send a signal to a process

**killall** – Kill processes by name

**shutdown** – Shutdown or reboot the system

***

## The Environment

***

**printenv** – Print part or all of the environment

**set** – Set shell options

**export** – Export environment to subsequently executed programs

**alias** – Create an alias for a command


***

## Package Management - Red Hat Style

***

**Distributions** - Fedora, RHEL, CentOS 

**Low-Level Tools** - rpm

**High-Level Tools** - yum


###Common Package Management Tasks

**yum search search_string** - Finding A Package In A Repository

**yum install package_name** - Installing A Package From A Repository

**yum erase package_name** - Removing A Package

**yum update** - Updating Packages From A Repository 

**yum info package_name** - Displaying Info About An Installed Package

**rpm -i package_file** - Installing A Package From A Package File

**rpm -U package_file** - Upgrading A Package From A Package File

**rpm -q package_name** - Determining If A Package Is Installed

**rpm -qa** - Listing Installed Packages
 
 **rpm -qf file_name** - Finding Which Package Installed A File
 
 
***
**I am reading :** The Linux Command Line by William E. Shotts, Jr.
***