+++
date = "2017-08-22"
title = "Fork, Branch, and Pull - A Concise Git Workflow"
description = ""
author = "Yudy Chen"
tags = [ "git" ]
categories  = [ "Development"]
slug = "concise-git-workflow"
+++


Here’s a super concise workflow for contributing to an existing Github project. In this guide, you will learn how to fork a project, branch a new feature or big fix, and contribute to the original project.
<br><br>
  
### **Initial Steps: Fork, Clone, and Add Upstream**
Head over to the Github page you want to contribute to and click the “Fork” button. Copy the url to your forked repository and then from the command line:
```bash
$ git clone https://github.com/<username>/<forked_repo>.git
```

Track the original upstream repository, by adding a remote and then verifying:
```bash
$ git remote add upstream https://github.com/<original_repo>.git
$ git remote -v
```
<br>

### **Stay in Sync with Upstream**
If you just did the above steps, you can create a branch and start working. Otherwise, it is a good idea to make sure you are up-to-date with the upstream repo’s latest commits.
Fetch upstream and view all branches
```bash
$ git fetch upstream
$ git branch -va
```
You then want to checkout your master branch and merge it with the upstream repo:
```bash
$ git checkout master
$ git merge upstream/master
```
You should not have any unique commits on the local master branch (since in this guide, we are doing commits against a separate branches). So git should perform a fast-forward and bring your local master branch up-to-date.
<br><br>

### **Branch and Start Working**
Before creating a branch, it is always nice to make sure you are branching from your local master. So first run:
```$ git branch```, to see if you are on the master branch, and if not: ```$ git checkout master```

Now create a new branch and check it out:
```bash
$ git branch newfeature
$ git checkout newfeature
```
Now you can make changes using the normal Git workflow with ```$ git add``` and ```$ git commit```
<br><br>

### **Refetch, Merge, Rebase, and Squash**
If this is a quick change, you can get away without doing this. But it is nice to ensure your local master branch is up-to-date with the upstream repo. As before:
```bash
$ git fetch upstream
$ git checkout master
$ git merge upstream/master
```
This brings your local master up-to-date with the upstream repo. And if any new commits were made upstream, you can now rebase them. This means the upstream repo's commits will be applied first, with your newfeature branch's commits *re-played* after the aforementioned upstream commits. This will make your eventual pull request much easier for the developer to review and merge. Here are the commands: 
```bash
$ git checkout newfeature
$ git rebase master
```
It is also a good idea to squash your smaller commits into a larger one:
```bash
$ git rebase -i
```
This will bring up an editor where you can squash your commits. If you had 3 commits, you might see something like this:
```bash
pick 01d1124 Commit Msg 1
pick 6340aaa Commit Msg 2
pick ebfd367 Commit Msg 3
```
... If you want to squash these commits into a single one, you might do something like this:
```bash
pick 01d1124 Commit Msg 1
squash 6340aaa Commit Msg 2
squash ebfd367 Commit Msg 3
```
... which will lead you to another editor where you can edit the commit message to something that describes all the changes made. **A good commit message should have a title/subject in imperative mood starting with a capital letter and no trailing period.**
<br><br>

### **Push, Pull, and Delete**

Now push your changes to your repository:
```bash
$ git push origin new-feature
```
You can then go to your forked repository on Github, find your branch and make a pull request. You can review the changes before you submit it. If the upstream repo's owner approves and merges it, Github will prompt you to delete your branch, which is safe to do now. Remember your forked master is now out-of-date and requires a fetch, checkout, and merge (see earlier step), which updates your local repository. Then do another push to update your remote forked repository. 

