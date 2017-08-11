#Java
<center>[Home](../index.html)</center>

[TOC]

##Compilation

###Create jar (IntelliJ IDEA)

File | Project Structure | Artifacts then you should press alt+insert or click the plus icon and create new artifact choose --> jar --> From modules with dependencies.

Next goto Build | Build artifacts --> choose your artifact.

###With libraries

####For UNIX

If you have these 3 libraries :

- lib1.jar

- lib2.jar

- lib3.jar

You have to type this: 

```bash
javac -cp ".:lib1.jar;lib2.jar;lib3.jar" sourcefile.jar
java -cp ".:lib1.jar;lib2.jar;lib3.jar" sourcefile.jar
```

```bash
javac -cp ".:lib1.jar:lib2.jar:lib3.jar" sourcefile.jar
java -cp ".:lib1.jar:lib2.jar:lib3.jar" sourcefile.jar
```

####For Windows

You just have to replace **:** by **;**.

```bash
javac -cp ".;lib1.jar;lib2.jar;lib3.jar" sourcefile.jar
java -cp ".;lib1.jar;lib2.jar;lib3.jar" sourcefile.jar
```

Example :

```bash
javac -cp ".;.\be\isims\coo\tp5\ex2\lib\libClock.jar" .\be\isims\coo\tp5\ex2\ClockTest.java
java -cp ".;.\be\isims\coo\tp5\ex2\lib\libClock.jar" be.isims.coo.tp5.ex2.ClockTest
```

##Strings

###Interpolation

If you're using Java 5 or higher, you can use _String.format_:

```java
urlString += String.format("u1=%s;u2=%s;u3=%s;u4=%s;", u1, u2, u3, u4);
```

> See [Formatter](http://download.oracle.com/javase/6/docs/api/java/util/Formatter.html) for details.

##Packages

> To compile code from a package, for example be.heh.ex, you have to do:

```bash
javac be/heh/ex/*.java
```

> And then, to run it you only have to do:

```bash
java be/heh/ex/Main
```


***

<center>ToolKit © 2017</center><center><a href="http://alexandre-ducobu.esy.es/En">About</a> </center>

