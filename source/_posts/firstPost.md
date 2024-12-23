---
date: '\<2024-09-10 Tue\>'
tags: 'hexo, blogging, org-mode, RaspberryPi'
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
-   Git

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
[here](https://hexo.io/docs/github-pages). I recently came across
another framework called Hugo and it has a built in org renderer so in
the future it might be worth to make the jump.

Pandoc
------

Pandoc is an extremely powerful tool that converts files from one markup
format to another. Initially I was looking to leverage a plugin I found
for Hexo <https://github.com/coldnew/hexo-renderer-org> but it had
issues and also required for emacs to be installed on my system which I
didn\'t want. I settled on using python to run a pandoc command to
convert from orgmode to markdown (which is what Hexo works with by
default).

``` python
#!/usr/bin/env python3

import sys

from os import listdir
from os.path import isfile, join
from subprocess import run

def main():
    copy_from = sys.argv[1]
    copy_to   = sys.argv[2]


    for _file in [f for f in listdir(copy_from) if isfile(join(copy_from, f))]:
        file_path = join(copy_from, _file)

        filename = _file.split(".")[0]

        run(["pandoc",
             "-s",
             "-f", "org",
             "-t", "markdown",
             "-o", f"{join(copy_to, filename)}.md",
             f"{file_path}"])

        run(["/home/salhashemi2/self_scripts/change_markdown_code_format",
             f"{join(copy_to, filename)}.md"])

if __name__ == "__main__":
    main()
```

The bottom `run` command was necessary because pandoc was converting to
a version of markdown called extended markdown, which wrapped code
blocks in a ```` ```{ .language }``` ```` block instead of the standard
```` ```language``` ```` block. This caused Hexo to render the
codeblocks as a plaintext file instead of the language they were typed
in so no syntax highlighting :(.

Raspberry Pi
------------

I host all the markup files that I edit on my Raspberry Pi. Once I make
a change, a set of scripts are run that uses Pandoc to convert org to
markdown, create a commit with the date, and push changes to Github
(where the Github Pages action I defined takes over).
