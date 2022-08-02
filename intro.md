Expected Knowledge
creating repositories with git init and git clone
reviewing repos with git status
using git log and git show to review past commits
being able to make commits with git add
commit them to the repo with git commit
you need to know about branching, merging branches together, and resolving merge conflicts
and being able to undo things in Git:
    git commit --amend to undo the most recent commit or to change the wording of the commit message
    and git reset If you're comfortable with all of these, then you'll be good to go for this course.

-: Remote Repositories:
So when you're collaborating with other developers make sure to create a new branch that has a descriptive name that describes what changes it contains.

A local repository is the one that you work on in your local machine. Remote repositories live elsewhere (e.g. a friend's computer, GitHub, etc.)

The way we can interact and control a remote repository is through the Git remote command:
$ git remote

A local repository can be connected to more than one remote repository.

-: Add A Remote Repository
The word "origin" is the defacto name that's used to refer to the main remote repository.

If you want to see the full path to the remote repository, then all you have to do is use the -v flag:
$ git remote -v


Let's take a look at the commits that I have in my Repository.
git log --oneline --graph --decorate --all

To send local commits to a remote repository you need to use the git push command.
e.g
git push -u origin main

-: Connecting to GitHub with SSH
https://docs.github.com/en/authentication/connecting-to-github-with-ssh

The output includes the shortname and the full URL that it refers to.

The git push command is used to send commits from a local repository to a remote repository.

$ git push origin master
The git push command takes:

the shortname of the remote repository you want to send commits to
the name of the branch that has the commits you want to send

-: Pulling Changes From A Remote
If you don't want to automatically merge the local branch with the tracking branch then you wouldn't use git pull you would use a different command called git fetch. You might want to do this if there are commits on the repository that you don't have but there are also commits on the local repository that the remote one doesn't have either.

When git pull is run, the following things happen:
    the commit(s) on the remote branch are copied to the local repository
    the local tracking branch (origin/master) is moved to point to the most recent commit
    the local tracking branch (origin/master) is MERGED into the local branch (master)

-: Pull vs Fetch
Git fetch is used to retrieve commits from a remote repository's branch but it does not automatically merge the local branch with the remote tracking branch after those commits have been received.

When git fetch is run, the following things happen:

the commit(s) on the remote branch are copied to the local repository
the local tracking branch (e.g. origin/master) is moved to point to the most recent commit
The important thing to note is that the local branch does not change at all.

You can think of git fetch as half of a git pull. The other half of git pull is the merging aspect.

One main point when you want to use git fetch rather than git pull is if your remote branch and your local branch both have changes that neither of the other ones has. In this case, you want to fetch the remote changes to get them in your local branch and then perform a merge manually. Then you can push that new merge commit back to the remote.


