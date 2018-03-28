- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Distributed Version Control

- [Git clone](#git-clone)   
- [Local and remote](#local-and-remote)   
- [Remote tracking branch](#remote-tracking-branch)
- [Pushing](#pushing)   
- [Rebase revisited](#rebase-revisited)
- [Features of GitHub](#features-of-github)

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

## Remote tracking branch

Remote-tracking branches are references to the state of remote branches. They’re local references that you can’t move; Git moves them for you whenever you do any network communication, to make sure they accurately represent the state of the remote repository. Think of them as bookmarks, to remind you where the branches in your remote repositories were the last time you connected to them.

Remote-tracking branches take the form <remote>/<branch>. For instance, if you wanted to see what the master branch on your origin remote looked like as of the last time you communicated with it, you would check the origin/master branch. 

<img src= "https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/RemoteTracking1.PNG" />

___________________________________________________________________________________________________________

<img src= "https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/RemoteTracking2.PNG" />

To synchronize your work, you run a **git fetch origin** command. This command looks up which server “origin” is (in this case, it’s git.ourcompany.com), fetches any data from it that you don’t yet have, and updates your local database, moving your origin/master pointer to its new, more up-to-date position.

<img src= "https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/RemoteTracking3.PNG" />

*git fetch origin* fetch data only from origin, and **git fetch --all** fetch data from all remotes (origin is one of them)

```
git push -u origin new-feature
```

This command pushes new-feature to the central repository (origin), and the -u flag adds it as a remote tracking branch. After setting up the tracking branch, git push can be invoked without any parameters to automatically push the new-feature branch to the central repository.

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

`git pull origin master` is the same of

```
git fetch origin
git merge origin/master
```

## Rebase revisited

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv17.png" />

We're working on the lisa branch, and we decide to roll the changes from master into lisa. You know that we can do this with either a merge or a rebase, so let's try the rebase this time. Git copies over the lisa commit so that its parent is now the latest commit on master, and there we are. However, remember that this new yellow commit that we have here is not the same commit as the previous yellow commit. Instead, it's a copy, a different database object. I marked it with an explanation point to tell it apart from the original commit.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv18.png" />

The original commit will actually be garbage collected at some point.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv19.png" />

So, now we have a conflict again. We can't just push because we have different histories on our local repo and on origin. This particular conflict, however, doesn't seem like much. We can fix it easily, for example by doing a force push or a pull followed by a push.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv20.png" />

In any case, we can work around this, and then we have the same stuff on origin that we have on local. However, things break down when we introduce another user.

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv21.png" />

_________________________________________________________________________________________________________________

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv22.png" />

She added a commit there, so now Annie has a pretty nasty conflict to sort out the next time she synchronizes with origin. She needs to understand what happened first, and then to solve the conflicts even though she didn't cause the conflicts herself. There are good chances that even after solving the conflicts she will end up with a confusing history that includes both yellow commits even though they look exactly the same. So, this is the bottom line when it comes to rebasing. As a general rule, never rebase stuff that has been shared with some other repository. It's okay to rebase commits that you haven't shared yet in general, but remember that it's easy to rebase share commits by mistake and then expect some trouble.

## Features of GitHub

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv23.png" />

A fork is kind of like clone, but it's a remote clone. We are cloning the project from someone else's GitHub account to our own GitHub account. So now we have a new project in the cloud, and we can clone that one on our local machine. When we do that, Git creates a remote in our local repo pointing at origin. Origin is pointing at our own GitHub project, not the original project, of course. Actually, from Git's point of view there is no connection at all between our project and the original project that we fork from. GitHub does know that the two projects are connected, but Git doesn't. So if we want to track changes to the original project, then we need to add another remote pointing at it. This is not something that Git does automatically. We have to do it ourselves. A common convention is to call this a remote upstream. Now we have our local project with multiple remotes. We can work on it, and we can synchronize all our local changes with origin. If we commit local changes, we can just push those changes to origin. If there are changes on upstream, we can pull them into our local project, solve any conflicts, and then push them to origin. One thing that we still cannot do, however, is to push changes to upstream. 

<img src="https://github.com/KiraDiShira/Git/blob/master/Distributed%20Version%20Control/Images/dv24.png" />

For example, we might like to contribute our orange commit to the original project, but we still do not have right access to upstream, so GitHub gives us an alternative. We can send a message to the maintainers of upstream and ask them to pull our changes. You know how it this is called. It's a pull request. Once again, pull requests are not a Git feature. They're not even a version control feature, strictly speaking. In a way, they are a social network feature. You're just sending a message to people. If those people like your changes, then GitHub makes it easy for them to do a remote pull and get your changes from origin. And that's all about forks and pull requests, two of the most important tools in modern open source development.
