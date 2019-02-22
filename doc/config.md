GG Configuration Files
======================

Config settings for how `gg` operates can come from multiple locations, with the highest priority ones on top.

* Environment variables override everything.
* Project config (`.gg/config`).
* User config (`~/.ggconfig`).
* Auto detection and reasonable defaults.

The following lists all of the config settings that are used by `gg`.


`filter.tags`
-------------

* Environment: `GG_FILTER_TAGS`
* Config file: `filter.tags`
* Default: No filtering of projects.

Commands that operate across projects will see if this setting is set to a non-empty value. If it is, the pool of projects that get the operation are limited. If a project lists any tag that is in this list, that project is included in the operation.

The list can be comma or space separated. Each tag must match exactly; it is case sensitive. The filter will match a project if any of the project's tags match against any filter tag.

Example Manifest (omitting the remote and path):

    [project1]
    tags=yellow,red,blue,green

    [project2]
    tags=red,pink

    [project3]
    tags=yellow black orange

Examples:

    # Synchronizes just project1 and project2
    GG_FILTER_TAGS=yellow gg sync

    # Synchronizes all three
    GG_FILTER_TAGS="green pink orange" gg sync

    # Synchronizes just project 3
    GG_FILTER_TAGS=black,purple,white gg sync


`parallel.jobs`
---------------

* Environment: `GG_PARALLEL_JOBS`
* Config file: `parallel.jobs`
* Default: 1 per processor.
* Restrictions: Minimum of 1.

This controls how many `git` operations can execute simultaneously for commands like `sync` or `status`. If you have a lot of repositories, you might want to increase this number.

Examples:

    # Forcibly sync just one project at a time
    GG_PARALLEL_JOBS=1 gg sync

    # Sync several projects at once
    GG_PARALLEL_JOBS=10 gg sync
