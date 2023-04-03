---
title: "Improving My Directory Workflow"
date: 2023-01-27T19:22:37+04:00
draft: false
tags:
  - tech
  - linux
---

This is my most used custom shell script.

````
#!/bin/sh

directory=$(find ~/myworkspace ~/Desktop -mindepth 0 -maxdepth 1 -type d | fzf)

if [ -z "$1" ]; then
    cd "$directory"
    exec bash
else
    exec ranger "$directory"
fi
````

# Speed 🏃🏻💨

`dic` was a little script I made to quickly find directories that I use a lot.

Gone are the days of `cd ~; cd important-directory/; ls; cd subdirectory; ls; vim important-document.md`

Now I just run `dic` and use `fzf` to search for the directory I need.
