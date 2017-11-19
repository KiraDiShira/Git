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

If I want to know the type (-t) of my persisted object:

```
git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -t
blob
```

For unzip the object, remove the header and print out (-p) the actual content:

```
git cat-file 23991897e13e47ed0adb91a0082c31c82fe0cbe5 -p
Apple Pie
```
### Git as a stupid content tracker

```
git status
```

To commit a file I need to put it in the staging area first

```
git add
git commit -m "First commit"
```
To look the list of existing commit:

```
git log
```
<img src="https://github.com/KiraDiShira/Git/blob/master/Images/gitlog.png" />

The commit is stored in the same way of a file, and If I print out his content:

<img src="https://github.com/KiraDiShira/Git/blob/master/Images/commitobject.png" />

I can see that is pointing to a tree object.
