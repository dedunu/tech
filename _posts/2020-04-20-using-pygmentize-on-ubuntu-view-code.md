---
layout: post
title: "Using pygmentize on Ubuntu view code files"
---

On the terminal, viewing code with colour might improve productivity. You can use `pygmentize` to view code in colour. Install `pygmentize` using below commands.

```bash
$ sudo apt install python3-pip
$ pip3 install Pygments
```

You can use view code using:

```bash
$ pygmentize -g /etc/profile.d/gawk.sh
```

If you add an alias like below you will be able to use `pygmentize` as a short command to your `.bashrc` or `.zshrc`.

```bash
alias ccat='pygmentize -g '
```

> Missing Image

# Tags

- terminal
- Ubuntu
- cli