# Basics  

## Local  

The working tree is your current local folder. Every file added to the working tree won't be
tracked by default by git, it won't be staged.

To stage a file is to move it from untracked to tracked. To do so use command `git add <file>`.
This marks the file as new in the staged area.

Only the staged files will be commited (saved in the following snapshot).

To remove the file from the staged area use command `git restore --staged <file>`. This marks the 
file as untracked again and won't be commited.

If a file was previously commited (exists in a previous snapshot) and has been modified in the
working tree, you can restore the file to the commited version using the command
`git restore <file>`. Is the same command as removing a file from the staged area but without
the arg --staged.

Another way to revert a file to the previous version is to checkout the file from the snapshot
`git checkout <file>`.

A file can be created (marked as new) in the working tree, then added to the staging area
and modified again. Such file will be marked as new in the staging area and modified in the working
tree. Git doesn't track files, it tracks changes. So the moment you stage a new file you are
staging a STATE of that file. If it is then modified in the working tree but not staged again
the following commit will have the state in which was staged, the 'new' state. The modifications
will still be visible in the working tree but not in the snapshot.

`git status` shows the current status of every file (use alias `gst`).
`git log` shows a history of every commit (use aliases `glol` and `glola`).

To commit a file is to move it from stage to the master branch (default name). This creates a
new snapshot and changes the previously staged files status to 'unmodified'. Use the command
`git commit -m "<message>"` (or the alias `gcmsg "<message>"`).

`git diff` compares the modified lines in unstaged files vs staged files.
`git diff --staged` compares the modified lines in staged files vs the previous snapshot.

## Remote  

Remote repositories allows you to have versions of your project hosted on the internet. This allows
other people to contribute to the project.

To clone a repository use `git clone <repository url>`. This will get every file on the repo and
clone it (copy it) to your local directory.

To list all the remote repositories use `git remote`.
The additional arg `-v` shows the url of every remote.

To add a new remote to your current project use `git remote add <shortname> <url>`.

To get data from your remote project you can run `git fetch <remote>`. This command goes out 
to that remote project and pulls down all the data from that remote project that you don't 
have yet. After you do this, you should have references to all the branches from that remote, 
which you can merge in or inspect at any time.


