`git-imp`
=========

This is a collection of Git command plugins that I've created and keep them here to maintain them and in the hope that others may find them useful. Most of the stuff I develope is named _Something_**Imp**. So I'm calling this collection `git-imp`. But there is no actual command called `git-imp` in the collection.

These are BASH and POSIX scripts I developed on my Mac and are not expected to work in all environments. Though they _should_ work in most UNIX/Linux environments. And in fact require at least BASH 3 due to use of BASH_REMATCH and such in many cases. See Command Chart bellow for details. I currently have no immediate plans of porting these scripts to be entirely POSIX compliant. Though that is a possibility in the future. And at least one of the scripts has a dependency on [BASHimp][] for option parsing. It is not included in this repo. But is another open source project of mine.


The Commands
------------

### `git-cpdiff`

Copies the current (uncommited) file specified by the user. Does a checkout of the same file and then runs opendiff (Mac: opendiff opens FileMerge) or diff on the two files. It outputs an error if there is no diffing tool found.

Example: `git cpdiff FILENAME`


### `git-current`

Outputs the current branch active in git.

Example:

```
$ git current
master
```


### `git-deep-clone`

This command allows you to clone a repo, initialize any submodules, and setup remote branch tracking for all remote branches. I may add the ability to dissable submodule initialization and the remote branch tracking or make them optional to begin with at a later time. Though really you probably don't need this command if you don't need all three. I'm always open to discussion though.  :-)

Example: `git deep-clone URI/REPOSITORY.git`


### `git-hist`

Outputs a nicely formated history limited to the specified number of commits per specification by user.

Example: `git hist 5` with the repo to view simple history of the last 5 commits with graphical (ASCII) display of multi-user actions.

```
$ git hist 5
* 4b8ad50 2015-07-02 | OPTIONIMP_ARGUMENTS and other goodies (HEAD -> develop, origin/develop) [Mark Gardner]
* dc1c887 2015-06-15 | added copy command so BASHimp could copy itself or another script into the user's bin. (release/v0.7.0) [Mark Gardner]
* 85f8fec 2015-06-14 | updated README.md [Mark Gardner]
* 38c8c9c 2015-06-14 | initial version with a working OPTIONimp mode (tag: v0.6.0) [Mark Gardner]
* 714504b 2015-06-13 | beginnings of OPTIONimp AKA BASHimp Beast Mode (tag: v0.5.0) [Mark Gardner]
```


### `git-rbt`

Git Remote Branch Track

Quick command to setup remote branch tracking in a repo that few or no branches tracking against a remote repo.

Example: `git rbt`


### `git-squash`

Quick command to start an interactive rebase of 1 or more commits you specify. So you can `edit`, `exec`, `fixup`, `pick`, `reword`, or `squash` those commits. I typically just use squash to clean up history before commiting to or merging with the main remote repo. This is potentually **VERY** destructive. Be sure you understand the topic and have backups of your repo before attempting to use this command or the rebase command in general.

Example: `git squash 3` from within the repo to do an interactive rebase of the last 3 commits. _Use at your own risk!_ Do not blame me if your invaded by aliens, audited by the IRS, or you switch genders in your sleep!

See [Git - Rewriting History](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History)


### `git-subswitch`

This command allows you to quickly do a few things to a collection of submodules.

Examples:

1. `git subswitch BRANCHNAME` will enter all subdirectories of the current directory, test if it's a submodule, and then `checkout` that submodule to the specified _BRANCHNAME_.
2. `git subswitch --basepath path/you/choose BRANCHNAME` does the same as above but will `cd` to the specified _basepath_ first. Then loop through the subdirectories as above.
3. `git subswitch --pull BRANCHNAME` does the same as #1 but will also `git pull` on the submodule after checkout to the specified _BRANCHNAME_.
4. `git subswitch --init` goes into each subdirectory of the current directory, test if it's _not_ an initialized submodule yet, and does `git submodule init` then `git submodule update`. This is handy if you forgot to specify `--recursive` with a `git clone` call on a repo with submodules.

`--basepath`
: This can be specified with any other option.

`--init`
: This option will override the default behavior; for obvious reasons.


### Command Chart

| Command          | Version | Usage     | Spec    | Dependencies | Description                                                                               |
| -------          | ------- | -----     | ----    | ------------ | -----------                                                                               |
| `git-cpdiff`     | 1.0.0   | Safe      | BASH 3+ |              | Copies an uncommited file and diffs it against the prior commited file.                   |
| `git-current`    | 1.0.0   | Safe      | BASH 3+ |              | Displays the current branch.                                                              |
| `git-deep-clone` | 1.0.0   | Safe      | BASH 3+ |              | Clones a repo recursively (gets submodules) and tracks remote branches.                   |
| `git-hist`       | 1.0.0   | Safe      | POSIX   |              | Displays a simple, graphical history of the repo limted by a specified number of commits. |
| `git-rbt`        | 1.0.0   | Safe      | BASH 3+ |              | Sets up remote branch tracking in a repo.                                                 |
| `git-squash`     | 1.0.0   | Dangerous | POSIX   |              | Initiates an interactive rebase for the specified number of commits.                      |
| `git-subswitch`  | 1.2.0   | Safe      | BASH 3+ | [BASHimp][]  | Runs checkout or submodule init and update for all subdirectories that are submodules.    |


Installation
------------

Copy the scripts (including `bashimp` if you don't already have it) into your `bin` directory. All git commands should work as expected now.


[BASHimp]: https://github.com/runeimp/bashimp

