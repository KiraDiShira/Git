- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Branches demystified

- [Git as a persistent map](#git-as-a-persistent-map)   
- [Git as a stupid content tracker](#git-as-a-stupid-content-tracker)

## Git as a persistent map

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
