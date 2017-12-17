- [Index](https://github.com/KiraDiShira/Git#table-of-content)   

# Branches demystified

- [Introduction to branches](#introduction-to-branches)   
- [How merge works](#how-merge-works)
- [Detached HEAD](#detached-head)


## Git log

I can use git log to look at the history, but the problem is the default in git log is not very useful when you're trying to make sense of a complex history because it squashes everything in a single list, so it's hard to make sense of branches and merges and understand what really happened. So I will use git log with a few options. The graph option gives me a nice graph-like structure where I can see how the commits and branch emerge and the decorate option shows the positional references like branches had. And finally, I will format the log so that each commit takes only one line.
```
“git log  --graph --decorate --oneline”
```
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h1.png" />



<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h2.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h3.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h4.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h5.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h6.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h7.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h8.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h9.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h10.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h11.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h12.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h13.png" />
<img src="https://github.com/KiraDiShira/Git/blob/master/History/Images/h14.png" />
