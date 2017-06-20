GG Configuration Files
======================

Config settings for how `gg` operates can come from multiple locations, with the highest priority ones on top.

* Environment variables override everything.
* Project config (`.gg/config`).
* User config (`~/.ggconfig`).
* Auto detection and reasonable defaults.

The following lists all of the config settings that are used by `gg`.


`parallel.jobs`
---------------

* Environment: `PARALLEL_JOBS`
* Config file: `parallel.jobs`
* Default: 1 per processor.
* Restrictions: Minimum of 1.

This controls how many `git` operations can execute simultaneously for commands like `sync` or `status`. If you have a lot of repositories, you might want to increase this number.
