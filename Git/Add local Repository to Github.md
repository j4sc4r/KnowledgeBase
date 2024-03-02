# Add local Repository to Github

## Create local repository 

- go into new directory
```bash 
git init
```

## Add and commit first files

- after adding the first files 

```bash 
git add <files>

git commit -m "<commit message>"
```

## Create remote repository 

- create new repository on [Github](https://github.com)

## Add remote repository

```bash 
git remote add origin <URL e.g. https://github.com/username/repository.git>
```

## Push local repository to remote repository

```bash
git push <remote branch> <local branch>

#example
git push origin main
```

## Common errors

### `error: src refspec main does not match any` 

- create or rename branch as the provided branch is not in the local repository 
```bash
# lookup the branches
git branch 

# change branch
git checkout <branch>

# change name of current branch
git branch -m <new name>
```

### fatal: refusing to merge unrelated histories

- if remote repository has not the same history or file as the local repository it will not push the new files 
```bash
#merge both histories
git pull <remote branch> <local branch> --allow-unrelated-histories

#push the new files
git push <remote branch> <local branch>

# example
git push origin main
```