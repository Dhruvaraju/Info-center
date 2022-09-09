## how to push an existing local repo to remote repo?
#git 
Creating a git repo locally and pushing it to hit hub:

```
echo "# prime-services-springboot-java-alpha" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/Dhruvaraju/prime-services-springboot-java-alpha.git
git push -u origin main

```

## Adding existing repo to git-hub
```
git remote add origin https://github.com/Dhruvaraju/prime-services-springboot-java-alpha.git
git branch -M main
git push -u origin main

```

## For Allowing unrelated histories
```
git pull origin main --allow-unrelated-histories

```