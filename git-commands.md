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




