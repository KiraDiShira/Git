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
