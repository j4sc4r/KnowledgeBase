# Git stages 

## Local 

Git has three main stages to get your changes saved locally.

![[git_stages.png | width=150%]]

## Remote

Git has a fourth stage when you want to save your repository online/remote.

![[git_stages_with_remote.png | width=150%]]

## Step by step explaination

What the commands mean is here [[Commands]]

   - Clone or Init a Repository
 ```bash
   git clone <URL> 
   git init
```

   - Change to the cloned branch if necessary
   ```bash
   git checkout <branch>
   ```
- if not necessary go on with working in the repository or in the working directory
- finished with work add modified files in the staging area
```bash
git add <file> or <.>
```
- use the "." when you want to add the whole directory
- see if any changes are not added 
```bash
git status
```
- if added commit the staged files in the local repository with a comment
```bash
git commit -m "comment"
```
- if you want to upload the commits to a remote repository push the repository 
```bash
git push origin <branch>
```
- when you need changes from a remote repository into your working directory on the local machine use the pull command
```bash
git pull origin <branch>
```