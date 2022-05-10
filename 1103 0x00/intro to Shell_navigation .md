pwd: print working directory
cd: change directory
ls: list files and directories in working directory
less: view text files
file: classify a file's contents

ls	: List the files in the working directory
ls /bin	: List the files in the /bin directory (or any other directory we care to specify)
ls -l	: List the files in the working directory in long format
ls -l /etc /bin	: List the files in the /bin directory and the /etc directory in long format

ls -la ..	: List all files (even ones with names beginning with a period character, which are normally hidden) in the parent of the working directory in long format

Manipulating Files
----------------------------
cp - copy files and directories
mv - move or rename files and directories
rm - remove files and directories
mkdir - create directories

These examples also point out an important concept about commands. Most commands operate like this:

command -options arguments

A Closer Look at Long Format
If we use the -l option with ls, you will get a file listing that contains a wealth of information about the files being listed. Here's an example:


-rw-------   1 me       me            576 Apr 17  2019 weather.txt
drwxr-xr-x   6 me       me           1024 Oct  9  2019 web_page
-rw-rw-r--   1 me       me         276480 Feb 11 20:41 web_site.tar
-rw-------   1 me       me           5743 Dec 16  2018 xmas_file.txt

----------     -------  -------  -------- ------------ -------------
    |             |        |         |         |             |
    |             |        |         |         |         File Name
    |             |        |         |         |
    |             |        |         |         +---  Modification Time
    |             |        |         |
    |             |        |         +-------------   Size (in bytes)
    |             |        |
    |             |        +-----------------------        Group
    |             |
    |             +--------------------------------        Owner
    |
    +----------------------------------------------   File Permissions

File Name
The name of the file or directory.
Modification Time
The last time the file was modified. If the last modification occurred more than six months in the past, the date and year are displayed. Otherwise, the time of day is shown.
Size
The size of the file in bytes.
Group
The name of the group that has file permissions in addition to the file's owner.
Owner
The name of the user who owns the file.
File Permissions
A representation of the file's access permissions. The first character is the type of file. A "-" indicates a regular (ordinary) file. A "d" indicates a directory. The second set of three characters represent the read, write, and execution rights of the file's owner. The next three represent the rights of the file's group, and the final three represent the rights granted to everybody else. We'll discuss this in more detail in a later lesson.
less
less is a program that lets us view text files. This is very handy since many of the files used to control and configure Linux are human readable.

What is "text"?
There are many ways to represent information on a computer. All methods involve defining a relationship between the information and some numbers that will be used to represent it. Computers, after all, only understand numbers and all data is converted to numeric representation.

Some of these representation systems are very complex (such as compressed multimedia files), while others are rather simple. One of the earliest and simplest is called ASCII text. ASCII (pronounced "As-Key") is short for American Standard Code for Information Interchange. This is a simple encoding scheme that was first used on Teletype machines to map keyboard characters to numbers.

Text is a simple one-to-one mapping of characters to numbers. It is very compact. Fifty characters of text translates to fifty bytes of data. Throughout a Linux system, many files are stored in text format and there are many Linux tools that work with text files. Even Windows systems recognize the importance of this format. The well-known NOTEPAD.EXE program is an editor for plain ASCII text files.

The less program is invoked by simply typing:

less text_file
This will display the file.

Controlling less
Once started, less will display the text file one page at a time. We can use the Page Up and Page Down keys to move through the text file. To exit less, we type "q". Here are some commands that less will accept:

Keyboard commands for the less program
Command	Action
Page Up or b	Scroll back one page
Page Down or space	Scroll forward one page
G	Go to the end of the text file
1G	Go to the beginning of the text file
/characters	Search forward in the text file for an occurrence of the specified characters
n	Repeat the previous search
h	Display a complete list less commands and options
q	Quit
file
As we wander around our Linux system, it is helpful to determine what kind of data a file contains before we try to view it. This is where the file command comes in. file will examine a file and tell us what kind of file it is.

To use the file program, we just type:

file name_of_file
The file program can recognize most types of files, such as:


Various kinds of files
File Type	Description	Viewable as text?
ASCII text	The name says it all	yes
Bourne-Again shell script text	A bash script	yes
ELF 64-bit LSB executable	An executable binary program	no
ELF 64-bit LSB shared object	A shared library	no
GNU tar archive	A tape archive file. A common way of storing groups of files.	no, use tar tvf to view listing.
gzip compressed data	An archive compressed with gzip	no
HTML document text	A web page	yes
JPEG image data	A compressed JPEG image	no
PostScript document text	A PostScript file	yes
Zip archive data	An archive compressed with zip	no
While it may seem that most files cannot be viewed as text, a surprising number can be. This is especially true of the important configuration files. During our adventure we will see that many features of the operating system are controlled by text configuration files and shell scripts. In Linux, there are no secrets!





Manipulating Files
This lesson will introduce the following commands:

cp - copy files and directories
mv - move or rename files and directories
rm - remove files and directories
mkdir - create directories
These four commands are among the most frequently used Linux commands. They are the basic commands for manipulating both files and directories.

Now, to be frank, some of the tasks performed by these commands are more easily done with a graphical file manager. With a file manager, you can drag and drop a file from one directory to another, cut and paste files, delete files, etc. So why use these old command line programs?

The answer is power and flexibility. While it is easy to perform simple file manipulations with a graphical file manager, complicated tasks can be easier with the command line programs. For example, how would you copy all the HTML files from one directory to another, but only copy files that did not exist in the destination directory or were newer than the versions in the destination directory? Pretty hard with with a file manager. Pretty easy with the command line:

[me@linuxbox me]$ cp -u *.html destination
Wildcards
Before we begin with our commands, we'll first look at a shell feature that makes these commands so powerful. Since the shell uses filenames so much, it provides special characters to help you rapidly specify groups of filenames. These special characters are called wildcards. Wildcards allow you to select filenames based on patterns of characters. The table below lists the wildcards and what they select:

Summary of wildcards and their meanings
Wildcard	Meaning
*	Matches any characters
?	Matches any single character
[characters]	Matches any character that is a member of the set characters. The set of characters may also be expressed as a POSIX character class such as one of the following:
POSIX Character Classes
[:alnum:]	Alphanumeric characters
[:alpha:]	Alphabetic characters
[:digit:]	Numerals
[:upper:]	Uppercase alphabetic characters
[:lower:]	Lowercase alphabetic characters
[!characters]	Matches any character that is not a member of the set characters
Using wildcards, it is possible to construct very sophisticated selection criteria for filenames. Here are some examples of patterns and what they match:

Examples of wildcard matching
Pattern	Matches
*	
All filenames

g*	
All filenames that begin with the character "g"

b*.txt	
All filenames that begin with the character "b" and end with the characters ".txt"

Data???	
Any filename that begins with the characters "Data" followed by exactly 3 more characters

[abc]*	
Any filename that begins with "a" or "b" or "c" followed by any other characters

[[:upper:]]*	
Any filename that begins with an uppercase letter. This is an example of a character class.

BACKUP.[[:digit:]][[:digit:]]	
Another example of character classes. This pattern matches any filename that begins with the characters "BACKUP." followed by exactly two numerals.

*[![:lower:]]	
Any filename that does not end with a lowercase letter.

We can use wildcards with any command that accepts filename arguments.

cp
The cp program copies files and directories. In its simplest form, it copies a single file:

[me@linuxbox me]$ cp file1 file2
It can also be used to copy multiple files (and/or directories) to a different directory:

[me@linuxbox me]$ cp file... directory
A note on notation: ... signifies that an item can be repeated one or more times.

Other useful examples of cp and its options include:

Examples of the cp command
Command	Results
cp file1 file2	Copies the contents of file1 into file2. If file2 does not exist, it is created; otherwise, file2 is silently overwritten with the contents of file1.
cp -i file1 file2	Like above however, since the "-i" (interactive) option is specified, if file2 exists, the user is prompted before it is overwritten with the contents of file1.
cp file1 dir1	Copy the contents of file1 (into a file named file1) inside of directory dir1.
cp -R dir1 dir2	Copy the contents of the directory dir1. If directory dir2 does not exist, it is created. Otherwise, it creates a directory named dir1 within directory dir2.
mv
The mv command moves or renames files and directories depending on how it is used. It will either move one or more files to a different directory, or it will rename a file or directory. To rename a file, it is used like this:

[me@linuxbox me]$ mv filename1 filename2
To move files (and/or directories) to a different directory:

[me@linuxbox me]$ mv file... directory
Examples of mv and its options include:

Examples of the mv command
Command	Results
mv file1 file2	If file2 does not exist, then file1 is renamed file2. If file2 exists, its contents are silently replaced with the contents of file1.
mv -i file1 file2	Like above however, since the "-i" (interactive) option is specified, if file2 exists, the user is prompted before it is overwritten with the contents of file1.
mv file1 file2 dir1	The files file1 and file2 are moved to directory dir1. If dir1 does not exist, mv will exit with an error.
mv dir1 dir2	If dir2 does not exist, then dir1 is renamed dir2. If dir2 exists, the directory dir1 is moved within directory dir2.
rm
The rm command removes (deletes) files and directories.

[me@linuxbox me]$ rm file...
Using the recursive option (-r), rm can also be used to delete directories:

[me@linuxbox me]$ rm -r directory...
Examples of rm and its options include:

Examples of the rm command
Command	Results
rm file1 file2	Delete file1 and file2.
rm -i file1 file2	Like above however, since the "-i" (interactive) option is specified, the user is prompted before each file is deleted.
rm -r dir1 dir2	Directories dir1 and dir2 are deleted along with all of their contents.

Be careful with rm!
Linux does not have an undelete command. Once you delete something with rm, it's gone. You can inflict terrific damage on your system with rm if you are not careful, particularly with wildcards.

Before you use rm with wildcards, try this helpful trick: construct your command using ls instead. By doing this, you can see the effect of your wildcards before you delete files. After you have tested your command with ls, recall the command with the up-arrow key and then substitute rm for ls in the command.

mkdir
The mkdir command is used to create directories. To use it, you simply type:

[me@linuxbox me]$ mkdir directory...
Using Commands with Wildcards
Since the commands we have covered here accept multiple file and directories names as arguments, you can use wildcards to specify them. Here are a few examples:

Command examples using wildcards
Command	Results
cp *.txt text_files	Copy all files in the current working directory with names ending with the characters ".txt" to an existing directory named text_files.
mv dir1 ../*.bak dir2	Move the subdirectory dir1 and all the files ending in ".bak" in the current working directory's parent directory to an existing directory named dir2.
rm *~	Delete all files in the current working directory that end with the character "~". Some applications create backup files using this naming scheme. Using this command will clean them out of a directory.
Further Reading
Chapter 4 of The Linux Command Line covers this topic in more detail