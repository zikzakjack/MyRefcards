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
I am reading : The Linux Command Line by William E. Shotts, Jr.
***