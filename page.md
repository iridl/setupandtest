Testing SourceTree

First commit from the data server!
Second commit.
Third commit
Xyz

= When you need help with Git and/or Bitbucket

* Open an issue at https://bitbucket.org/ikh/setupandtest/issues/new
* Also feel free to contact <<user ikh>> at ikh@iri.columbia.edu 

= Install Git software

Open a terminal session and check if you have Git command line tools on your system:

{{{
$ git --version 
git version 1.7.9.1
}}}

If you have Git 1.7+, then you do not need to install Git Command line tools. 

== Mac

* Git command line:  https://bitbucket.org/ikh/setupandtest/downloads/git-1.7.9.1-intel-universal-snow-leopard.dmg
* Git GUI: https://bitbucket.org/ikh/setupandtest/downloads/GitXStable.app.zip

= Introduce yourself to Git

Introduce yourself to Git with your name and public email address. This information will be recorded in Git repository when you commit your changes. The easiest way to do so is:

{{{
$ git config --global user.name "Your Name"
$ git config --global user.email "you@iri.columbia.edu"
}}}

Alternatively, you may add this information to {{{~/.gitconfig}}} as follows: 

{{{
[user]
       name = Your Name
       email = you@iri.columbia.edu
}}}

Make sure to repeat this setup for all your home directories (Mac, Linux, etc.) 

= Generate and setup certificate

1. Generate:
{{{
$ ssh-keygen -f ~/.ssh/bitbucket -t rsa -C "you@iri.columbia.edu"
}}}
2. Set up certificate at https://bitbucket.org/account/ssh-keys/ as follows:
* Set {{{Label}}} field to {{{you@iri.columbia.edu}}} 
* Copy/paste the contents of {{{~/.ssh/bitbucket.pub}}} to {{{SSH Key}}} field 
* Press {{{Add key}}}

3. Run {{{ssh -i ~/.ssh/bitbucket.pub git@bitbucket.org}}}. You should see something like this:

{{{
ssh -i ~/.ssh/bitbucket.pub git@bitbucket.org
. . .
You can use git or hg to connect to Bitbucket. 
. . .
}}}

4. At this point you can start using git to clone, pull, and push projects from/to Bitbucket:
{{{
$ mkdir ~/projects
$ cd ~/projects
$ git clone git@bitbucket.org:ikh/setupandtest.git
Cloning into 'setupandtest'...
remote: Counting objects: 3, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), 26.20 KiB, done.
$ cd setupandtest
$ ls
test.txt
... edit test.txt ...
$git commit -a -m 'your comment'
[master f80b5b4] removed metadata
 1 files changed, 0 insertions(+), 26 deletions(-)
$ git push 
Counting objects: 5, done.
Delta compression using up to 2 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 283 bytes, done.
Total 3 (delta 1), reused 0 (delta 0)
remote: bb/acl: ikh is allowed. accepted payload.
To git@bitbucket.org:ikh/setupandtest.git
   fcba8d8..f80b5b4  master -> master
$ git pull
Already up-to-date.
}}}
= Setup command prompt (optional)
You may set up your command prompt to show which branch you are on. Add the following line to your {{{~/.profile}}}:
{{{
PS1="$YELLOW\h:\w$RED\$(parse_git_branch)$NO_COLOUR\$ "
}}}

This will display the following prompt:
{{{
chesapeake:~/projects/setupandtest (master)$ 
}}}
= Congratulations

Congratulations! Now you are ready to start using Git and Bitbucket for real.

* To learn more about Git:  http://git-scm.com/
* To learn more about Bitbucket: http://confluence.atlassian.com/display/BITBUCKET/bitbucket+101
* To obtain help, open an issue at https://bitbucket.org/ikh/setupandtest/issues/new and feel free to contact <<user ikh>> at ikh@iri.columbia.edu


