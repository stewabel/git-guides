# Git for beginners

## A quick intro

Git is a Distributed Version Control System (DVCS). It was originally conceived and developed for version control of the Linux kernel with the aim of being distributed, open source, high performance, and hard to corrupt. Since its inception in 2005, it became the prefered VCS for open source projects and subsequently has gained traction in the wider software community. A lot of this is down to Git's performance, reliability and flexibility. While Git can seem complex, and some of the more advanced features can have a steep learning curve, only a small subset of commands and techniques are needed in order make effective use of it.

## The aim of this guide

The intention of this guide is to provide the basic commands and techniques you need to know about, and explain how they work. Git was written for programmers by programmers, and an understanding of what is happening under the hood is key to fully understanding how to use it. We won't look into any advanced features, as it's important to get used to the basics first, if you really want to delve further than this guide, two resources I have found particularly useful in the past are the website http://think-like-a-git.net, and the book [Git In Practice](https://www.manning.com/books/git-in-practice)

## Cloning a repo from BitBucket/GitHub

OK, so someone has already created a repo and shared it on a Git hosting site and we want to work on this for the first time. The command we need is `git clone [URI]`. If we navigate to the web interface for the repository on the Git hosting site, we will see an example git clone with the URI, for example `git clone git@github.com:stewabel/git-guides.git`.

`git clone [URI]` when run without any additional parameters will:
- Create a new directory named after the repository. In the example here, that would be `git-guides`.
- Clones the entire repository from the server into a sub directory named `.git`
- Sets a remote repository link named `origin`
- Checks out the `master` branch into the working directory.

## Branching

### Creating a new Branch

We've got a repo checked out, and now want to do some work. The first thing to do is to create and checkout a new branch. This can be done with the command `git checkout -b <branch-name>`.

The flag `-b` tells the checkout command we want to create a new branch. Following this command, we will have a new local branch and it will be checked out to the working directory.

### Pushing a branch to the remote repository

At this point in time, the new branch only exists on the local machine. Once you've added some commits, we are ready to push up to the remote repository in order to open a pull request. The command to push is `git push`, however running that command will result in an error:
```
$ git push
fatal: The current branch <branch-name> has no upstream branch.
To push the current branch and set the remote upstream, used

  git push --set-upstream origin <branch-name>
```
This is due to how git handles branches, when a new branch is created locally there is no equivalent branch on the remote repository to push the changes to, and no local tracking branch. So we can do as git suggests and use the flag `--set-upstream` or `-u` specifying which remote repository (origin) and the name of the branch we are pushing.

Now we have a new branch on the remote repository which matches our local branch. We can continue adding commits to the local branch, these commits will not be on the remote branch, our local branch is 'ahead' of the remote branch. This time round, as our local branch is already configured to know where the upstream branch is, we can simply use `git push`.

### Checking out an existing branch

First of all, run a `git fetch` to ensure you have all the latest changes from the origin repository. Then `git checkout <branch-name>`. If this is not the first time you have checked this branch out, run `git merge` to ensure your local branch is up to date.


## Getting changes from the remote repository

A PR has been raised and merged into master on the Git hosting site, so how do we get those changes locally? The most forward way is pull the changes. In order to do that we first need to checkout the master branch:

```
$ git checkout master
```

This updates our working directory to our local copy of the master branch, if we now pull

```
$ git pull
```

then we will have retrieved the changes to master which are in the remote repository, merged them into our local master branch, and checked out the new HEAD of the master branch into our local working directory. Thats quite a lot of things happening with that simple `push` command, lets explore in some more detail

Essentially `git pull` combines a couple of commands; `git fetch` and `git merge`, let's take a look at these commands.

### fetch
The first stage of git pull is to fetch changes from the remote repository into our local repository. At this point the local copy of the branch is not yet updated, but the commits have been fetched for all branches.

### merge
The next stage is to merge the changes into our local branch. We are now up to date. The reason a merge is performed is that there could be a situation where we have added commits to our local branch which don't yet exist on the remote branch.

## Adding commits

After adding, making changes to or deleting files, the changes will not yet have been tracked by git. We need to add the changes to the staging area. In effect, the staging area is essentially a temporary branch which allows you to prepare a commit before adding it to the repository. We then commit the changes to the currently checked out branch, and we can then push to the remote repository following the procedure above.

The outline of the steps is:
- Ensure you have checked out the branch you intend to commit to
- Add the changes to the staging area
- Commit to the branch

To add all changes to the staging area, the simplest approach is to ensure we are in the root folder of the repository and then run
```
$ git add .
```

All changes will be now staged. Next commit
```
$ git commit -m "<commit message>"
```

Be aware that at this point in time, the changes are only committed in our local repository, if we are ready, we can now push the changes to the remote or continue adding subsequent commits.

At any point in time, to see what changes are pending, we can run `git status` resulting in an output similar to the following:
```
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git-for-beginners.md

no changes added to commit (use "git add" and/or "git commit -a")
```

## Digging deeper into git commands
The git manual can be accessed from the command line by running `man git`.

Detail for a specific git command can be found by running `git <command> --help`
