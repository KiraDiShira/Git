- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Workflow

- [Sharing commit between branches](#sharing-commit-between-branches)   

## Sharing commit between branches

Branch 1 as the red commit that I want to merge in branch 2.

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf1.png" />

Git as a special command that is just for that:

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf2.png" />

It’s like a single commit rebase. And some project don’t want rebase, they prefer merge, so another solution is to put the shared commit on a 3rd branch, and then you merge the 3rd branch with both the first and the 2nd branch

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf3.png" />

This is a common situation when you have a bug fix

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf4.png" />



