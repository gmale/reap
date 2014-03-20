Reap
====

Reap is like [Google's Repo tool](https://code.google.com/p/git-repo/), just a bit simpler. It is designed to make working with multiple git repositories as easy as it should be. At a high level, the main thing Reap does is clone repositories to a location, remember how to find them later and then allow users to work with those repos in bulk.

Reap is:
 - a complement to git
 
Reap is not:
 - a replacement for git
 
##Origin
GIT is an amazing tool that has had a major impact on the entire software industry. It's an elegant solution, until you need to work with a half-dozen or more repos simultaneously. Of course, writing software nearly always requires modular "building blocks." Yet, when there's a "models" or "utilities" project that is a dependency of many larger projects, GIT makes mixing and matching those building blocks a real challenge.

That's where tools like [git submodules](http://git-scm.com/docs/git-submodule), [git subtree](https://github.com/git/git/blob/master/contrib/subtree/git-subtree.txt), and [Google Repo](https://code.google.com/p/git-repo/) come into play. After trying them all, they share one common fault: complexity. Repo is my personal favorite but it doesn't lend itself well to my most common usecase: recombining repositories (dependencies) into parent projects.


##Gameplan

####Reap what you sow
Given a "statement of work" defined in a json-formatted `.sow` file, containing mostly repository meta-data, this tool provides various commands that facilite working with those repositories.

####Objectives
Reap has 4 main objectives:

1. simplicity
1. minimal learning curve
1. make working with multiple repos as elegant as it should be
1. simplicity

####.sow Files
_Statement of Work_ files will be written in JSON because it's much simpler than XML. They will consist of two main sections:
 - Configuration
     * will contain a few basic options that apply to all repositories like `workspace_dir` and `git_url`
 - Repositories
     * will contain basic properties that allow for a flexible range of actions on repositories
     * The primary actions for repositories are
         - clone a repository to a directory
         - optionally create a symlink to that directory
         - remember where/how to find each repository after it's cloned, for bulk actions later
     * `repo_name`
     * `clone_type` ssh, http, etc.
     * `package_type` aar, apk, jar, war, etc.
     * `clone_to_dir` directory to clone the repo to. Defaults to $workspace_dir/$repo_name
     * `symlink_source` optional target for a symlink. Defaults to $clone_to_dir/$repo_name
     * `symlink_destination` optional symlink to use. Can make use of directories in configuration object

####Commands
Proposed commands include:

`reap init` reap everything in the .sow file. This command will clone all the repositories and put them where they go.    
`reap status` summarize the git status of all projects. This is similar to running `reap forall git status` but provides a more streamlined summary.    
`reap status -i` interactive version of _reap status_ that allows users to select a subset of projects on which to report     
`reap forall <cmd>` apply one or more semi-colon separated commands to all repositories    
`reap forall -i` interactive version of _reap forall_ that allows users to select a subset of projects on which to run commands    

##Status

Reap is currently in the pre-alpha phase. I just thought this up an hour ago. However, I hope to have a usable release ready by the end of the month of March, 2014.
