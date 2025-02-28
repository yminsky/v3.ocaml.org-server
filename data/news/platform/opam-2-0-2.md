---
title: "opam 2.0.2 release"
authors: [ "Raja Boujbel", "Louis Gesbert"]
date: "2018-12-12"
description: "Release announcement for OPAM 2.0.2"
tags: [platform]
---

We are pleased to announce the release of [opam 2.0.2](https://github.com/ocaml/opam/releases/tag/2.0.2).

As **sandbox scripts** have been updated, don't forget to run `opam init --reinit -ni` to update yours.

This new version contains mainly [backported fixes](https://github.com/ocaml/opam/pull/3669):
* Doc:
  * update man page
  * add message for deprecated options
  * reinsert removed ones to print a deprecated message instead of fail (e.g. `--alias-of`)
  * deprecate `no-aspcud`
* Pin:
  * on pinning, rebuild updated `pin-depends` packages reliably
  * include descr & url files on pinning 1.2 opam files
* Sandbox:
  * handle symlinks in bubblewrap for system directories such as `/bin` or `/lib` ([#3661](https://github.com/ocaml/opam/pull/3661)).  Fixes sandboxing on some distributions such as CentOS 7 and Arch Linux.
  * allow use of unix domain sockets on macOS ([#3659](https://github.com/ocaml/opam/issues/3659))
  * change one-line conditional to if statement which was incompatible with set -e
  * make /var readonly instead of empty and rw
* Path: resolve default opam root path
* System: suffix .out for read_command_output stdout files
* Locked: check consistency with opam file when reading lock file to suggest regeneration message
* Show: remove pin depends messages
* Cudf: Fix closure computation in the presence of cycles to have a complete graph if a cycle is present in the graph (typically `ocaml-base-compiler` ⇄ `ocaml`) 
* List: Fix some cases of listing coinstallable packages
* Format upgrade: extract archived source files of version-pinned packages
* Core: add is_archive in OpamSystem and OpamFilename
* Init: don't fail if empty compiler given
* Lint: fix light_uninstall flag for error 52
* Build: partial port to dune
* Update cold compiler to 4.07.1

---

Installation instructions (unchanged):

1. From binaries: run

    ```
    sh <(curl -sL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh)
    ```

    or download manually from [the Github "Releases" page](https://github.com/ocaml/opam/releases/tag/2.0.2) to your PATH. In this case, don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed or to update your sandbox script.

2. From source, using opam:

    ```
    opam update; opam install opam-devel
    ```

   (then copy the opam binary to your PATH as explained, and don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed or to update you sandbox script)

3. From source, manually: see the instructions in the [README](https://github.com/ocaml/opam/tree/2.0.2#compiling-this-repo).

We hope you enjoy this new minor version, and remain open to [bug reports](https://github.com/ocaml/opam/issues) and [suggestions](https://github.com/ocaml/opam/issues).

> NOTE: this article is cross-posted on [opam.ocaml.org](https://opam.ocaml.org/blog/) and [ocamlpro.com](http://www.ocamlpro.com/category/blog/). Please head to the latter for the comments!
