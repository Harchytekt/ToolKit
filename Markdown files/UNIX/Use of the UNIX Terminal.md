#Use of the UNIX Terminal (macOS)
<center>[Home](../index.html)</center>

[TOC]

##Open a file in an app
> There's a command for that: ```open```.

###Open it in the default app
> This is the simplest way: you just have to type the filename.

- Format:  

```bash
open myFile.ext
```

- Example:

```bash
open Main.java
```

###Open it in a chosen app
> You just have to add the name of the app preceded by **-a**.  

> Note: you have the choice to type the filename **before or after** the " _-a myApp_ ".

- Format:  

```bash
open myFile.ext -a myApp
# or
open -a myApp myFile.ext
```

- Example:

```bash
open Main.java -a atom
```

###Alias
> You can create an alias to go faster.

**Example:**

```bash
alias idea="open -a 'IntelliJ IDEA'"
```

***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a> </center>
