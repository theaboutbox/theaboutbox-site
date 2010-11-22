---
kind: article
title: Migrating Part of a Subversion Repository
created_at: 20101122T145855
---
Recently I needed to take part of a monolithic Subversion repository, and create a new, smaller repository, while keeping all of the
history intact. For all intents and purposes, I needed to move:

    https://svn.example.com/lots_of_projects/project_a

to its own repository rooted at

    https://svn.example.com/project_a

Oh, and to make matters more fun, I don't have admin access to any of these repos.

Import/Export
-------------

The easy way to copy things from one repository to another is do an `svn export` followed by an `svn import` to the new
repository. This works, but you lose all of the history, which is a bummer.

Git-Svn
-------

Another possibility to keep all of the revisions intact is to use `git-svn` to clone the subversion repository with history
and then use it as a basis to populate a new subversion repository. I haven't tried it, but something like this would probably work:

    git svn clone [args] [subversion repo] temp-repo

Follow the instructions [here on Google Code](http://code.google.com/p/support/wiki/ImportingFromGit) but when you fetch, fetch from
the `temp-repo` you just created.

One nice thing about this approach is that it requires nothing on the subversion server side to work. The downside is that you will
probably lose dates and user information in the history.

Sync + Filter
-------------

Probably the most robust way to do this is without physical access to the svn server is to create a local repository, mirror the source
repository, filter out everything that is NOT what you want to copy, and then sync that with the destination repo. There are a few steps
involved and it's better to actually get access to both repositories (then you can just use Subversion's admin tools) to get everything, 
but in the absence of access to the servers, then [svnsync](http://svnbook.red-bean.com/en/1.4/svn.ref.svnsync.html) is the next best 
thing to get a repository's contents, with history.

    svnadmin create temp-repo
    cd temp-repo/hooks
    echo "exit 0" > pre-revprop-hook
    chmod a+x pre-revprop-hook
    cd ../..
    svnsync initialize file://[path-to-temp-repo] https://svn.example.com/lots_of_projects
    svnsync synchronize file://[path-to-temp-repo]
    (Time passes)
    svnadmin dump ./temp-repo > everything.dump
    cat everything-dump | svndumpfilter include project_a --drop-empty-revs --renumber-revs > project-a-dump
    svnadmin create project_a; svnadmin load project_a < project_a_dump
    svnsync initialize https://svn.example.com/project_a file://[path-to-project_a-repo]
    svnsync synchronize https://svn.example.com/project_a

In essence, what we are doing is creating a local mirror copy of the big repo that we can play with. Once we have a mirror that we can
manipulate, we can dump its history and filter out only the project that we are interested in. Once we have that, we create a new local
repo with only those commits in it, and synchronize it with its new home.

The only problem with this approach is that there needs to be a pre-revprop-hook installed on the target repository, which will
require some cooperation from the administrator of that repository.

If anyone else knows of a way to copy part of a subversion repository with all of its history, I would love to hear it.