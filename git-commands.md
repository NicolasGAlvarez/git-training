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



