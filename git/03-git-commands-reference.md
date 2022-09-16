## Reverting commit 
#revert #git-commit
**Reverting a commit before push**
- To Only undo the last commit command but keep the other work: `git reset --soft HEAD~1`
- To revert your work and undo the last commit as well: `git reset --hard HEAD~1`

**Reverting commit after push**
- To revert last commit which is already pushed on remote branch: `git revert HEAD~1`
- To undo any commit use the commit hash id: `git revert <commit-hash-id>`

 ## Stashing a specific file
 - To stash a specific file `git stash push -m "stash-message" <file-with-complete-path-finename-with-ectension>`
 - In the above command `-m "stast-message"` is optional. It is used to add more description.

**Splitting commits**

If all files are added in a single commit by mistake, if you need to split them in to multiple commits
```
git rebase HEAD~
```

After this command you can commit the files you want grouping them or individually.

**Recovering Lost Files**
#Recovery
```
git restore -- <file-path>
```

This will also get the files that are removed from recycle bin

## Reverting commits from different branches
If you have committed last 2 commits in master instead of a feature branch. Perform the below commands in the same order.

```
//In master branch
git reset HEAD~2
git stash

//In feature branch
git checkout feature
git stash pop
```






