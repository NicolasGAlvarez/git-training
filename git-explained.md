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


## Branching  

Git doesn't store data as a series of changesets or differences, but instead as a series of
snapshots. When you make a commit, git stores a commit object that contains a pointer to the 
snapshot of the content you staged.

Let's assume that you have a directory containing three files, and you stage them all and commit.
Staging the files computes a checksum for each one (SHA-1 hash), stores that version of the file
in the git repository, and adds that checksum to the staging area.

When you create the commit, git checksums each subdirectory and stores them as a tree object in the
git repository. Git then creates a commit object that has the metadata and a pointer to the root
project tree so it can re-create that snapshot when needed.

Your git repository now contains five objects: three blobs (one checksum for each file), one tree
that lists the contents of the directory and specifies which file names are stored as which blob,
and one commit with the pointer to that root tree and all the commit metadata.

If you make some changes and commit again, the next commit stores a pointer to the commit that
came immediately before it.

A branch in git is simply a lightweight movable pointer to one of these commits. The default
branch name in git is `master`. As you start making commits, you're given a `master` branch that
points to the last commit you made. Every time you commit, the `master` branch pointer moves
forward automatically.


### Creating a new branch

What happens when you create a new branch? Well, doing so creates a new pointer for you to move
around. Let's say you want to create a new branch called `testing`. You do this with the
`git branch` command: `git branch testing`. This creates a new pointer to the same commit you're 
currently on.

How does git know what branch you're currently on? It keeps a special pointer called `HEAD`.

Becaus a branch in git is actually a simple file that contains the 40 character SHA-1 checksum
of the commit it points to, branches are cheap to create and destroy. Creating a new branch is
as quick and simple as writing 41 bytes to a file (40 characters and a newline).

Use `git switch <branch>` to switch to an existing branch.

Create a new branch and switch to it `git switch -c <branch>`.

Return to your previously checked out branch `git switch -`.


### Merging branches

To merge a branch first switch to the branch your are gona merge into,
in this case the master branch `git checkout master`. And then do a merge 
`git merge <branch to merge>`. 

If the new content does not conflict with the data already on master, git will 
`auto-merge`. That is, it will add the new content to the already created files.

In case of conflic, git will create a warning and wait for the user to manually resolve
conflicts in each file. You can open every file with vsCode and make use of the options
above each conflict: either accept the incoming data or keep the old one.

Once finished you can check `git status` and see which files need to be added 
`git add <file>` and lastly commited `git commit`. Doing so will open the default editor
and wait for a message just like when commiting. Once closed the editor git finishes
the merge.