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


In case you need to synch your master with the upstream:
```
git reset --hard upstream/master
git push --force
```

## Cherry Picking
In case you are working on a branch and there are other commits in your PR which is not related to your work, you can:
1. create a `tmp` branch from your master (make sure master is synched with upstream)
1. go back to your branch and squash all your commits into one commit: `git rebase -i 9823e10` (where the Stash is the commit before your first commit)
1. do `git log` to find the hash for your new squashed commit. 
1. checkout your `tmp` branch
1. `git cherry-pick df3d4f8e2078e91058c630a92a1ac01f35af07f4`


In case you are working on a brnach and you need to synch with master but merge adds all kinds of commits (can happen if you branched from a different branched, which was merged and squashed), here is what you can do:
1. backup your brnach `git checkout -b BRANCH-123_bak`
1. go back to your branch `git checkout -`
1. open a new console window to show all your commits `git log --grep=BRANCH-123 --online`
1. reset your brnach to the master `git reset --hard upstream/master`
1. cherry pick your commits `git cherry-pick 7c3b0ca` in case you have a range of commits you can do this with one command `git cherry-pick 7c3b0ca^..26aeeb8` add the `^` to include the first hash. 
1. resolve any conflicts in case there are
1. push your commits `git push --force origin BRANCH-123`
1. remove the backup branch if all was ok. 
