This tutorial has two sections: (1) Branches (2) Cheat sheet


# Branches

## Why Branches ?
To expand.
Trees need branches to expand. 
Banks needs (office) branches to expand.
Company needs (code) branches to expand.
E.g. Branches for Bugs, testing, featuers, production, staging etc. 

## What is a branch ?
Branch is a name given to the commit. Internally, it is pointer to the commit object.
By default, this name/pointer is **master**. Every time you make a new commit, this pointer moves forward.
When you create a new branch, new name/pointer is created to point to the current commit.
How does Git know which branch you are currently one ? It keeps a special pointer called **HEAD**.

## HEAD in the Git
 HEAD points to the tip of the "current branch". When you switch branches with `git checkout MyBranch` command, the HEAD starts to point to the tip of the new branch.
To see where the HEAD is pointing, run: `cat .git/HEAD` in your working directory. In my case, the output is:
```
$ cat .git/HEAD
ref: refs/heads/master
```
It is possible for HEAD to refer to a specific commit (revision) that is not associated with a branch name. This situation is called a detached HEAD.

## What is remote ?

If you're using Git collaboratively, you'll probably need to sync your commits with other machines or locations. In Git terminology, each machine or location is called a **remote**, and each one may have one or more branches. Most often, you'll just have one, named origin.
To list all the remotes, run
`$ git remote`

 To see which locations these remote names are shortcuts for, run
```
 $ git remote -v
 origin    https://github.com/unmeshvrije/leetcode
 origin    https://github.com/unmeshvrije/leetcode

 Each remote has a directory under git/refs/remotes/:
 $ ls -F .git/refs/remotes/
```

## Checkout

    The git checkout command lets you navigate between the branches created by git branch. Checking out a branch updates the files in the working directory to match the version stored in that branch, and it tells Git to record all new commits on that branch. Think of it as a way to select which line of development you’re working on.

To check out the specified branch, which should have already been created with git branch, run:
`git checkout <existing-branch>`
This makes <existing-branch> the current branch, and updates the working directory to match.

To create and check out <new-branch>, run
`git checkout -b <new-branch>`
    The -b option is a convenience flag that tells Git to run git branch <new-branch> before running git checkout <new-branch>.

## Pushing the new local branch to remote Git repository
`git checkout -b feature` creates and switches to a new branch **feature**
`git push -u origin feature` will create the equivalent remote branch and push the changes from local **feature** branch.

## Types of Branches

On your local machine, you've got three types of branches:
 1. local non-tracking branches
 2. local tacking branches (that often track remote tracking branch)
 3. remote-tracking branches (local copy of the remote branch)

On a remote machine, you have just one type of branch called **remote branch**.


### 1 Local branches 

 To view a list of all the local branches on your machine, run
```
$ git branch
 master
 new-feature

 Each local branch has a file under .git/refs/heads/:
 $ ls -F .git/refs/heads/
 master new-feature
```

 There are two types of local branches on your machine: non-tracking local branches, and tracking local branches.
#### 1.1 Non-tracking local branches 
  Non-tracking local branches are not associated with any other branch. To create one, run 
`$ git branch <branchname>`

#### 1.2 Tracking local branches 
Tracking local branches are associated with another branch, usually a remote-tracking branch. To create one, run 
`$ git branch --track <branchname> [<start-point>]`

To view which one of your local branches are tracking branches, run
```
  $ git branch -vv
  master      b31f87c85 [origin/master] "my sample commit"
  new-feature b760e04ed "my branch is strong"
```
From this command's output, you can see that the local branch master is tracking the remote-tracking branch origin/master, and the local branch new-feature is not tracking anything.

"Tracking local branches" are useful. They allow you to run git pull and git push, without specifying which upstream branch to use. If the branch is not set up to track another branch, you'll get an error like this one:
```
  $ git checkout new-feature
  $ git pull
  There is no tracking information for the current branch.
  Please specify which branch you want to merge with.
  See git-pull(1) for details
  $ git pull <remote> <branch>
```
  If you wish to set tracking information for this branch you can do so with:

`$git branch --set-upstream new-feature <remote>/<branch>`

### 2. Remote-tracking branches (still on your machine)

A remote tracking branch is a local copy of a remote branch.
  To view a list of all the remote-tracking branches on your machine, run
```
  $ git branch -r
  bitbucket/master
  origin/master
  origin/new-branch
```
  Each remote-tracking branch has a file under .git/refs/<remote>/:
```
$ tree -F .git/refs/remotes/
  .git/refs/remotes/
  ├── bitbucket/
  │   └── master
  └── origin/
  ├── master
  └── new-branch
```

  Think of your remote-tracking branches as your local cache for what the remote machines contain. You can update your remote-tracking branches using git fetch, which git pull uses behind the scenes.
  Even though all the data for a remote-tracking branch is stored locally on your machine (like a cache), it should never be called a local branch. It's just called a remote-tracking branch.

## Branches on a remote machine:
    To view all the remote branches (that is, the branches on the remote machine), run
```    
    $ git remote show origin
    *remote origin
    Fetch URL: git@github.com:Flimm/example.git
    Push  URL: git@github.com:Flimm/example.git
    HEAD branch: master
    Remote branches:
    io-socket-ip            new (next fetch will store in remotes/origin)
    master                  tracked
    new-branch              tracked
    Local ref configured for 'git pull':
    master     merges with remote master
    new-branch merges with remote new-branch
    Local ref configured for 'git push':
    master     pushes to master     (up to date)
    new-branch pushes to new-branch (fast-forwardable)    
```
    This git remote command queries the remote machine over the network about its branches. It does not update the remote-tracking branches on your local machine, use git fetch or git pull for that.
    From the output, you can see all the branches that exist on the remote machine by looking under the heading "Remote branches" (ignore lines marked as "stale").

    If you could log in to the remote machine and find the repository in the filesystem, you could have a look at all its branches under refs/heads/.


## Merging the changes from a branch
To merge the changes from say branch `new-branch`, you cannot be on the `new-branch` itself.
You have to checkout say a `master` branch with `git checkout master`.
To confirm that you are on the master branch
```
$git branch
*master
new-branch
```
In this `*` indicates that you are currently on the `master` branch.
`git merge new-branch` will then merge the latest commit from the `new-branch` into `master` branch.

# Cheat sheet:
1. To delete a local branch, whether tracking or non-tracking, safely:
`git branch -d <brachname>`
2. To delete a local branch, whether tracking or non-tracking, forcefully:
`git branch -D <branchname>`
3. To delete a remote-tracking branch:
`git branch -rd <remote>/<branchname>`
4. To create a new local non-tracking branch:
`git branch <branchname> [<start-point>]`
5. To create a new local tracking branch: (Note that if <start-point> is specified and is a remote-tracking branch like origin/foobar, then the --track flag is automatically included)
`git branch --track <branchname> [<start-point]`
Example:
`git branch --track hello-kitty origin/hello-kitty
6. To delete a branch on a remote machine:
`git push --delete <remote> <branchname>`
7. To delete all remote-tracking branches that are stale, that is, where the corresponding branches on the remote machine no longer exist:
`git remote prune <remote>`
8. To check the status of the git repository. (which files are staged, added to the commit, etc.)
`git status`
9. To see the log of previous 'n' commits,
`git log -n`
10. To restore the file <filename> to the version of latest commit
`git checkout -- <filename>`
11. To see the difference between the local repository and the latest commit (HEAD)
`git diff [filename]`
12. THIS IS DANGEROUS!!: To remove the file from both working directory and git
`git rm`
13. To remove the file from git tracking, but still keep it in the working directory:
`git rm --cached`

    You may have noticed that in some commands, you use <remote>/<branch>, and other commands, <remote> <branch>.

    Examples: git branch origin/hello-kitty and git push --delete origin hello-kitty.
    It may seem arbritrary, but there's simple way to remember when to use a slash and when to use a space. When you're using a slash, you're referring to a remote-tracking branch on your own machine, whereas when you're using a  space, you're actually dealing with a branch on a remote machine over the network.
