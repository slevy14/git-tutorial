## Introduction
This is a tutorial on the basics of using git for version control in the command line. Created for my Computer Science Junior Seminar, Spring 2024.
## Required Applications
This tutorial uses the default terminal on a computer running MacOS. Vim and Python3 are required to follow along with the tutorial. In my environment, Python3 is run using the command `python3`; if this doesn't work in yours, try `python`.
## Initializing a Project
We will be exclusively using the command line for this project. Let's start by creating the directory and files we will be working on, and initializing git.
### Create a directory
Open the "Terminal" application. You should be met with a blank window that looks like this (with your login information, not mine!): ![[new_window.png]]
Navigate to the directory you want your project to be stored in with `cd [FILEPATH]`, replacing `[FILEPATH]` with the path. Alternatively, you can stay in the home directory. Create a new directory at this location:
```shell
mkdir git-tutorial
```
And enter that directory:
```shell
cd git-tutorial
```
### Create a file
Now that we have a directory for our project, lets create a new file before initializing Git. Create a new python file:
```shell
touch hello.py
```
Next, we'll edit the file using Vim. Vim is a command line text editor that can do everything we need! Open the file with the following command:
```shell
vim hello.py
```
Press `i` to put vim in insert mode to start editing the file. Add the following line to the python file:
```python
print("hello!")
```
That's all we want to add for now, so let's exit Vim. Press `esc` to exit insert mode, then type `:wq` to save the file and exit Vim.
### Test the file
Let's see what this file does! In the command prompt, type:
```shell
python3 hello.py
```
You should see the following output:
```Output
hello!
```
### Initialize Git
Here's where the real fun begins. We'll initialize this project as a local git repository:
```shell
git init
```
Git is a version control system that allows us to save changes, track a project's history, create multiple feature branches, and much more. Let's take a deeper look at what we can do with git, how we can do it, and why.
## Committing Your Changes
Committing is how we save changes in git. Any files that are added, deleted, or edited are added to a list of changes to be committed. Commit your changes often and leave clear messages with them that describe what you changed. Let's make our first commit.
### Create an initial commit
In the command prompt, enter:
```shell
git status
```
This will give you a list of all staged changes (green) and unstaged/untracked changes (red). Notice that our file `hello.py` is currently untracked. This means that this file has not yet been part of a commit, and its changes are not being tracked by git. Let's add it to our commit:
```shell
git add hello.py
```
If you run `git status` again, you'll see that `hello.py` is now staged. Now let's make the actual commit:
```shell
git commit -m "initial commit"
```
We add our commit message as an argument to the command `git commit` by using `-m "MESSAGE"`. The message is just a label that explains what we did in the commit. In this case, "initial commit" works as the message, as we haven't yet done much.
### Edit a file
Let's edit our file a bit. Open up vim:
```shell
vim hello.py
```
Press `i` to insert, and add the following lines to the file just below the first print statement:
```python
print("io triumphe!")
print(9+10)
```
Hit `esc`, then `:wq` to save your work. You should see the following output:
```output
hello!
io triumphe!
19
```
### Commit your changes
Now that we've made some more changes, it's time to commit them. If you want to see which files are staged, you can run `git status` again. It's not necessary here, as we only made changes on one file, but this would be more useful if you had more files to track, or if wanted to make sure certain files were staged but not others, for example.   

Because we `hello.py` exists in a previous commit, it is no longer untracked. However, the changes we made to it are currently unstaged, so let's add them to the commit:
```shell
git add hello.py
```
Everything is staged, so let's commit:
```shell
git commit -m "added new print statements"
```
### Make more changes and commit
Let's make things a little more complicated for our next commit. Create a new file:
```shell
touch testing.py
```
And open it in vim:
```shell
vim testing.py
```
As before, press `i` to enter insert mode and add the following function:
```python
def secondfile():
	print("this function is from testing.py!")
```
Hit `esc` and type `:wq` to save the file. Back to `hello.py`, let's reopen it in vim and make some changes. Add the new lines to your code so it looks like this:
```python
import testing

print("hello!")
print("io triumphe!")
print(9 + 10)

testing.secondfile()
```
Run the file in the command prompt:
```shell
python3 hello.py
```
And it should produce the following output:
```Output
hello!
io triumphe!
19
this function is from testing.py!
```

If we run the command `git status`, you'll see that neither of the files are staged. Note that `testing.py` is untracked because it is new, but `hello.py` is tracked and unstaged. We can stage both of these files together with:
```shell
git add .
```
The `.` argument in place of a file name stages everything that is currently unstaged. Let's commit one more time:
```shell
git commit -m "created second file"
```
Remember to commit often! Git is just like any word processor or video game -- save often so you don't lose your work!
## Stashing and Branching
Git allows you to create multiple branches of commits for working on different features, experimenting, separating the work of different collaborators, and more. In this section, we'll look at how branches and stashing work.
### Make some changes
Reopen `testing.py` in Vim:
```shell
vim testing.py
```
Press `i` to insert, and add the following function beneath your print statement:
```python
def add_two_nums(a, b):
	return(a + b)
```
Hit `esc`, then `:wq` to save your work. Now, call this function from `hello.py` by reopening it in Vim:
```shell
vim hello.py
```
Append the following lines to the bottom of your code:
```python
a = 6
b = 15
print("the sum of", a, "and", b, "is", testing.add_two_nums(a, b))
```
Hit `esc`, then `:wq` to save your work. Run the file:
```shell
python3 hello.py
```
And you'll see the following output:
```Output
hello!
io triumphe!
19
this function is from testing.py!
the sum of 6 and 15 is 21
```
### Stash those changes
What if you don't actually want to commit those changes now? Let's stash the changes: this will remove the changes from the working tree, but save them to be restored later if you want. Run the following command:
```shell
git stash
```
After this, if you run `git status`, you'll see that the working tree is clean, despite the fact that we didn't commit these changes. In fact, if you run the file with `python3 hello.py`, you'll see that the last line of the output is missing. The files are reverted to their status at the previous commit without any edits. In a bit you will see why this is a necessary step before branching (in fact, git wont let you switch branches without a clean working tree).
### Make a branch
One reason to make a branch may be to make experimental changes without effecting the main branch. Make a new branch called "new-branch" to make some changes on:
```shell
git branch new-branch
```
Now that we have a new branch, run the command without any arguments to see a list of all branches:
```shell
git branch
```
The branch you are currently on will be highlighted. Creating a branch doesn't switch which branch you're on. Instead, you have to do that manually:
```shell
git switch new-branch
```
If we hadn't committed or stashed our previous changes, this command would fail. But we're one step ahead and already stashed everything, so this should work! Run `git branch` one more time if you want to confirm that you're on the correct branch.
### Make some changes and commit
- vim testing.py
- change line 2 to print("now we're on a new branch!")
- commit the changes
### Switch branches
- git switch master
### Make some changes and commit
- vim testing.py
- change line 2 to print("this is the main branch!")
- commit the changes
## Merging
### Merge new branch into main
- make sure you're on master
- git merge new-branch
- oh no! problems :(
	- notice that the issue is with testing.py
### Resolve conflicts
- vim testing.py
- choose which one we want to keep -- lets actually keep both
- save the file
- git add .
- git commit -m "resolved merge conflict, kept both lines"
### Restore changes from stash
- not part of merge, but lets restore from stash
- git stash pop
- notice how testing.py is different bc merges
- vim testing.py
- edit this however you want! i'll choose to keep everything
- git add .
- git commit -m "add stashed changes"
## Github
### Create repository on GitHub
- no readme, license, or gitignore
- copy remote repository URL
### Set up origin
- make sure you're in project directory
- git remote add origin REMOTE-URL
- confirm with git remote -v
### Push changes to GitHub
- first push is git push -u origin master
	- whatever is the name of the default branch, mine is master but sometimes its main
- everything else in the future is just git push
## Conclusion
And that's it! You should now have the tools to create both a local repository on your computer and a remote repository on GitHub.
## Quick Command Reference
A brief summary of all of the commands covered here, as well as a few more!   

`cd [DIRECTORY]` changes your current directory.   
`mkdir [DIRECTORY NAME]` creates a new directory at your current location.   
`touch [FILENAME]` creates a new file at your current location.   
`vim [FILENAME]` opens a file in Vim. Press `i` to enter insert mode, `esc` to exit, and `:wq` to save and quit. I use Vim here because it is the command line text editor that I'm most familiar with. For more information and a quick shortcut/command reference, check out https://vim.rtorr.com/.   
`python3 [FILENAME].py` runs a python file.   
<br>
`git init` creates a new local git repository at your current location.   
`git status` shows you the current status of your working tree: files that are untracked, changes that are staged and unstaged, etc.   
`git add [FILENAME]|.` stages the desired file, or stages all changes by using `.`.   
`git commit -m "MESSAGE"` creates a new commit on the current branch with the desired message.   
`git stash` saves all changes on the working tree without creating a new commit. This is necessary to switch branches without committing. `git stash pop` restores the most recently stashed changes to the working tree.   
`git branch [BRANCH NAME]` creates a new branch. Without the branch name, `git branch` lists all branches.    
`git switch [BRANCH NAME]` switches the working directory to the desired branch.
`git merge [BRANCH NAME]` merges a desired branch into the current branch. This is done by using the last commits from both branches as parent commits and attempting to combine them. Often, this will result in conflicts that can be solved using vim or another text editor.   
`git rebase [BRANCH NAME]` takes the commit history of one branch and effectively "replays" it onto the most recent commit of the current branch. This can also result in conflicts that the user must solve using vim or another text editor.   
`git log` shows you the full commit history of your project.   
`git log --graph` shows you the same information, but split into branches.   

