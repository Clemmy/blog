---
title: "'Gitting' it Right"
tags: [git, technology]
---

Hello my fellow readers! It's great to post again, and I must say I apologize for being out of touch for so long. I actually started writing this blog post in the middle of my work term at Ten Thousand Coffees, but I delayed it for a while after becoming a bit caught up in work. Without any further ado, let's get to the main content:

For a while now, I have been using Git, but I haven't been _using_ Git (the right way). Instead, I adopted a push/pull flow similar to how central repositories like SVN work. However, thanks to a mandatory training camp I had to undertake during the first week of my co-op term at Ten Thousand Coffees, I did my research on Git and now appreciate its power, and have been using it ever since. Ever since I began 'Gitting it right', I have stopped being afraid of large code changes permanently breaking code, crossing my fingers that my teammates didn't make painfully conflicting changes, and working on multiple different features at once. Instead, Git has significantly improved my programming productivity and helps me dive into problems with the confidence that I can easily navigate around the Git tree and rollback/jump through different stages in the commit history. In fact, I am terrified to write anything without version control now, and evidently, I chose to put both my resume and report under version control in order to utilize powerful Git features such as diffing, comparing revisions, and seeing all the changes I have made.

As a starting point, I personally found Atlassian's set of [tutorials](https://www.atlassian.com/git/tutorials/) to be among the most clear, simple, and concise. It gave me a solid foundation for a majority of the Git statements that I use on a daily basis, and only takes a few hours to read through. Additionally, there's a cool [interactive git tutorial](http://pcottle.github.io/learnGitBranching/).

After understanding the fundamentals of Git, I learned that there were two major workflows for Git. Certain people use the "Rebase workflow", while a vast majority use the "Git Flow workflow". They both have their own specific use cases, where a rebase workflow is focused on having a clean, linear history, and a merge workflow is more concerned about the preservtion of history. In practice, I have mainly used a "Git Flow workflow", but more details about a rebase workflow can be found [here](http://randyfay.com/content/rebase-workflow-git).

#Git Flow
The Git Flow is a branching model is in broad, a strategy for organizing Git commits and branches in such a way that it is easy for the team to develop in parallel. It consists of a two infinitely long main branches:

- a master branch (where the HEAD always reflects a production ready state)
- a development branch (where developers branch out onto feature branches, and develop until the next deploy)

The model also consists of shorter branches known as:

- feature branches (branches off development, and merged back to development, these branches contain commits related to a new feature)
- hotfix branches (branches off master, that are merged back into development and master, these branches fix bugs that are found in production code)

For more details, read about Git Flow [here](http://nvie.com/posts/a-successful-git-branching-model/).

#Some git commands I use regularly
Throughout my several months of using Git, I noticed that there were several commands I used very often.

- ```git checkout <file> <commit_id>``` which grabs a file from a specific revision
- ```git checkout -- .``` which replaces all unstaged changes with the corresponding files from the previous commit
- ```git reset --hard <commit_id>``` which moves your local HEAD to the specified commit_id. It's useful when you want to move your HEAD to a diverged commit, or when you bring you make a bad commit locally.
- ```git add <file>``` which simply adds a changed file to the stage area
- ```git fetch``` which grabs data about the git repository from the specified remote, and can be followed by a ```git pull``` or ```git rebase``` to update your local repo
- ```git status``` which displays status about your repository, such as what files are staged, unstaged, and your HEAD's position relative to the tracked repository
- ```git pull --ff``` which, after fetching, can merge the remote changes into your local repository without a merge commit.
- ```git merge``` to merge one branch with another
- ```git rebase -i``` which allows you to ammend commits, break up commits into multiple commits, squash multiple commits into one, and reorder the application of commit diffs. It is a very powerful feature which allows you to organize your git commits locally before pushing, and can make the difference between [this](images/in_post_images/clean-git-tree.png) and [this](images/in_post_images/messy-git-tree.png).
#Some other cool git stuff
-imerge
-git flow cli
- git rerere
I recommend a git GUI as well as a mergetool (for 3 way merging, as opposed to a 2 way merge)


#One of my craziest experiences with Git
One of the tasks I was assigned to do at my company was to split a repository of ~6000 commits into 2 repos: server and client repositories, while retaining the branch structures and history.
patch
diff
idk
set somehting as something

They say, know your tools well.
-git flow
-git rerere,/imerge

<!--end-->
