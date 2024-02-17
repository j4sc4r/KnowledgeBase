# Git commands

| Command  | Parameters                                                             | Usage                                                                                         |
|:-------- | ---------------------------------------------------------------------- |:--------------------------------------------------------------------------------------------- |
| init     | `git init`                                                             | Initializes a new Git repository in a directory                                               |
| clone    | `git clone 'URL'`                                                      | Copies an existing repository into a new directory                                            |
| add      | `git add 'file'`                                                       | Adds files or changes to the index to prepare them for committing                             |
| commit   | `git commit -m "comment"`                                              | Stores the current index changes permanently in the repository                                |
| push     | `git push origin 'branch'`                                             | Transfers local commits to a remote repository                                                |
| pull     | `git pull origin 'branch'`                                             | Updates the local branch with changes form a remote repository                                |
| merge    | `git merge 'branch'`                                                   | Incorporates changes from another branch into the current branch                              |
| rebase   | `git rebase 'base branch'`                                             | Moves or "rebases" commits onto a different base point                                        |
| fetch    | `git fetch origin`                                                     | Downloads changes from a remote repository without merging them with the local branch         |
| diff     | `git diff 'source' 'target'`                                           | Shows differences between commits, working copy and index                                     |
| restore  | `git restore 'file'`                                                   | Resets modified files to the state of the last commit                                         |
| reset    | `git reset 'commit'`                                                   | Resets the index and/or the working copy to a specific commit                                 |
| mv       | `git mv 'old file' 'new file'`                                         | Moves or renames a file and reflects the change in Git                                        |
| rm       | `git rm 'file'`                                                        | Removes files from the index and the filesystem                                               |
| log      | `git log`                                                              | Displays a chronological list of commits                                                      |
| show     | `git show 'commit'`                                                    | Shows information about a specific commit or object                                           |
| status   | `git status`                                                           | Shows the status of the working copy and the index                                            |
| branch   | `git branch` or `git branch 'branch name'`                             | Displays, creates, or deletes branches in the repository                                      |
| checkout | `git checkout 'branch'` or for a new branch `git checkout 'branch' -b` for a specific commit `git checkout 'commit`  | Command allows switching between different branches or restoring files from a specific commit |
| switch   | `git switch 'branch'`                                                  | Switches between different branches or creates and switches to a new branch                   |
