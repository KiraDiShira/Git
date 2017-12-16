- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# The four areas

- [Introduction](#introduction)   
- [Basic workflow](#basic-workflow)   
- [Reset](#reset)
- [The stash](the-stash)

## Introduction

A Git project stores information in four separate storage areas. 

The first of the four areas is the project directory on your file system, your **working area**. 

The second area is the **repository** (Once you commit your data, Git stores it in what it considers the really important area, the repository). The repository contains the entire history of the project. 

In between these two areas, there is another intermediate area called the **index**. It's the place where you put your files before a commit. 

Finally, the fourth area sits a bit to the side. It's a temporary storage area called **stash**. It's not nearly as important as the other three, but it's useful.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa1.png" />

If you want to really understand a Git command, then for most commands, you should ask two important questions.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa2.png" />

the index is unique to Git or at least Git is the only versioning system that allows you to modify the index directly. You can visualize the index as something that stands between the working area and the repository. You generally don't move the data from the working area to the repository directly. You go through the index. That's why the index is also called the staging area. You stage your changes by adding them from the working area to the index and then you commit the changes from the index to the repository.

If you look at the content of the .git folder, you will see the index.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa3.png" />

It's a binary file, so we cannot just open it in a text editor, for example. Think of it as just another area that holds everything, just like the working area and the repository, all of your files and folders. So when we say git status and we see this message, 

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa4.png" />

that doesn't mean that the index is empty. It means that the index contains the same files and folders as the repository.

We can double check that with the git diff command. Git diff gives you the differences between two areas. One thing that is a bit counterintuitive about diff is if I use diff without any argument, then it's going to compare the working area with the index. Right now, they contain exactly the same data, so the diff is empty. But usually, I don't use this diff style, not too often. The git status command is usually all I need to see the difference between what I have that is my working area and what I am going to commit, the index. Instead, most of the times I want to compare the stuff I want to commit with the stuff I already committed. That is, I want to compare the index with the repository. For that, you can use git diff with the --cached option. Right now, the index and the latest committing the repository are aligned, so this diff is also empty. Okay, we're all clean.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa5.png" />

## Basic workflow

We know the flow from working area to repository:

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa6.png" />

What about the flow from repository to working area?

**checkout** does two things essentially. In the repository, it moves the head reference generally to another branch. So it changes the current commit. And the second thing it does is it takes data from the new current commit and it copies that data from the repository to the working area and to the index, so it changes the repository first and moves data second.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa7.png" />

Remove files in git:

What if I want remove the file from the index but not from the working area?

I can think that the opposite of “add” is “remove”, but unfortunatly this is not what remove does, or better is not the only thing that “remove” does.

If I used it without any option, then remove would try to delete the file from both the working area and the index. 

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa8.png" />

This could be pretty destructive, so remove has kind of a security feature built in, which you can see if I send this command.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa9.png" />

What happened is that Git noticed that the file I'm removing is not in our repository, so Git is essentially telling me look I don't see this file in the project history. If I remove it from both the working area and the index, then it will be gone forever, are you sure you want to do that? And it gives me a couple of options. I can force the removal, which is like saying yes, I know what I'm doing, just delete this file and forget about it. And I also have the option of removing the file from the index only, but not the working area with --cached.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa10.png" />

For removing from the working area:

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa11.png" />

Renaming files:

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa12.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa13.png" />

If I ask git status:

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa14.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa15.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa16.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa17.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa18.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa19.png" />

Git already understood what's happening. It compared the content of the file in the working area and the index with content of the files in the repository and it noticed that the orange file and the yellow file have the same content, so they must be the same file with a different name. That's pretty smart and it works both for renaming and for moving.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa20.png" />

## Reset

Reset is an operation that is all about moving a branch. You get a commit, say this commit here,

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa21.png" />

and the reset moves the current branch to that commit.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa22.png" />

So that commit is now the current commit.

Notice that reset doesn't move head. Head is still pointing to the same branch it was pointing at before, but the branch itself is moving, so head is following along for the ride. If you only look at the repository, then that's all that reset does. It moves a branch to point at the specific commit. The part that you might find confusing, however, is not what reset does to the repository, it's the second step, what a reset does to the other two main areas, the working area and the index, and the reset does different things there depending on its options. If you give it the **--hard** option, then reset copies data from the new current commit to both the working area and the index.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa23.png" />

With the **--mixed** option, reset copies data from the new current commit to the index, but leaves the working area alone. This is the default option, so if you don't give any option to reset, that will be a mixed reset.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa24.png" />

And finally, the **--soft** option means don't touch any of the areas. Just move the branch and skip step two entirely.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa25.png" />

The use case was I want to revert the whole project to the state it was in a previous commit. We did that with a hard reset, but that is not the only reason to use a reset.

```
git reset --hard fbe53536
```
I want to keep the changes in my working area, but I want to remove all changes from the index. In the index, I want the same version of the files that is in the repository. How do I do that? Earlier on, we've seen one way to do that using the **rm --cached** command. That works, but it's not the only way to do it. In fact, if you read Git's messages carefully, when I asked for the status, Git itself suggested a different command to our stage file. It suggested to using a reset.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa26.png" />

How exactly? Well the idea is to have what I call a head reset. This means that we're moving the current branch to the commit pointed at by head, but the current branch is already pointing at that commit by definition, so in this case, the reset does move the branch. If you wish, it moves it to the same place where it already is, so it doesn't move it. This is like skipping the first step in a reset altogether, the step where it moves the branch. What happens after that: Git moves data from the repository to the working area in the index. In this case, we didn't specify the kind of reset we want, so git will go with the default, and the default is a mixed reset.

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa27.png" />

## The stash

<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa28.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa29.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa30.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa31.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa32.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa33.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa34.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa35.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/TheFourAreas/Images/tfa36.png" />

