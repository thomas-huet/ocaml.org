---
title: "opam 2.0.4 release"
authors: [ "Raja Boujbel", "Louis Gesbert"]
date: "2019-04-10"
description: "Release announcement for OPAM 2.0.4"
tags: [platform]
---

We are pleased to announce the release of [opam 2.0.4](https://github.com/ocaml/opam/releases/tag/2.0.4).

This new version contains some [backported fixes](https://github.com/ocaml/opam/pull/3805):
* Sandboxing on macOS: considering the possibility that TMPDIR is unset [[#3597](https://github.com/ocaml/opam/pull/3597) [@herbelin](https://github.com/herbelin) - fix [#3576](https://github.com/ocaml/opam/issues/3576)]
* display: Fix `opam config var` display, aligned on `opam config list` [[#3723](https://github.com/ocaml/opam/pull/3723) [@rjbou](https://github.com/rjbou) - rel. [#3717](https://github.com/ocaml/opam/issues/3717)]
* pin:
  * update source of (version) pinned directory [[#3726](https://github.com/ocaml/opam/pull/3726) [@rjbou](https://github.com/rjbou) - [#3651](https://github.com/ocaml/opam/issues/3651)]
  * fix `--ignore-pin-depends` with autopin [[#3736](https://github.com/ocaml/opam/pull/3736) [@AltGr](https://github.com/AltGr)]
  * fix pinnings not installing/upgrading already pinned packages (introduced in 2.0.2) [[#3800](https://github.com/ocaml/opam/pull/3800) [@AltGr](https://github.com/AltGr)]
* opam clean: Ignore errors trying to remove directories [[#3732](https://github.com/ocaml/opam/pull/3732) [@kit-ty-kate](https://github.com/kit)]
* remove wrong "mismatched extra-files" warning [[#3744](https://github.com/ocaml/opam/pull/3744) [@rjbou](https://github.com/rjbou)]
* urls: fix hg opam 1.2 url parsing [[#3754](https://github.com/ocaml/opam/pull/3754) [@rjbou](https://github.com/rjbou)]
* lint: update message of warning 47, to avoid confusion because of missing `synopsis` field internally inferred from `descr` [[#3753](https://github.com/ocaml/opam/pull/3753) [@rjbou](https://github.com/rjbou) - fix [#3738](https://github.com/ocaml/opam/issues/3738)]
* system:
  * lock & signals: don't interrupt at non terminal signals [[#3541](https://github.com/ocaml/opam/pull/3541) [@rjbou](https://github.com/rjbou)]
  * shell: fix fish manpath setting [[#3728](https://github.com/ocaml/opam/pull/3728) [@gregory-nisbet](https://github.com/gregory)]
  * git: use `diff.noprefix=false` config argument to overwrite user defined configuration [[#3788](https://github.com/ocaml/opam/pull/3788) [@rjbou](https://github.com/rjbou), [#3628](https://github.com/ocaml/opam/pull/3628) [@Blaisorblade](https://github.com/Blaisorblade) - fix [#3627](https://github.com/ocaml/opam/issues/3627)]
* dirtrack: fix precise tracking mode [[#3796](https://github.com/ocaml/opam/pull/3796) [@rjbou](https://github.com/rjbou)]
* fix some mispellings [[#3731](https://github.com/ocaml/opam/pull/3731) [@MisterDA](https://github.com/MisterDA)]
* CI enhancement & fixes [[#3706](https://github.com/ocaml/opam/pull/3706) [@dra27](https://github.com/dra27), [#3748](https://github.com/ocaml/opam/pull/3748) [@rjbou](https://github.com/rjbou), [#3801](https://github.com/ocaml/opam/pull/3801) [@rjbou](https://github.com/rjbou)]

> Note: To homogenise macOS name on system detection, we decided to keep `macos`, and convert `darwin` to `macos` in opam. For the moment, to not break jobs & CIs, we keep uploading `darwin` & `macos` binaries, but from the 2.1.0 release, only `macos` ones will be kept.

---

Installation instructions (unchanged):

1. From binaries: run

    ```
    sh <(curl -sL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh)
    ```

    or download manually from [the Github "Releases" page](https://github.com/ocaml/opam/releases/tag/2.0.4) to your PATH. In this case, don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed or to update you sandbox script.

2. From source, using opam:

    ```
    opam update; opam install opam-devel
    ```

   (then copy the opam binary to your PATH as explained, and don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed or to update you sandbox script)

3. From source, manually: see the instructions in the [README](https://github.com/ocaml/opam/tree/2.0.4#compiling-this-repo).

We hope you enjoy this new minor version, and remain open to [bug reports](https://github.com/ocaml/opam/issues) and [suggestions](https://github.com/ocaml/opam/issues).

> NOTE: this article is cross-posted on [opam.ocaml.org](https://opam.ocaml.org/blog/) and [ocamlpro.com](http://www.ocamlpro.com/category/blog/). Please head to the latter for the comments!
