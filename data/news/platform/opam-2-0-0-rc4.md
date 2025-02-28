---
title: "opam 2.0.0 RC4-final is out!"
authors: [ "Raja Boujbel", "Louis Gesbert"]
date: "2018-07-26"
description: "Release announcement for OPAM 2.0.0~rc4"
tags: [platform]
---

We are happy to announce the [opam 2.0.0 final release candidate](https://github.com/ocaml/opam/releases/tag/2.0.0-rc4)! 🍾 

This release features a few bugfixes over [Release Candidate 3](../opam-2-0-0-rc3). **It will be promoted to 2.0.0 proper within a few weeks, when the [official repository](https://github.com/ocaml/opam-repository) format switches from 1.2.0 to 2.0.0.** After that date, updates to the 1.2.0 repository may become limited, as new features are getting used in packages.

It is safe to update as soon as you see fit, since opam 2.0.0 supports the older formats. See the [Upgrade Guide](http://opam.ocaml.org/2.0-preview/doc/Upgrade_guide.html) for details about the new features and changes. If you are a package maintainer, you should keep publishing as before for now: the [roadmap](https://opam.ocaml.org/blog/opam-2-0-0-repo-upgrade-roadmap) for the repository upgrade will be detailed shortly.

The opam.ocaml.org pages have also been refreshed a bit, and the new version showing the 2.0.0 branch of the repository is already online at [http://opam.ocaml.org/2.0-preview/](http://opam.ocaml.org/2.0-preview/) (report any issues [here](https://github.com/ocaml/opam2web/issues)).


---

Installation instructions:

1. From binaries: run

    ```
    sh <(curl -sL https://raw.githubusercontent.com/ocaml/opam/master/shell/install.sh)
    ```

    or download manually from [the Github "Releases" page](https://github.com/ocaml/opam/releases/tag/2.0.0-rc4) to your PATH. In this case, don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed.

2. From source, using opam:

    ```
    opam update; opam install opam-devel
    ```

   (then copy the opam binary to your PATH as explained, and don't forget to run `opam init --reinit -ni` to enable sandboxing if you had version 2.0.0~rc manually installed)

3. From source, manually: see the instructions in the [README](https://github.com/ocaml/opam/tree/2.0.0-rc4#compiling-this-repo).

We hope you enjoy this new version, and remain open to [bug reports](https://github.com/ocaml/opam/issues) and [suggestions](https://github.com/ocaml/opam/issues).

> NOTE: this article is cross-posted on [opam.ocaml.org](https://opam.ocaml.org/blog/) and [ocamlpro.com](http://www.ocamlpro.com/category/blog/). Please head to the latter for the comments!
