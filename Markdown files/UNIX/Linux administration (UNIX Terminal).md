# Linux administration (UNIX Terminal)
<center>[Home](../index.html)</center>

[TOC]

```
+-------------------------------------------------------------------------------+
|	man																			|
|	short for manual, it is a documentation usually found on a UNIX system.		|
+-------------------------------------------------------------------------------+
```

**Format**  

```bash
man <commande>
```

**Example:**  

```bash
man ls
```

**RQ:** _RTFM_ means _Read The Fucking Man_

## Commands

### Various

#### Add a message of the day at login

```bash
vi /etc/motd
Your message
```

#### Concatenate two file in one

```bash
cat file1 file2 > finalFile
```

#### Create new directory

**Format**

```bash
mkdir path/dirname
```

**Examples:**

```bash
mkdir myDir
mkdir /home/username/Desktop/myNewDir
```

#### Create new file

**Format**

```bash
touch path/filename
```

**Examples:**

```bash
touch README
touch /home/username/Desktop/script.py
```

#### Determine file type

```bash
file filename
```

_For **multiple** files, separate them with spaces._

```bash
file file1 /dir/file2
```

#### Display 'Hello' and the current date
```bash
echo "Hello " $(date '+%A %W %Y %X')
```

#### Execute a command as root

```bash
su root -c "nano /etc/fstab"
```

#### Find filenames quickly (needs updateDB)

```bash
locate filename
```

##### updatedb

_To be able to make a search, you have to build a database of your filesystem._  
_The norm is to execute **updatedb** in a cron: cron.daily at5 am. (see **cron**)_

```bash
updatedb
```

#### Get a calendar of the current month

```bash
cal
```

#### Get current directory

```bash
pwd
```

#### Get current user

```bash
whoami
```

#### Get the date

```bash
date
```

#### Get last logins of users and ttys

```bash
last
```

#### Get user's terminal name

**Format**

```bash
tty
```

**Example:**

```bash
tty
/dev/ttys000
```
#### Get line, word, character, and byte count of a file

_Displays, by default, the **number of lines, words, and bytes**._

```bash
wc file
```

**Example:**

```bash
cat test.txt 
This is a short line.
This is a second short line.
wc test.txt 
       2      11      51 test.txt
```
#### Locate a program file in the user's path - which

**Format**

```bash
which program
```

**Example:**

```bash
which passwd
/usr/bin/passwd
```

#### Move in file like in Vim - less

```bash
less myFile.txt
```

#### Move in command result like in Vim - less

```bash
chkconfig | less
```

#### Search in command result - grep

```bash
chkconfig | grep sshd
#Search for sshd from listed services by chkconfig
```

### Backup - tar

#### Save all the files (and dir) in 'file.tar.gz' and compress the data
```bash
tar -zcvf file.tar.gz files /dir
```

#### Save all the files and /dir in 'file.tar'

```bash
tar -cvf file.tar files /dir
```

#### Extract all the files and/or dir from the file (extract it from the root dir)

```bash
tar -xvf file.tar
```

#### Extract all the data from the dir inside the .tar

```bash
tar -xvf file.tar -C /dir
```

#### List all the content of the .tar

```bash
tar -tvf file.tar
```

#### Decompress the archive.
_The second line is the result of **ls**._

```bash
gunzip file.tar.gz
file.tar
```

### Clear the Terminal history
> By pressing the **up** arrow in the command line we'll see the last command we ran. Keep pressing **up** and we’ll see more commands; we can go back days, months, or even years.  

> This is called the history, and it’s very convenient. If we made a mistake typing a long command, simply press **up** and fix the problem. If we want to re-connect to an SSH server we used the other day, simply press **up** until we see the relevant command.  

> It’s useful, but there’s also a potential security problem here, particularly if we accidentally typed a password in plain text at some point. How could we clear the history?  

> Here’s how to do it.

#### Clear all of your Bash history
> If we want to remove the entirety of the history, we have to type this command:
```rm ~/.bash_history```.

> Alternatively, we could open the file and delete any lines we want to.

#### Clear the current session’s history
> The history can be broke down into two parts. There’s the current sessions’ history, and the long-term history.  
> Our first command deals with the current session: ```history -c```.

> The history command is built into Bash itself, and the -c modifier tells the program to clear that history.  
> This command will prevent anything in the current session from being written to the long-term history, but does not clear out that long-term history.

### Compression - (g)zip

#### Compress the file with gzip into 'file.txt.gz'

```bash
gzip file.txt
```

#### Decompress the file
```bash
gunzip file.txt.gz
```

#### Display information about the file's compressed and uncompressed size
**Also shows** _ratio, uncompressed name._  
Add **-v** for more infos.

```bash
gzip -l file.ext.gz
```

#### Compress the files with zip into file.zip
```bash
zip file.zip files
```

#### Compress all the files and dirs from /dir

```bash
zip -r file.zip /dir

```

#### Compress multiple files and dirs

_You have to **separate** them with spaces._

```bash
zip -r files.zip file1 file2 /dir
```

#### Decompress the file

```bash
unzip file.zip
```

### Copy files

#### Copies the file and renames it

```bash
cp fileName newFileName
```

#### Copies the file in myDir/ (without renaming it)

```bash
cp fileName myDir/
```

#### Copies the file in myDir and renames it

```bash
cp fileName myDir/newFileName
```

#### Copies myDir with a new name

```bash
cp -R myDir myNewDir
```

#### Copies all the .jpg files into myDir

```bash
cp *.jpg myDir/
```

### Disk usage - du

#### Get the disk usage for all the files of the disk

```bash
du
```

#### Get size of a file (or the files of a folder)

##### Default size _(in units of 1024 bytes)_

**Format**

```bash
du filename
```

**Example:**

```bash
du Desktop/Test/Grid.java 
16		Desktop/Test/Grid.java
```

##### Human-readable output -h

_Use unit suffixes: Byte, Kilobyte, Megabyte, Gigabyte, Terabyte and Petabyte._

**Format**

```bash
du -h filename
```

**Example:**

```bash
du -h Desktop/Test/Grid.java 
8,0K	Desktop/Test/Grid.java
```

#### Get size of a folder - sh

**Format**

```bash
du -sh myDir/
```

**Example:**

```bash
du -sh Desktop/Test
22M	Desktop/Test
```

### Find

#### Find a file _(locate is better)_

**Be careful** _Without **-name**, the command will return that the file doesn't exist._

##### In a given directory

```bash
find / -name filename
#The file will be searched everywhere → '/'.
```
##### In the current directory

```bash
find -name filename
```

#### Find a file from its last modified date

##### Files modified n days ago

```bash
find / -mtime n
```

##### Files modified more than n days ago

```bash
find / -mtime +n
```

##### Files modified less than n days ago

```bash
find / -mtime -n
```

### List directory contents - ls

#### Lists current directory contents

```bash
ls
```

#### List in long format
**Total sum** _for all the file sizes is output on a line before the long listing._

```bash
ls -l
```

#### Include hidden directory entries
_Those whose names begin with **a dot (.)**_

```bash
ls -a
```

#### Reverse the order of the sort
_To get reverse lexicographical order or the oldest entries first (or largest files last, if combined with sort by size)._

```bash
ls -r
```

#### Recursively list subdirectories encountered

```bash
ls -R
```

#### Sort by time modified
_Most recently modified first before sorting the operands by lexicographical order._

```bash
ls -t
```

#### A combination of the different options

```bash
ls -lart
```

#### Enable colorized output.
_This option is equivalent to defining CLICOLOR in the environment._

```bash
ls -G
```
_See **man ls** for more options_

### Remove/delete files and directories
**RQ:** _The **rm** utility removes symbolic links, not the files referenced by the links._

#### Delete a file (won't be in Trash)

```bash
rm file
```
#### Delete the file after confirmation

```bash
rm -i file
```

#### Delete all the named files

```bash
rm file1 file2
```

#### Delete directory

##### Default, ecursive mode

**Works also** _with -r_

```bash
rm -R myDir
```

##### Other method _(only if the directory is empty)_

```bash
rmdir myDir
```

#### Delete files/dirs with override

```bash
rm -f item
```

#### Delete multiple directories

```bash
rm -rf {dir1,dir2}
```

### Renamming/moving files

#### Renames fileName into newFileName

```bash
mv fileName newFileName
```

#### Renames myDir into myNewDir

```bash
mv "myDir" "myNewDir"
```

#### Moves fileName in myDir and renames it

```bash
mv fileName myDir/newFileName
```

### Shutdown command

#### Shutdown the system

```bash
shutdown -h now
```

**or**

```bash
halt
```

#### Restart the system

```bash
shutdown -r now
```

**or**

```bash
reboot
```

### User management

### Add a new user

```bash
useradd username
```

### Add password to an user

```bash
passwd password
```

### Delete an user

```bash
userdel username
```

## Services

**You have to be _root_**

### (Re)launch a service

**Format**  

```bash
service <daemon> start
```

**Example:**  

```bash
service sshd start
service sshd restart
```

### Gets the service status

**Format**  

```bash
service <daemon> status
```

**Example:**  

```bash
service sshd status
openssh-daemon (pid  2362) en cours d'exécution…
```

### Stop a service

**Format**  

```bash
service <daemon> stop
```

**Example:**  

```bash
service sshd stop
```


***

<center>ToolKit © 2017</center><center><a href="https://alexandre-ducobu.com/En">About</a> </center>
