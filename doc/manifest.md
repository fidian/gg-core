GG Manifest
===========

A manifest repository contains a single file that tells [gg] what projects to clone and where they are stored.  It's an INI-style file.  Let's dive right in with an example:

    [project-name]
    remote=git@github.com:example/project.git
    path=project-name

    [second-project]
    remote=git@github.com:example/second-project.git
    path=second-place

    [config]
    remote=git@github.com:example/config.git
    path=data/config

If this were a useful file and someone ran `gg sync` in an initialized directory, the folder structure would look like this when done:

    /home/user/initialized-directory/.gg/gg-core    # Most of the gg commands
    /home/user/initialized-directory/.gg/manifest   # Repo with the above file
    /home/user/initialized-directory/project-name   # The first project
    /home/user/initialized-directory/second-place   # The second project
    /home/user/initialized-directory/data/config    # The config project

INI Format and Keys
-------------------

The format is an INI file so that additional properties can be associated with each project.  Section names are just identifiers and are used for display purposes only.  There is a `default` section that can provide default values if the project does not list a setting, though it is of no use right now.

Comments are supported with either or `#` or `;` as the first character on the line.


### remote

This lists the remote URL to use for the initial git clone.

Examples:

    [Sample Project]
    remote=http://github.com/example/project.git
    path=project/


### path

The path is the destination directory where the repository should be checked out.

Examples:

    [Apache Configs]
    ; Installs this repository to config/apache/
    remote=http://github.com/example/apache-config.git
    path=config/apache/



[gg]: https://github.com/fidian/gg
