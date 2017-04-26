# All kinds of Git Stuff I learned

## Working with forks
In some companies i worked with, they liked to work with `forks` rather than with `branches`. 

There are some stuff that i learned in the process wich is worth monetioning here. 

1. [Configuring a remote for a fork](https://help.github.com/articles/configuring-a-remote-for-a-fork/)
1. [Syncing a fork](https://help.github.com/articles/syncing-a-fork/)

In case you need to work on someone else branch on his own fork, you first need to add his fork:
1. `git remote add NAME git@github:NAME/REPO.git` - this will add his fork as a remote
1. `fetch NAME` - to make sure you have all his branches
1. `git checkout -b BRANCH_NAME NAME/BRANCH_NAME` - create a branch in your fork based on his branch in his fork. 
