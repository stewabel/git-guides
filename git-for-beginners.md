# Git for beginners

## A quick intro

Git is a Distributed Version Control System (DVCS). It was originally conceived and developed for version control of the Linux kernel with the aim of being distributed, open source, high performance, and hard to corrupt. Since its inception in 2005, it became the prefered VCS for open source projects and subsequently has gained traction in the wider software community. A lot of this is down to Git's performance, reliability and flexibility. While Git can seem complex, and some of the more advanced features can have a steep learning curve, only a small subset of commands and techniques are needed in order make effective use of it.

## The aim of this guide

The intention of this guide is to provide the basic commands and techniques you need to know about, and explain how they work. Git was written for programmers by programmers, and an understanding of what is happening under the hood is key to fully understanding how to use it. We won't look into any advanced features, as it's important to get used to the basics first, if you really want to delve further than this guide, two resources I have found particularly useful in the past are the website http://think-like-a-git.net, and the book [Git In Practice](https://www.manning.com/books/git-in-practice)

## There's a repo on BitBucket/GitHub I want to work on

OK, so someone has already created a repo and shared it on a Git hosting site and we want to work on this for the first time. The command you need is `git clone [URI]`. If we navigate to the web interface for the repository on the Git hosting site, we will see an example git clone with the URI, for example `git clone git@github.com:stewabel/git-guides.git`.

`git clone [URI]` when run without any additional parameters will:
- Create a new directory named after the repository. In the example here, that would be `git-guides`.
- Clones the entire repository from the server into a sub directory named `.git`
- Checks out the `master` branch into the working directory.

## Branching

### Creating a new Branch

We've got a repo checked out, and now want to do some work. The first thing to do is to create and checkout a new branch. This can be done with the command `git checkout -b <branch-name>`.

The flag `-b` tells the checkout command you want to create a new branch. Following this command, you will have a new local branch and it will be checked out to your working directory.
