- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Branches demystified

- [Exploring the past](#exploring-the-past)   

## Exploring the past

I can use git log to look at the history, but the problem is the default in git log is not very useful when you're trying to make sense of a complex history because it squashes everything in a single list, so it's hard to make sense of branches and merges and understand what really happened. So I will use git log with a few options. The graph option gives me a nice graph-like structure where I can see how the commits and branch emerge and the decorate option shows the positional references like branches had. And finally, I will format the log so that each commit takes only one line.
```
“git log  --graph --decorate --oneline”
```
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h1.png" />

Another way to inspect a committ is to give Git the name of a reference to this pointing at the commit.
```
git show nogood
```

or

```
git show HEAD
```
what if we want to reference this other commit?

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h2.png" />

There is no reference pointing at it, so it seems that our only option is to use its hash. However, there are other ways. I can start at head and add a caret like this. The caret means the parent commit, so now I'm asking for the parent commit of head.

```
git show HEAD^
```

And if I want to refer to this commit here?

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h3.png" />

```
git show HEAD^^
```
Or
```
git show HEAD~2
```
What if I want refer to this commit?

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h4.png" />

It’s the second parent of the second commit before head

```
git show HEAD^2~2
```
`git blame`. This shows you where the lines in the file are coming from.

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h5.png" />

Comparing differences between commit

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h6.png" />

Comparing differences between branches:
```
git diff nogood master
```
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h7.png" />

## Fixing the latest commit

Suppose that I make a commit but I realize that I miss something. I could create a new commit but the best option is to change the last commit

```
git commit --amend
```

What happen under the hood? Commits are immutable

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h8.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h9.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h10.png" />

In this case, I amended a commit that I hadn't shared yet. I'd never pushed it to a shared repository, so it was okay to change it. 

## Interactive rebase

Rebase can also change history, interactive rebase can rewording, squashing, picking commit and so on.
`git rebase –i` needs a reference to a commit, so for example:

```
git rebase –i origin/master
```

This means, let me edit history from this commit excluded.

## The Reflog

We said that whenever you do anything that changes history like an interactive rebase, for example, or even something as simple as a menu commit, Git has to copy information from all commits to new commits. The new commits might look like the old commits, but they are not the same objects and the old commits are left behind and usually they are unreachable. There is no branch or tag pointing at them anymore. So they would stay in the object database for a while until Git eventually decides to garbage collect them. Now what if I change my mind and I want to recover one of those objects. This is not a common situation, but sometimes it can happen. For example, what if I do an interactive rebase and delete the commit by mistake. Now that commit and its associated data, they're not in the history anymore. I know they're still somewhere in the object database, but I don't know their hashes anymore, so I cannot recover them, so what do I do now? Well the good news is there is a very easy way to recover the hashes of abandoned objects. Every time a reference moves in the repository, Git logs that move. Git logged those movements into something that is called the reference log or the ref log for short and I can look at the ref log with git reflog and then I can give it the name of reference:
```
git reflog HEAD
```

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h11.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h12.png" />

And if you can see it, then you can recover it. For example, you can put a branch on it and then it's not an abandoned commit anymore. Just to make it clear, the information in the ref log is strictly local information. This ref log belongs to this repository and this repository alone. If I clone this repository again to another directory, then I will get a different ref log. But when it comes to this repository, every time head moves, Git is going to log it here. And the same goes for other references, such as the master branch.

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h13.png" />

## Reverting

All that it does is write a new commit with new data that is the opposite of existing data.
The git revert command undoes a committed snapshot. But, instead of removing the commit from the project history, it figures out how to undo the changes introduced by the commit and appends a new commit with the resulting content. This prevents Git from losing history, which is important for the integrity of your revision history and for reliable collaboration.

<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h14.png" />

```
git revert <commit>
```

Generate a new commit that undoes all of the changes introduced in <commit>, then apply it to the current branch.

