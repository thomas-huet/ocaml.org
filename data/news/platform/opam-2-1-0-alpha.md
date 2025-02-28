---
title: "opam 2.1.0 alpha is here!"
authors: [ "Raja Boujbel", "Louis Gesbert"]
date: "2020-04-21"
description: "Release announcement for opam 2.1.0~alpha"
tags: [platform]
---

We are happy to announce a alpha for opam 2.1.0, one year and a half in the 
making after the release of 2.0.0.

Many new features made it in (see the [complete
changelog](https://github.com/ocaml/opam/blob/2.1.0-alpha/CHANGES) or [release
note](https://github.com/ocaml/opam/releases/tag/2.1.0-alpha) for the details),
but here are a few highlights of this release.


# Release highlights

The two following features have been around for a while as plugins and are now 
completely integrated in the core of opam. No extra installs needed anymore, and
a more smooth experience.


### Seamless integration of System dependencies handling (a.k.a. "depexts")

A number of opam packages depend on tools or libraries installed on the system,
which are out of the scope of opam itself. Previous versions of opam added a
[specification format](http://opam.ocaml.org/doc/Manual.html#opamfield-depexts),
and opam 2.0 already handled checking the OS and extracting the required system
package names.

However, the workflow generally involved letting opam fail once, then installing
the dependencies and retrying, or explicitely using the
[opam-depext plugin](https://github.com/ocaml/opam-depext), which was invaluable
for CI but still incurred extra steps.

With opam 2.1.0, _depexts_ are seamlessly integrated, and you basically won't
have to worry about them ahead of time:

- Before applying its course of actions, opam 2.1.0 checks that external
  dependencies are present, and will prompt you to install them. You are free to
  let it do it using `sudo`, or just run the provided commands yourself.
- It is resilient to _depexts_ getting removed or out of sync.
- Opam 2.1.0 detects packages that depend on stuff that is not available on your
  OS version, and automatically avoids them.

This is all fully configurable, and can be bypassed without tricky commands when
you need it (_e.g._ when you compiled a dependency yourself).


### Dependency locking

To share a project for development, it is often necessary to be able to
reproduce the exact same environment and dependencies setting — as opposed to
allowing a range of versions as opam encourages you to do for releases.

For some reason, most other package managers call this feature "lock files".
Opam can handle those in the form of `[foo.]opam.locked` files, and the
`--locked` option.

With 2.1.0, you no longer need a plugin to generate these files: just running
`opam lock` will create them for existing `opam` files, enforcing the exact
version of all dependencies (including locally pinned packages).

If you check-in these files, new users would just have run
`opam switch create . --locked` on a fresh clone to get a local switch ready to
build the project.


### Pinning sub-directories

This one is completely new: fans of the _Monorepo_ rejoice, opam is now able to
handle projects in subtrees of a repository.

- Using `opam pin PROJECT_ROOT --subpath SUB_PROJECT`, opam will look for
  `PROJECT_ROOT/SUB_PROJECT/foo.opam`. This will behave as a pinning to
  `PROJECT_ROOT/SUB_PROJECT`, except that the version-control handling is done
  in `PROJECT_ROOT`.
- Use `opam pin PROJECT_ROOT --recursive` to automatically lookup all sub-trees
  with opam files and pin them.


### Opam switches are now defined by invariants

Previous versions of opam defined switches based on _base packages_, which
typically included a compiler, and were immutable. Opam 2.1.0 instead defines
them in terms of an _invariant_, which is a generic dependency formula.

This removes a lot of the rigidity `opam switch` commands had, with little
changes on the existing commands. For example, `opam upgrade ocaml` commands are
now possible; you could also define the invariant as `ocaml-system` and have
its version change along with the version of the OCaml compiler installed
system-wide.


### Configuring opam from the command-line

The new `opam option` command allows to configure several options,
without requiring manual edition of the configuration files.

For example:
- `opam option jobs=6 --global` will set the number of parallel build
  jobs opam is allowed to run (along with the associated `jobs` variable)
- `opam option depext-run-commands=false` disables the use of `sudo` for
  handling system dependencies; it will be replaced by a prompt to run the
  installation commands.

The command `opam var` is extended with the same format, acting on switch and
global variables.

# Try it!

In case you plan a possible rollback, you may want to first backup your
`~/.opam` directory.

The upgrade instructions are unchanged:

1. Either from binaries: run

    ```
    bash -c "sh <(curl -fsSL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh) --version 2.1.0~alpha"
    ```

    or download manually from [the Github "Releases" page](https://github.com/ocaml/opam/releases/tag/2.1.0-alpha) to your PATH.

2. Or from source, manually: see the instructions in the [README](https://github.com/ocaml/opam/tree/2.1.0-alpha#compiling-this-repo).


You should then run:
```
opam init --reinit -ni
```


This is still a alpha, so a few glitches or regressions are to be expected.
Please report them to [the bug-tracker](https://github.com/ocaml/opam/issues).
Thanks for trying it out, and hoping you enjoy!


> NOTE: this article is cross-posted on
[opam.ocaml.org](https://opam.ocaml.org/blog/) and
[ocamlpro.com](http://www.ocamlpro.com/category/blog/). Please head to the
latter for the comments!
