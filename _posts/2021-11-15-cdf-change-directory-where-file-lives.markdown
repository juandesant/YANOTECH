---
layout:     post
author:     Juande Santander-Vela
title:     "cdf: a function to change to the directory that contains a file"
categories: command-line-interface, posix, bash, zsh, shell
---

> **TL;DR**: `cdf` is a tool that you can use in any bash-like shell (zsh included) to change to the directory that contains the file whose path is being passed as an argument.

As a macOS user, I'm very used to the fact that you can use *Show in Finder* or *Show in enclosing folder* on many occassions. But sometimes, you want to do something similar in the terminal.

That is why I developed the following bash function (which started in my `.bash_profile`, and now lives in my `.zshrc`) that does exactly that:

```lang-bash
cdf() {
	dest_dir=$(dirname "$1")
	cd "$dest_dir"
}
````

This simply gets the destination directory from the path being passed (using `dirname`, and the `$()` substitution).

Then, use use `cd` to that directory. We need to use quotes after cd to make sure that we don't split directories that cointain blanks…

And that is it! You can now start typing `cdf ` in your terminal, and then drag and drop from your file manager — say, the Finder on macOS — and a full path to a file, and you will change directory to the folder containing that file.