- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Rebasing made simple

- [Introduction to rebase](#introduction-to-rebase)   
- [Rebase under the hood](#rebase-under-the-hood)
- [Rebase vs merge](#rebase-vs-merge)
- [Tags](#tags)

## Introduction to rebase

There is another way of merging branches: *rebase*. This is how conceptually works. Green branch is the HEAD:

<img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase1.PNG" />

Git looks for the first commit in spaghetti that is also a commit in master. It's this commit here.

<img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase2.PNG" />

This is the base of this spaghetti branch. All the history before this commit is already shared between the two branches,
so it's not relevant here. Now Git detaches the entire spaghetti branch from this commit and moves it on top of master,
so it changes the base of this branch. That's why it's called a rebase.

<img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase3.PNG" />

Suppose to switch to master branch e rebase spaghetti, as in the merge we will have:

<img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase4.PNG" />

Just like in a merge, we have all the commits that deal with the spaghetti and all the commits that deal with the pie in the same 
history. However, different than a merge, we got that result not by letting multiple branches flow together, but by rearranging the
branches so that they look like one single branch.

## Rebase under the hood

We explained a simplified version of rebase. 
What happens if you change the parent of this commit?

<img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase5.PNG" />

The parents SHA1 is stored inside the commit, so the commit data must change, and the commit must get a new SHA1. 
Now that this commit has a new SHA1, this other commit

<img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase6.PNG" />

 also has to change because its own parent has changed, so it gets a new SHA1 as shown for all the commits in the branch. 
 So Git cannot just move the commits. The commits in the rebase branch must have different SHA1s, so there must be different objects in the database. In other words, new commits, and indeed that's what they are. Here is how rebasing really works. When you rebase, Git makes copies of the commits. It creates new commits with mostly the same data, actually exactly the same data except for their parents.
 
<img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase7.PNG" />

 So these new commits look almost exactly like the original commits, but they are new objects with new SHA1s, so they are new files with new file names in the database directory. And finally, Git moves the rebase branch to the new commits leaving the old commits behind.
 
 <img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase8.PNG" />
 
 What’s happen to?
 
 <img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase9.PNG" />
 
 Git garbage-collects unreachable objects
 
 ## Rebase vs merge
 
  <img src="https://github.com/KiraDiShira/Git/blob/master/Rebasing%20Made%20Simple/Images/rebase10.PNG" />
  
  Merge perseveres history exactly as it happened.
  
  Rebasing helps you refactor your project history so that it's always nice to look at. This neatness, however, comes at a cost. This nicely designed history is not real. It was forced by rebasing, which is a distractive operation. Rebasing creates new commits and leaves behind existing commits that might get garbage collected. So a rebase history looks cleaner, but it is a lie its own way.
  
## Tags

In Git there are two types of tags. In module one we talked about annotated tags. The other kind of tag doesn't have a specific name, so people sometimes call them non-annotated tags or lightweight tags.

We could create an annotated tag. Maybe you still remember that we can do that with tag -a. This tag would contain a lot of useful information such as the date that the tag was created, who created it, a description, and so on. However, in some cases I could decide that there is no reason to have all that information. I might just want to mark this commit with a simple label for my own use. If that is the case, then lightweight tag is enough. I can create such a tag by skipping the -a option in the tag command. There, now we have a tag. There it is. I did not have to provide the message or anything. Now, let's peek inside the .git refs directory. There is heads directory here that we already know about, it contains the branches, and then there is a tags directory that contains the tags. There are two tags in there, the one we already had and the one we just created. They are two simple files that contain the SHA1 of an object in the database. See. A tag is a reference to an object, in this case a commit just like a branch. I could actually turn this tag into a branch just by moving it to the refs heads directory. This is a lightweight tag, so it contains the SHA1 of a commit. An annotated tag is similar, but it contains the SHA1 of a tag object in the database, and that object in turn is referencing a commit besides containing all the extra information like the tag description. If tags look just like branches, then what's the difference between a tag and the branch? Simply enough, while branches move, tags don't. If I create a new commit right now, then master will move to track it because it's the current branch, but the tag will just stick to the same object forever.

 
