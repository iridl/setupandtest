# Submodules

## Working with submodules

	 $ git clone --recursive git@bitbucket.org:ikh/superproj.git

	 $ git clone git@bitbucket.org:ikh/superproj.git
	 $ git submodule update --recursive --init

	 $ git submodule status
	  fb48478a1715099bc335a807550571cca057da5a public/ike2 (1.0-8-gfb48478)
	  9d84caadaa4a51356a48610832ae44e014fb42d7 setupandtest (igor-1.0.1)

## Adding a submodule

	 $ git clone git@bitbucket.org:ikh/superproj.git

	 $ git submodule add git@bitbucket.org:iridl/miconf.git miconf

	 $ git status 
	 # On branch master
	 # Changes to be committed:
	 #   (use "git reset HEAD <file>..." to unstage)
	 #
	 #	modified:   .gitmodules
	 #	new file:   miconf
	 #

	 $ cat .gitmodules 
         . . . 
	 [submodule "miconf"]
	 	path = miconf
	 	url = git@bitbucket.org:iridl/miconf.git

	 $ cat .git/config 
	 . . .
	 [submodule "miconf"]
	 	url = git@bitbucket.org:iridl/miconf.git


	 $ cd miconf
	 $ git checkout miconf-1.1.0
	 Note: checking out 'miconf-1.1.0'.  You are in 'detached HEAD' state. ... 

         $ cd ..
         $ git add miconf

         $ git commit -m 'added submodule miconf @ miconf-1.1.0'

	 $ git submodule 
	  8754a9f8466e54b538a0fae9eaef32b89c0281a5 miconf (miconf-1.1.0)
	 -fb48478a1715099bc335a807550571cca057da5a public/ike2
	 -9d84caadaa4a51356a48610832ae44e014fb42d7 setupandtest

	 $ git push


## Vendor code management

### Initialize repo and submit initial vendor version

	 $ mkdir szip
	 $ cd szip
	 $ git init
	 $ git commit --allow-empty -m 'empty commit'
	 $ git checkout -b vendor
	 $ tar xvfz ~/Downloads/szip-2.1.tar.gz 
	 $ mv szip-2.1/* .
	 $ rmdir szip-2.1
	 $ git add .
	 $ git commit -m 'Vendor update. Version 2.1'
	 $ git tag 'vendor-2.1'
	 $ git checkout master 
	 $ git merge vendor
	 $ git tag szip-2.1.0
	 . . . adjust / fix the code . . . 

### N-th vendor update

	 $ git checkout vendor
	 $ rm -rf *
	 $ tar xvfz ~/Downloads/szip-2.2.tar.gz 
	 $ mv szip-2.2/* .
	 $ rmdir szip-2.2
	 $ git add .
	 $ git commit -a -m 'Vendor update. Version 2.2' # -a picks up deleted 
	 $ git tag 'vendor-2.2'
	 $ git checkout master 
	 $ git merge vendor
	 $ git tag miconf-2.2.0

# Git practices

## Learn Git CLI by heart, use GUI with care

## Tagging

         $ git tag ingrid-0.9.4
         $ git push
         $ git push --tags

### Tag pattern

	 <label>-<major>.<minor>.<patch>

Example:

	ingrid-0.9.4

### `git-generate-version-info`

         $ git-generate-version-info ingrid 'ingrid-[0-9.]*' c
         #define ingrid_VERSION_RAW "ingrid-0.9.4-4-g41dd732a0a14921f25f2b44d9cec96d27815b4c8"
         #define ingrid_VERSION "0.9.4"
         #define ingrid_VERSION_MAJOR 0
         #define ingrid_VERSION_MINOR 9
         #define ingrid_VERSION_PATCH 4
         #define ingrid_VERSION_AHEAD 4
         #define ingrid_VERSION_ID "41dd732a0a14921f25f2b44d9cec96d27815b4c8"
         #define ingrid_VERSION_SCM "git"
         #define ingrid_VERSION_REF "HEAD"


# Branch out, merge often, keep in sync

![git_base][]

         $ git branch hotfix     # create a new branch 'hotfix'
         $ git checkout hotfix   # switch to branch 'hotfix'

         $ git checkout master    # make sure you are on the right branch
         $ git merge hotfix       # merge 

	 $ git branch -d hotfix   # delete branch label

When to branch out:

* You are about to make a major or disruptive change
* You are about to make some changes that might not be used
* You want to experiment on something that you are not sure it will work
* When you are told to branch out, others might have something they need to do in master

# `git pull --rebase`

![git_rebase][]

#  How to import a repo with branches to Bitbucket

	 $ cd szip
	 $ git remote add origin git@bitbucket.org:iridl/szip.git
	 $ git config --add remote.origin.push '+refs/heads/*:refs/heads/*'
	 $ git config --add remote.origin.push '+refs/tags/*:refs/tags/*'
	 $ git push
	 $ cd ..
	 $ mv szip szip.backup
	 $ git clone --recursive git@bitbucket.org:iridl/szip.git
	 # check szip
	 # remove szip.backup


[git_base]: images/git_base.png
[git_rebase]: images/git_rebase.png


