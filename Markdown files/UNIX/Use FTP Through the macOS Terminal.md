# Use FTP Through the macOS Terminal
<center>[Home](../index.html)</center>

[TOC]

## The connection
You'll have to know the address for your server _(or its domain)_:
```bash
ftp YourServerHere.com
```
> ❕ sftp is also available...

The Terminal will ask your username and your password.

## The available commands
The prompt is now ```ftp>```.  

<details><summary>These are the available command:</summary>

- The basics:
    - ```ls```, to list the files and directories in the current directory

    - ```cd```, to change of directory

    - ```quit```, to end your ftp session 

- The upload:
    - ```put```, to upload a file to the server

    - ```mput```, to upload multiple files on the server

- The download:
    - ```get```, to download a file from the server

    - ```mget```, to download multiple files on the server

- The modification:
    - ```mkdir```, to create a new folder

    - ```rename```, to rename/move a file

    - ```delete```, to delete a file
    > You'll have to use ```rm``` if you're using SFTP

    - ```!touch```, to create a file
</details>

## The upload

The command to upload files to a remote server is:

```bash
put localFile remoteFile
```

## The download

The command to download files off of a remote server is:

```bash
get remoteFile localFile
```

## The modification

### Rename a file on the server

The command to rename files on a remote server can be done with the following command:

```bash
rename oldName newName
```

### Move a file on the server

The command to move files within the server is:

```bash
rename newPath/fileName
```

### Create a file on the server _(kindof)_

The commands to create a file on the remote server are:

```bash
!touch localFile

put localFile remoteFile
```

> To use commands on the local host, you'll have to add a _**!**_ before the command.


***

<center>ToolKit © <!--[if IE 8]>2017<![endif]--><!--[if !IE 8]> -->2017 <span id="currentYear"></span><!-- <![endif]--></center><center><a href="https://alexandre-ducobu.com/En">About</a> </center>
