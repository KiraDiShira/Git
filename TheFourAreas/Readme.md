- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# The four areas

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
