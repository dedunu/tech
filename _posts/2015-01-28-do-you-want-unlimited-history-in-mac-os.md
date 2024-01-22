---
layout: post
title: "Do you want Unlimited history in Mac OS X Terminal?"
---

Back in 2013, I wrote [a post about expanding terminal history unlimited](http://www.dedunu.info/2013/06/do-you-want-unlimited-history-in-linux.html). Recently I moved from Linux to Mac OS. Then I wanted unlimited history. Usually, in Mac OS X you will only get 500 entries in history. New entries would replace old entries.

Take the terminal window and type below command.

```console
$ open ~/.bash\_profile
```

or 

```
$ vim ~/.bash\_profile
```

Most probably you will get an empty file. Add below lines to that file. If the file is not empty add them in the end.

```bash
export HISTFILESIZE=
export HISTSIZE=
```

Next, you have to save the file. Close the terminal and get new terminal windows. Now onwards your whole history would be stored in the `~/.bash_history` file.

### Tags

- terminal
- terminal history
- Mac