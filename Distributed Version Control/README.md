- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Distributed Version Control

- [Git clone](#git-clone)   
- [Local and remote](#local-and-remote)   
- [Pushing](#pushing)   

## Git clone

The git clone command takes the address of Git repository. I got the entire *.git* directory as well and all the files it contains. After copying this stuff, Git checked out the master branch to rebuild these files in the working area.

When we issued the git clone command, Git added a few lines to the configuration of our repository.

Each Git repository, such as this one, can remember information about other copies of the same repository. Each other copy is called a remote. You can define as many remotes as you want, but when you clone a project Git immediately defines a default remote and calls it with a conventional name, origin.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv1.png" />

## Local and remote

If we ask it for branches, then it will just show the local branches. We only have master now. But if you list the branches with the --all switch, then you see all the references, including the ones on the remote, the remote branches and the current position of HEAD.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv2.png" />

Git tracks a remote by just exactly like it tracks local branches, by writing those branches as references in the refs folder.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv3.png" />

If you look inside this folder, you might find that some of the branches are missing. In this case, I can only see the remotes HEAD here and not the branches. That's because of a low-level optimization in Git. To avoid maintaining one small file for each branch, Git sometimes compacts some of them into a single file called packed-refs here. There is no simple command to unpack this file, so you will have to take my word for it that the branches that are not in the refs directory must be in this file. This can happen for both local and remote branches.
Whenever you synchronize with a remote, Git updates remote branches. Let's see how that synchronization happens in practice.

## Pushing

Simplest case:

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv4.png" />
______________________________________________________________________________________________________________

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv5.png" />

______________________________________________________________________________________________________________

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv6.png" />

______________________________________________________________________________________________________________

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv7.png" />

______________________________________________________________________________________________________________

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv8.png" />

Another case, when we have a conflict: two different histories that need to be reconcilied

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv9.png" />

We have 2 options.
1)	Force a push: not raccomanded!

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv10.png" />

Green commit will be garbage collected.
We're also creating a very confusing situation for all other people synchronizing to the same remote because now their local history will be conflicting with the history in origin. So, probably forcing a push is not a good idea.

2)

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv11.png" />

What we want to do in general is we want to fix the conflict on our own machine before we push. To do that, we need first to fetch the data from the remote. There is a command to do that called git fetch. We get the new objects from the remote, and we also update the current position of the remote branches, as usual.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv12.png" />

Now that we have the new commit and the related objects, we can merge our local changes with the remote history. So, we did a fetch. Now we do a merge. Of course during the merge we might have to fix merging conflicts and the like, but the important point here is that we are not rewriting history. Merges never do that. Instead, they just add the new objects.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv13.png" />

 So, once we do the merge, our history is the history from the remote plus some more stuff, and we can push that new stuff to the remote without rewriting the remote's history.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv14.png" />
______________________________________________________________________________________________________________

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv15.png" />

This sequence of a git fetch followed by a git merge is so common that there is one single command that does both. It's called, you guessed it, git pull, a fetch followed by a merge.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv16.png" />


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

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/githiddenfolder.png" />

This directory is where maps are persisted. Actually I have persisted only one item: "Apple Pie" --> 23991897e13e47ed0adb91a0082c31c82fe0cbe5

And in .git/objects directory there are other three directory.
I will talk later about *info* and *pack* directory, but note that *23* are the first two digits of the value of my item, while the remaining digits are the 23 directory's content:

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/23new.PNG" />

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
## Git as a stupid content tracker

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
<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/gitlog.png" />

The commit is stored in the same way of a file, and If I print out his content:

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/commitobject.png" />

I can see that is pointing to a tree object.

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/objmod1.png" />

If I do a second commit:

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/secondcommit.PNG" />

Only the first commit has no parent, and each commit has a different tree value:

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/secondcommittree.PNG" />

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/gom.png" />

At this time there are 8 objects in the database:

```
git count-objects
```
If I change only 1 row in a 10000 rows files will be created a new object in my database? This will not happen, and this is the reason we exist the *info* and *pack* directories. We can't focus on this optimization layer to understand the git objects model.

TAG is like a label for the current state of the project. There are 2 type of tags: regular and annotated. Now we will see annotated tag.

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/tag.png" />

The git objects model is made up only of:
- Blob
- Commits
- Trees
- Annotated tags

<img src="https://github.com/KiraDiShira/Git/blob/master/GitIsNotWhatYouThink/Images/gomfinal.png" />
