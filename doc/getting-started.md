Getting Started with GG
=======================

This guide will help you build your first Git Group and explain the fundamentals of how `gg` works.

You will need:

* Git
* An internet connection
* `gg` installed (see the [installation instructions for `gg`](https://github.com/fidian/gg))
* A place to host your manifest file.


Create a Git Repository
-----------------------

This will hold your manifest file and track its changes. It's temporary and can safely be deleted later.

    $ mkdir gg-demo-manifest
    $ cd gg-demo-manifest
    $ git init
    Initialized empty Git repository in /home/gg/gg-demo-manifest/.git/
    $


Create the Initial Manifest
---------------------------

Create a file called `manifest.ini` in the root of the repository. It will describe your projects. This example will pull down the `gg` repository and `gg-core`. The first one is the `gg` tool and the second is where all of the extra library functions get added.

    [gg]
    remote=http://github.com/fidian/gg.git
    path=gg

    [gg-core]
    remote=http://github.com/fidian/gg-core.git
    path=gg-core

The details of the manifest file are [explained elsewhere](manifest.md).

Save the file and now we add it to the repository.

    $ git add manifest.ini
    $ git commit -m 'Initial commit' manifest.ini
    [master (root-commit) f95e557] Initial commit
     1 file changed, 7 insertions(+)
     create mode 100644 manifest.ini
    $


Publish the Git Repository
--------------------------

Excellent work. Now we publish this repository somewhere. This step changes a lot, depending on where you host your files. Only a very generic set of instructions are shown here.

    $ git remote add origin git@github.com:fidian/gg-demo-manifest.git
    $ git push -u origin master
    Counting objects: 3, done.
    Delta compression using up to 8 threads.
    Compressing objects: 100% (2/2), done.
    Writing objects: 100% (3/3), 288 bytes | 288.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To github.com:fidian/gg-demo-manifest.git
     * [new branch]      master -> master
    Branch 'master' set up to track remote branch 'master' from 'origin'.
    $


Clean Up (Optional)
-------------------

It's now safe to delete this repository.

    $ cd ..
    $ rm -rf gg-demo-manifest
    $


Cloning Your Git Group
----------------------

Finally, it's time to see how this `gg` tool works. We initialize the folder using the remote's URL and a local directory name.

    $ gg init http://my-git-server/gg/gg-demo-manifest gg-demo
    *** Creating meta dir: .gg
    *** Cloning gg-core: git@github.com:fidian/gg-demo-manifest.git
    Cloning into '.gg/gg-core'...
    remote: Enumerating objects: 148, done.
    remote: Total 148 (delta 0), reused 0 (delta 0), pack-reused 148
    Receiving objects: 100% (148/148), 28.39 KiB | 476.00 KiB/s, done.
    Resolving deltas: 100% (72/72), done.
    *** Cloning manifest: git@github.com:fidian/gg-demo-manifest.git
    Cloning into '.gg/manifest'...
    remote: Enumerating objects: 3, done.
    remote: Counting objects: 100% (3/3), done.
    remote: Compressing objects: 100% (2/2), done.
    remote: Total 3 (delta 0), reused 3 (delta 0), pack-reused 0
    Receiving objects: 100% (3/3), done.
    *** Initialization complete.
    Your next action will probably be: gg sync
    $

You'll see a lot going on there. What ends up happening is the `gg-demo` group folder is created. Within that, `.gg/` is made to hold the meta information, such as the manifest file and `gg` libraries. The libraries are pulled down from the repository and the demo manifest repository is cloned as well. It even gives you a hint of what to do next.

This is not yet done. We need to still pull down our repositories.

    $ cd gg-demo
    $ gg sync
    *** Synchronizing .gg/gg-core
    Already up to date.
    *** Synchronizing .gg/manifest
    Already up to date.
    *** Cloning gg into gg
    Cloning into 'gg'...
    warning: redirecting to https://github.com/fidian/gg.git/
    warning: redirecting to https://github.com/fidian/gg.git/
    Already up to date.
    *** Cloning gg-core into gg-core
    Cloning into 'gg-core'...
    warning: redirecting to https://github.com/fidian/gg-core.git/
    warning: redirecting to https://github.com/fidian/gg-core.git/
    Already up to date.
    $

The list of repositories is read from the manifest file and `gg` notices that this folder is missing two of them, so it automatically clones them into `gg-demo` for you. If you peek about in this file, you'll see that you have two fully functional repositories.

Success! You've done it!


What's Next?
------------

I would suggest looking around in the repositories. Now that you are within a Git Group, you can run `gg` anywhere under this folder and commands will all operate at the right level. There's a lot more commands that get added to the simple `gg` command that all help you to manage your repositories.
