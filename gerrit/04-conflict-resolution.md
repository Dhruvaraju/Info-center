### Rebase
Rebase is a utility that specializes in integrating changes into a branch. It does this by taking the commits from your current branch or change of your reference and creating new commits on the head of the destination branch, that will apply the changes. Rebasing will help you to submit change reviews that cannot be merged due to conflicts.

- [ ] When a conflict occurs, to rebase a change got to the change >> Click on download >> select the command from download section.
- [ ] In the destination branch do a git pull to get most recent code
- [ ] Run the `git fetch` command copied from download option
- [ ] Perform `git rebase` on destination branch example : `git rebase origin/master`
- [ ] It might fail with few conflicts, resolve those conflicts 
- [ ] Add the updated files to using `git add <<file_name>>` or `git add .`
- [ ] Continue git rebase with `git rebase --continue`
- [ ] Once done push the changes `git push origin HEAD:refs/for/master` if the destination branch is master
- [ ] Now the change will be updated with a patch set which can be reviewed and approved for merge.

### Cherry-pick
Cherry-pick is a utility that allows you to pick out a specific permit reference from a change of view or another branch and apply it to the destination branch. Cherry picking will help you to submit a change that is dependent on another change by picking out that specific reference.