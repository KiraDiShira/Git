- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Rebasing made simple

- [Introduction to rebase](#introduction-to-rebase)   
- [How merge works](#how-merge-works)
- [Detached HEAD](#detached-head)


## Introduction to rebase

There is another way of merging branches: *rebase*. This is how conceptually works. Green branch is the HEAD:

<img src="rebase1.PNG" />

Git looks for the first commit in spaghetti that is also a commit in master. It's this commit here.

<img src="rebase2.PNG" />

This is the base of this spaghetti branch. All the history before this commit is already shared between the two branches,
so it's not relevant here. Now Git detaches the entire spaghetti branch from this commit and moves it on top of master,
so it changes the base of this branch. That's why it's called a rebase.

<img src="rebase3.PNG" />

Suppose to switch to master branch e rebase spaghetti, as in the merge we will have:

<img src="rebase4.PNG" />

Just like in a merge, we have all the commits that deal with the spaghetti and all the commits that deal with the pie in the same 
history. However, different than a merge, we got that result not by letting multiple branches flow together, but by rearranging the
branches so that they look like one single branch.

## Rebase under the hood

We explained a simplified version of rebase. 
What happens if you change the parent of this commit?

<img src="rebase5.PNG" />

The parents SHA1 is stored inside the commit, so the commit data must change, and the commit must get a new SHA1. 
Now that this commit has a new SHA1, this other commit

<img src="rebase6.PNG" />

 also has to change because its own parent has changed, so it gets a new SHA1 as shown for all the commits in the branch. 
 So Git cannot just move the commits. The commits in the rebase branch must have  different 
