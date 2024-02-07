# Git Tutorial
## Instructions
Write a follow-along tutorial for CS students that teaches them how to use git from the command line. The tutorial should use a small coding project as the context for the reader to apply git commands, with the goal that students will be able to use git for their own projects afterwards. Your tutorial must cover the use of stashes and branches, and one of either rebasing or merging. You are not required to go into detail about git internals such as the commit graph, although you are also not prohibited from doing so; use your own judgment for how much detail to present given the goal of the tutorial.  
  
This assignment has no page constraints, and you are encouraged to include images and other supporting elements to make the tutorial easier to follow. Your tutorial should be submitted as a URL, such as a GitHub URL with a Markdown file that could be read online. If you want to use a different design for your URL, please speak with me.
## Introduction
This project is a tutorial on the basics of using git for version control. Created for my Computer Science Junior Seminar, Spring 2024.
## Initializing a Project
### Create a directory
- open terminal
- navigate to directory you want your project to be located in
- mkdir git-tutorial
- cd into that directory
### Create a file
- touch hello.py
- vim touch.py
- type print("hello!")
- hit escape, :wq
### Test the file
- python3 hello.py
	- (or python, however its configured in your environment)
- Should see output (photo)
### Initialize Git
- git init
## Committing Your Changes
### Create an initial commit
- git status
- git add hello.py
- git commit -m "initial commit"
### Edit a file
- vim hello.py
- add lines print("io triumphe!") and print(9+10)
- python3 hello.py
- Should see output (photo)
### Commit your changes
- git status
- git add hello.py
- git commit -m "added new print statements"

### Make more changes and commit
- create a new file, touch testing.py
- vim testing.py, create function
```python
def secondfile():
	print("this function is from testing.py!")
```
- vim hello.py, call function
```python
import testing

print("hello!")
print("io triumphe!")
print(9 + 10)

testing.secondfile()
```
- git add . (stages everything)
- git commit -m "created second file"
- commit often!!
## Stashing and Branching
### Make some changes
- vim testing.py, create new function
```python
def add_two_nums(a, b):
	return(a + b)
```
- vim hello.py, call new function (append to bottom)
```python
a = 6
b = 15
print("the sum of", a, "and", b, "is", testing.add_two_nums(a, b))
```
- run the file
- output as follows: (photo)
### Stash those changes
- we don't actually want to commit those changes now
- git stash, working tree is clean
### Make a branch
- git branch new-branch
- git branch (to see branches)
- git switch new-branch
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
## Vim
Vim is the command line text editor that I'm most familiar with, so it's what I use here. For more information and a quick shortcut/command reference, check out https://vim.rtorr.com/.
## Quick Command Reference
A brief summary of all of the commands covered here, as well as a few more!

`cd [DIRECTORY]` changes your current directory.
`mkdir [DIRECTORY NAME]` creates a new directory at your current location
`touch [FILENAME]` creates a new file at your current location.
`vim [FILENAME]` opens a file in Vim. I use Vim here because it is the command line text editor that I'm most familiar with. For more information and a quick shortcut/command reference, check out https://vim.rtorr.com/.
`python3 [FILENAME].py` runs a python file.

`git init` creates a new local git repository at your current location.
`git status` shows you the current status of your working tree: files that are untracked, changes that are staged and unstaged, etc.
`git add`
`git commit`
`git stash`
`git branch`
`git switch`
`git merge`
`git rebase`
`git log` shows you the full commit history of your project.
`git log --graph` shows you the same information, but split into branches.


