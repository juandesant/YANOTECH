---
layout:     post
author:     Juande Santander-Vela
title:     "Recover the remote URL from a Git repository"
categories: git URL development
---

When you download a Git repository, many times you're interested in going to the GitHub (or GitLab, or BitBucket… you get the idea) repository. Maybe you want to use Merge Requests, or comments, or raise an issue…

You can get the URL with the git command

```bash
git config --get remote.origin.url
```

This URL can be directly used in a macOS open command like this:

```bash
open $(git config --get remote.origin.url)
```

But that is only true if the reported URL is an HTTP-based one, and sometimes repositories have been downloaed using SSH. Also, the `git config` syntax is difficult to remember, so I created a helper bash/zsh function `git-url` which is availble as a GitHub Gist:

<script src="https://gist.github.com/juandesant/df06131666d80c34c6b9a7a9a7c1ea61.js"></script>

Hope that is useful for you… I know I find it useful for me!