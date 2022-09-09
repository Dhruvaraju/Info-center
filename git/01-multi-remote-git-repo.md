## Adding multiple Remotes for same git repo
Generally a git repo will have a single remote but it is possible to add multiple remotes, if we want to push same code to multiple remote repositories (Can be hosted on different providers.).

Clone a git repo from any provider. To see the remotes associate to a git repo use `git remote -v` . Adding a git remote for a repo which do not have a remote can be done using command `git remote add origin <remote repo url>`.
An example remote addition
`git remote add origin https://github.com/Dhruvaraju/prime-services-springboot-java-alpha.git`

When we try to use the same command again like `git remote add origin <remote repo url>` it will throw an exception showing remote already present. To add a new remote change the name of it `git remote add <new_name> <new_remote_url>`

**Example:**
```
git remote add new-origin https://www.gerrit.com/alpha-project
```

Now to push code to new remote `git push new-origin master`

> [!Note] Naming
> Instead of new-origin or origin we can use any text, but while pushing and pulling use the same name

