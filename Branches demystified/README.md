- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Branches demystified

- [Introduction to branches](#introduction-to-branches)   
- [How merge works](#how-merge-works)
- [Detached HEAD](#Detached-HEAD)


## Introduction to branches

When first commit is made, git creates "master" branch.
Branches are stored in this folder:

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/branchesfolder.PNG" />

*A branch is just a reference to a commit.*

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/Branch%20ob.png" />

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/pointer.png" />

To create a new branch:
```
git branch branchname
```
To see the list of branches:
```
git branch
```
What is the current branch? HEAD, is a reference to a branch

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/headd.png" />

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/head.png" />

When we make a new commit, the current branch points to that.

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/newcommit.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/newcommit2.png" />

How switch between branches?

```
git checkout branchname
```
Checkout = move head and update working area

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/checkout.png" />

## How merge works

If there is a new commit on Lisa branch:

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/merge1.png" />

We want to merge on master branch the commit on Lisa branch

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/merge2.png" />

If there is a conflict we need to resolve it with smartgit

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/merge3.png" />

and then put the resolved files in staging area, and finally made a merging commit. A merge is just a commit with one exception: it has 2 parents.

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/merge4.png" />

*References between commits are used to track history. All the other references are used to track content.*

Now we will see another type of merge:

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/merge5.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/merge6.png" />

In this case, it's not created a merge committ because master branch is ahead and so all conflicts are already been resolved. This behaviour is called *fast forward*.

## Detached HEAD

It's possible that HEAD refers to a commit instead of a branch:

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/dethead1.png" />

If I do other commits, HEAD behaves like a branch:

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/dethead2.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/dethead3.png" />

Garbage collector will delete unreachable objects.
If I don't want that this happen:

<img src="https://github.com/KiraDiShira/Git/blob/master/Branches%20demystified/Images/gc.png" />




