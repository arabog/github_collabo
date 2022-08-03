-: Forking A Repository
In version control terminology if you "fork" a repository that means you 
duplicate it. Typically you fork a repository that belongs to someone else. 
So you make an identical copy of their repository and that duplicate copy 
now belongs to you.

This concept of "forking" is also different from "cloning". When you clone a 
repository, you get an identical copy of the repository. But cloning happens 
on your local machine and you clone a remote repository. When you fork a 
repository, a new duplicate copy of the remote repository is created. This 
new copy is also a remote repository, but it now belongs to you.

If a repository doesn't belong to your account then it means you do not 
have permission to modify it.

This is where forking comes in! Instead of modifying the original repository 
directly, if you fork the repository to your own account then you will have 
full control over that repository.

to check for changes: `git diff`

-: Reviewing Existing Work
We can discover details about what other developers have done by using the 
extremely powerful `git log` command.

Group By Commit Author
A quick way that we can use to see how many commits each contributor has 
added to the repository is to use the `git shortlog` command:
$ git shortlog

git shortlog with the -s -n flags to show only the number of commits each 
author has made, sorted numerically.
$ git shortlog -s -n

Filter By Author
Another way that we can display all of the commits by an author is to use 
the regular `git log` command but include the --author flag to filter the 
commits to the provided author.
$ git log --author=Surma

If we wanted to see only the commits by Paul Lewis(in case dre is anoda Paul) 
we have to run:
$ git log --author="Paul Lewis"

Filter Commits By Search
Before going through this section on filtering by searching, I feel like I 
need to stress how important it is to write good, descriptive commit messages. 
If you write a descriptive commit message, then it's so much easier to search 
through the commit messages, later, to find exactly what you're looking for.

$ git show 5966b66

We can filter commits with the --grep flag.
How about we filter down to just the commits that reference the word "bug". 
We can do that with either of the following commands:

$ git log --grep=bug
$ git log --grep bug

-: Determining What To Work On (open source works)
The first thing you should always look for in a project is a file with the 
name CONTRIBUTING.md.

Recap
Before you start doing any work, make sure to look for the project's 
CONTRIBUTING.md file.
Next, it's a good idea to look at the GitHub issues for the project. look at 
the existing issues to see if one is similar to the change you want to contribute
if necessary create a new issue.
communicate the changes you'd like to make to the project maintainer in the issue
When you start developing, commit all of your work on a topic/named branch.

do not work on the master branch
make sure to give the topic branch clear, descriptive name

As a general best practice for writing commits.
make frequent, smaller commits
use clear and descriptive commit messages
update the README file, if necessary

-: Create a Pull Request
A pull request is a request to the original or source repository's maintainer 
to include changes in their project that you made in your fork of their project. 
You are requesting that they pull in changes you've made.

As long as you follow the steps we covered in the previous section on:
reviewing the project's CONTRIBUTING.md file
checking out the project's existing issues
talking with the project maintainer
...your pull request is sure to be included!

Recap
A pull request is a request for the source repository to pull in your commits 
and merge them with their project. To create a pull request, a couple of things 
need to happen:
you must fork the source repository
clone your fork down to your machine
make some commits (ideally on a topic branch!)
push the commits back to your fork
create a new pull request and choose the branch that has your new commits

-: Stay in sync with source project
Stars & Watching
If you want to keep up-to-date with the Repository, GitHub offers a 
convenient way to keep track of repositories - it lets you star 
repositories:

Watching A Repository
If you need to keep up with a project's changes and want to be notified of 
when things change, GitHub offers a "Watch" feature:

-: Including Upstream Changes
We're going to use the git remote command to add a new shortname and URL 
to this list. This will give us a connection to the source repository.

$ git remote add upstream https://github.com/udacity/course-collaboration-travel-plans.git

Remember that the names origin and upstream are just the default or de facto 
names that are used. If it's clearer for you to name your origin remote mine 
and the upstream remote source-repo, then by all means, go ahead and rename 
them. What you name your remote repositories in your local repository does 
not affect the source repository at all.

Using the git remote rename command to rename origin to mine and upstream 
to source-repo.
$ git remote rename origin mine
$ git remote rename upstream source-repo

Retrieving Upstream Changes
Now to get the changes from upstream remote repository, all we have to do 
is run a `git fetch` and use the upstream shortname rather than the origin 
shortname:
$ git fetch upstream master

Q: Now that you've added a connection to the new upstream remote repository, 
if you run `git fetch upstream master` will that update your forked repository 
on GitHub?
Ans: `git fetch` only updates the local repository. To update the project on 
GitHub, we'd need to push these newly acquired commits to our fork after 
merging it.

# to make sure I'm on the correct branch for merging
$ git checkout master

# merge in Lam's changes
$ git merge upstream/master

# send Lam's changes to *my* remote
$ git push origin master

Q: What single command would we use if we want to fetch the u
pstream/master changes and merge them into the master branch?
Ans: `git pull upstream master`

Remember from the lesson on remotes that a `git pull` is the same thing 
as a `git fetch` + `git merge`!

Recap
When working with a project that you've forked. The original project's 
maintainer will continue adding changes to their project. You'll want 
to keep your fork of their project in sync with theirs so that you can 
include any changes they make.

To get commits from a source repository into your forked repository on 
GitHub you need to:
get the cloneable URL of the source repository
create a new remote with the `git remote add` command
use the shortname upstream to point to the source repository
provide the URL of the source repository
`git fetch` the new upstream remote
`git merge` the upstream's branch into a local branch
`git push` the newly updated local branch to your origin repo

-: Squash(combine) Commits
To squash commits together, we're going to use the extremely powerful 
`git rebase` command. 

The Rebase Command
The git rebase command will move commits to have a new base. In the command 
`git rebase -i HEAD~3`, we're telling Git to use HEAD~3 as the base where all 
of the other commits (HEAD~2, HEAD~1, and HEAD) will connect to.

The -i in the command stands for "interactive". You can perform a rebase in 
a non-interactive mode. While you're learning how to rebase, though, I 
definitely recommend that you do interactive rebasing.

Ancestry References
As a brief refresher, HEAD indicates your current location (it could point 
to several things, but typically it'll either point to a branch name or 
directly to a commit's SHA). The ~3 part means "three before", so HEAD~3 
will be the commit that's three before the one you're currently on. We're 
using this relative reference to a commit in the git rebase command.

to force push
$ `git push -f origin main`

-: Force Pushing
Using git rebase creates a new commit with a new SHA. When I tried using 
`git push` to send this commit up to GitHub, GitHub knew that accepting 
the push would erase the three separate commits, so it rejected it. So 
I had to force push the commits through using git push -f.

Rebase Commands
Let's take another look at the different commands that you can do with git rebase:
use p or pick – to keep the commit as is
use r or reword – to keep the commit's content but alter the commit message
use e or edit – to keep the commit's content but stop before committing so that you can:
add new content or remove content or alter the content that was going to be committed
use s or squash – to combine this commit's changes into the previous commit (the commit 
above it in the list)
use f or fixup – to combine this commit's change into the previous one but drop the 
commit message
use x or exec – to run a shell command
use d or drop – to delete the commit

-: When to rebase
So you should not rebase if you have already pushed the commits you want to rebase. 
If you're collaborating with other developers, then they might already be working 
with the commits you've pushed. If you then use git rebase to change things around 
and then force push the commits, then the other developers will now be out of sync 
with the remote repository.

Inside the interactive list of commits, all commits start out as pick, but you can 
swap that out with one of the other commands (reword, edit, squash, fixup, exec, 
and drop).

I recommend that you create a backup branch before rebasing, so that it's easy to 
return to your previous state. If you're happy with the rebase, then you can just 
delete the backup branch!

https://up-for-grabs.net/#/
https://firstpr.me/#arabog
https://github.com/jlord/git-it-electron
https://github.com/search?utf8=%E2%9C%93&q=label%3Afirst-timers-only+is%3Aopen&type=Issues&ref=searchresults
https://www.firsttimersonly.com/