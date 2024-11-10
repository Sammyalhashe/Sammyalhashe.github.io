---
author:
- Sammy Al Hashemi
title: Working with devenv on a basic Python project
---

My friends and I have been working on a basic personal python project.
During initial project setup, as I have been experimenting with nix, I
decided to give `devenv.sh` a try.

[devenv website](https://devenv.sh/)

What it is
==========

-   devenv makes it possible to create declarative dev environments that
    are reproducible between machines.
-   It works using `nix` as the declarative language.
-   You can specify packages to install, shell dependencies that you
    want in your dev environment, run scripts on shell startup, and run
    services crucial to your development in the background.
