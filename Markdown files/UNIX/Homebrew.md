# Homebrew (macOS)
<center>[Home](../index.html)</center>

[TOC]

## Installation of Homebrew
[For more informations](http://docs.brew.sh)

### 1. Install Xcode

### 2. Install Homebrew

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 3. Debug it

```bash
brew doctor
```

## If you aren't admin
> You can add a basic user to the **sudoers** file as admin.
> [source](http://osxdaily.com/2014/02/06/add-user-sudoers-file-mac/)

### 1. Log in as admin
### 2. Launch Terminal and type:

```bash
sudo visudo
```

### 3. Navigate down to the “#User privilege specification” section
It should look like this:

```bash
# User privilege specification
root	ALL=(ALL) ALL
%admin	ALL=(ALL) ALL
```

### 4. Insert the username you want add to the sudoers file

Type **i** to enter the _Insertion Mode_.

```bash
username ALL=(ALL) ALL
```
Type **esc** to quit  _Insertion Mode_, then type **:wq** to quit _Vi_.

## Usefull commands

### Before anything
> You should update the local data base of brew before any operation.

```bash
brew update
```

### Cleanup
> This command is used to remove/uninstall old versions of packages.

#### To remove the old version(s) of a certain package

```bash
brew cleanup package
```

#### To see what could be cleaned up

```bash 
brew cleanup -n
```

#### To clean up everything at once

```bash
brew cleanup
```

### Doctor
> To fix all the warnings (outdated Xcode/CLT and unbrewed dylibs are very likely to cause problems).

```bash
brew doctor
```

### Install package

```bash
brew install package
```

### Leaves
> List of the packages which can be removed without problem.

```bash
brew leaves
```

### Missing
> List of the missing packages, that means the recipes that are a dependency of another installed package but are not installed.

```bash
brew missing
```

### Outdated
> To find out which packages are outdated.

```bash
brew outdated
```

### Remove software
> **uninstall** and **rm** are also available.

```bash
brew remove softwareName
```

### Search
> Before installing a package, you can search it to choose the version (Pyhton 2 or 3), to have the right name,…

```bash
brew search package
```

#### In Cask
> Go to this page: [Cask](https://github.com/caskroom/homebrew-cask/find/master)
> and type the wanted sofware.  
> This [site](https://caskroom.github.io/search) is also available.

### Upgrade
> This command will upgrade the outdated packages.

#### All

```bash
brew upgrade
```

#### A certain package

```bash
brew upgrade package
```

#### Stop a package from being updated

```bash
brew pin package
```

**Remarque:** _The unstop it, replace **pin** with **unpin**._

## And now? We install stuff!

### Ant
> Apache Ant is a Java library and command-line tool whose mission is to drive processes described in build files as targets and extension points dependent upon each other. The main known usage of Ant is the build of Java applications. Ant supplies a number of built-in tasks allowing to compile, assemble, test and run Java applications.

```bash
brew install ant
```

### [Cask](https://caskroom.github.io)

> Homebrew Cask extends Homebrew and brings its elegance, simplicity, and speed to macOS applications and large binaries alike.

```bash
brew tap caskroom/cask
```

**Remarque:** _When you install stuff with Cask (not as admin), you have to give the right to **write** to the '**Staff**' group on '**/Users/alexandre/Library/QuickLook**' (through the GUI)._

#### [QuickLook plugins (with Cask)](https://github.com/sindresorhus/quick-look-plugins/blob/master/readme.md)  

##### QLColorCode
> Preview source code files with syntax highlighting

```bash
brew cask install qlcolorcode
```

##### QLStephen
> Preview plain text files without or with unknown file extension. Example: README, CHANGELOG, index.styl, etc.

```bash
brew cask install qlstephen
```

##### QLMarkdown
> Preview Markdown files

```bash
brew cask install qlmarkdown
```

##### ProvisionQL
> Preview iOS / macOS app and provision information

```bash
brew cask install provisionql
```

### Clisp
> Common Lisp is a high-level, general-purpose, object-oriented, dynamic, functional programming language.

```bash
brew install clisp
```

### [ExifTool by Phil Harvey](http://www.sno.phy.queensu.ca/~phil/exiftool/)
> ExifTool is a platform-independent Perl library plus a command-line application for reading, writing and editing meta information in a wide variety of files.

```bash
brew install exiftool
```

### go
> Go is an open source programming language that makes it easy to build simple, reliable, and efficient software.

```bash
brew install go
```

**Remarque:** _You have to add this to the PATH:_

```bash
# go path
export GOPATH=/Users/alexandre/go/
export PATH=$GOPATH/bin:$PATH
```

#### [Licence (through go)](https://github.com/nishanths/license)
> Create licenses from the command-line.

```bash
go get -u github.com/nishanths/license
```

### [Mackup](https://github.com/lra/mackup)
> Keep your application settings in sync (OS X/Linux)

```bash
# Install Mackup
brew install mackup

# Launch it and back up your files
mackup backup

# Or

# Launch it and restore your files
mackup restore
```

### [Support to BPG](http://bellard.org/bpg/)

> BPG(Better Portable Graphics) is a new image format. Its purpose is to replace the JPEG image format when quality or file size is an issue.

```bash
brew install libbpg
```

#### [QuickLook plugin for BPG](https://github.com/Nyx0uf/qlImageSize)
> This is a QuickLook plugin for OS X 10.11+ to display the dimensions of an image and its file size in the title bar. It can also preview and generate Finder thumbnails for unsupported images formats like bpg and WebP.

### Others

#### [ m-cli](https://github.com/rgcr/m-cli)
> 💥 Swiss Army Knife for macOS ! 

#### [Mac CLI](https://github.com/guarinogabriel/Mac-CLI)
>  macOS command line tools for developers – The ultimate tool to manage your Mac. It provides a huge set of command line commands that automatize the usage of your OS X system.

#### [Awesome OS X Command Line](https://github.com/herrbischoff/awesome-osx-command-line)
> Use your OS X terminal shell to do awesome things.


***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a> </center>

