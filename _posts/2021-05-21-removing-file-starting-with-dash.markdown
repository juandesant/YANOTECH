---
layout: post
author: Juande Santander-Vela
title:  "How to read, remove a file with dashes from the command line in macOS, Linux/Unix"
categories: bash command-line-interface macOS Linux Unix
---

I inadvertedly created a file starting with two dashes (the filename was `--verbose`) because I was trying to do something with `curl` that was misinterpreted.

When I tried to look at the content with `cat --verbose`, instead of the content this is what I got:

    $ cat --verbose 
    cat: illegal option -- -
    usage: cat [-benstuv] [file ...]

If I tried to use `less` instead, I got a similar message:

    $ less --verbose
    There is no verbose option ("less --help" for help)
    Missing filename ("less --help" for help)

What to do, then? Running `man rm`, I actually found the `--` option, which stops interpreting dashes as command-line arguments: so now I could use:

    $ rm -v --verbose
    --verbose

But you can also use a full path, or a relative path! For instance, this works!

    $ rm -v ./--verbose
    ./--verbose

Hope that helps!

ps. I later found that this [StackOverflow post][1] has both solutions… oh, well!

[1]: https://stackoverflow.com/questions/5677558/how-do-i-deal-with-a-filename-that-starts-with-the-hyphen-character "StackOverflow: How do I deal with a filename that starts with the hyphen (-) character?"

pps. How do I actually create easily, rather than by accident, an empty file starting with dashes? You can also use the `--` option in `touch` to do that! And you can also use `--` in `ls` for listing it!

    $ touch "--file"   
    touch: illegal option -- -
    usage:
    touch [-A [-][[hh]mm]SS] [-acfhm] [-r file] [-t [[CC]YY]MMDDhhmm[.SS]] file ...
    $ touch -- '--file'
    $ ls -l -- --file
    -rw-r--r--  1 myuser  131030740  0  2 Nov 07:37 --file
