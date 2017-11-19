# Git

## Table of content

### Git as a persistent map

At his core git is a persistent map. Key: any sequence of bytes --> Values: SHA1 hash. For example: "Apple Pie" --> 23991897e13e47ed0adb91a0082c31c82fe0cbe5

```
 echo "Apple Pie" | git hash-object --stdin
```
For persisting map I need a repository:

```
git init
```
And then write (-w) on it:

```
 echo "Apple Pie" | git hash-object -w
```

If I search on hiddens file of my root directory:

```
 ls -a
```
I will find an hidden *.git* folder:

<img src="https://github.com/KiraDiShira/Git/blob/master/Images/githiddenfolder.png" />

This directory is where maps are persisted. Actually I have persisted only one item: "Apple Pie" --> 23991897e13e47ed0adb91a0082c31c82fe0cbe5

And in .git/objects directory there are other three directory.
I will talk later about *info* and *pack* directory, but note that *23* are the first two digits of the value of my item, while the remaining digits are the 23 directory's content:

<img src="https://github.com/KiraDiShira/Git/blob/master/Images/23new.PNG" />
ciao
