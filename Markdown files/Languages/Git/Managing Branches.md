<!--
Author: Alexandre Ducobu
Creation date: Mer 24 jan 2018 10:48:25 CET
-->

# Managing Branches
<center>[Home](../../index.html)</center>

- [Managing Commits](Managing%20Commits.md)
- [Managing Branches](Managing%20Branches.md)
    - [Create a new branch](#newbranch)
    - [Change branch](#changebranch)
    - [Delete a branch](#deletebranch)
    - [Merge two branches](#merge)

<a name="newbranch"></a>
### Create a new branch

Create a new branch is easy.  
There're two methods to create a branch.  
I'll show you the easiest.  

So, we want to create a branch to **fix** the **logout** of our site.  
I'll name it _**fix/logout**_...  
> You should have a _Branch Naming Convention_

```
git checkout -b fix/logout
```

We're now on the _**fix/logout**_ branch!  
Push it the remote repo:  

```
git push --set-upstream origin fix/logout
```


<a name="changebranch"></a>
### Change branch

To begin, we have to know the branches we have and on which one we are:  

```
$ git branch
* develop
  feature/AddComments
  feature/Unknown
  fix/logout
  master
```

We have 4 branches:

- _**develop**_: the main branch where the source code is always in a state with
the latest development changes delivered for the next release.
- _**feature/AddComments**_: the branch where the new feature, _the comments_, is
developed.
- _**feature/Unknown**_: the branch where an unknown feature will be developed.
- _**fix/logout**_: the branch where the logout is fixed.
- _**master**_: the main branch where the source code is always in a
production-ready state.

The asterisk shows us the branch we're currently on.

Now that we know where we are, we can choose where we're going: I choose
_**feature/AddComments**_.  

We only have to write this command:  

```
git checkout feature/AddComments
```

And we are on the branch!


<a name="deletebranch"></a>
### Delete a branch

The deletion of branches is easy, but we have to be careful: a branch have to be
deleted locally _(on your PC)_ and remotely _(e.g. on GitHub)_.  

We are on _**feature/AddComments**_ and, for some reason, we abandon the
functionality. We should delete its branch then.  

First, we have to change branch. Let's say we go to _**develop**_:  

```
git checkout develop
```

We can delete the local branch:  

```
git branch -d feature/AddComments
```

Now we delete the remote one:  

```
git push origin -d feature/AddComments
```


<a name="merge"></a>
### Merge two branches

So, we are on _**fix/logout**_ and we have to merge it with _**develop**_.  
To do so, we have to:

1. return to _**develop**_  

```
git checkout develop
```  

2. merge the two branches  

```
git merge --no-ff fix/logout
```  

3. delete _**fix/logout**_ _(locally)_  

```
git branch -d fix/logout
```  

4. push the changes  

```
git push -u origin develop
```  

5. delete _**fix/logout**_ _(remotely)_  

```
git push origin -d fix/logout
```


<a name="renamebranch"></a>
### Rename a branch

There're only three branches left:  

```
$ git branch
* develop
  feature/Unknown
  master
```

We're going to work on that _unknown_ feature but we should rename it.  
Indeed the name isn't representative of our feature...  

As we want to add articles to the site, let's call it _**feature/AddArticles**_.  
Because we are on _**develop**_, the command is:  

```
git branch -m feature/Unknown feature/AddArticles
```

If we were on _**feature/Unknown**_, the command would be:  

```
git branch -m feature/AddArticles
```

Now we have to push the changes:  

```
git push origin :feature/Unknown feature/AddArticles
```

Then we push the new branch and connect the remote and local branches:  

```
git push --set-upstream origin feature/AddArticles
```



***

<center>ToolKit © <!--[if IE 8]>2017<![endif]--><!--[if !IE 8]> -->2017 <span id="currentYear"></span><!-- <![endif]--></center><center><a href="https://alexandre-ducobu.com/En">About</a> </center>
