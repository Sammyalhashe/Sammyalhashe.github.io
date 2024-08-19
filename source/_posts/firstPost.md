---
title: How I made this blog.
---

I\'ve been wanting to make a blogging system that works relatively
seemless and integrates with the tools I already use. This is how I
accomplished that.

Tools I use
===========

-   Neovim
-   Github Pages
-   Hexo
-   Raspberry Pi
-   Python/Bash
-   Pandoc

The basic premise is that I configure a github pages repository that
deploys everytime something is pushed to its `master` branch. For now, I
am being a little silly and running a bash script that automatically
creates a new commit and pushes it up when it notices I made a change
after a configurable amount of time.

Basic Infrastructure
====================

Github Pages
------------

Github pages was probably the simplest way to get a simple website up
and running. All I did was follow it\'s basic guide
[here](https://pages.github.com/).

Hexo
----

Hexo is a static site generator similar to Jekyll. I decided to use this
simply because I stumbled upon a blog post that sung its praises and it
also had easy to follow documentation for setting it up for Github
Pages. I followed its documentation
[here](https://hexo.io/docs/github-pages).
