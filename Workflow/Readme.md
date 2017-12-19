- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Workflow

- [Sharing commit between branches](#sharing-commit-between-branches)   
- [Small workflow](#small-workflow)

## Sharing commit between branches

Branch 1 as the red commit that I want to merge in branch 2.

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf1.png" />

Git as a special command that is just for that:

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf2.png" />

It’s like a single commit rebase. And some project don’t want rebase, they prefer merge, so another solution is to put the shared commit on a 3rd branch, and then you merge the 3rd branch with both the first and the 2nd branch

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf3.png" />

This is a common situation when you have a bug fix

<img src="https://github.com/KiraDiShira/Git/blob/master/Workflow/Images/wf4.png" />

## Small workflow

**Branch creation**

```
git checkout master 
git pull origin master
git branch feature/LangTranslation
git checkout feature/LangTranslation
```

**Sviluppo quotidiano**

```
git checkout master
git fetch origin
git checkout feature/LangTranslation
git rebase origin/master

git add .
git commit -m "message name"
git push origin feature/LangTranslation
```

**Fine sviluppo**

```
git rebase -i origin/master
In editor: tutti f e il primo r. Salva e chiudi.
In editor: rinomina con messaggio di commit
git push -f origin feature/summary_of_the_feature
```

**Rimozione del branch**

```
git branch -D feature/LangTranslation --> cancella branch locale
git push origin :feature/LangTranslation --> cancella branch remote
```
