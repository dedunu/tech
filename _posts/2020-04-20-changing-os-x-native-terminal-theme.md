---
layout: post
title: Changing OS X native Terminal theme from commands
---

I used iTerm2 for a while. But it is taking a lot of memory. I wanted to configure the native terminal application on OS X.

I have a virtual box and I used it for my development. I connect to a bridge to access production. I wanted the terminal to change colours/themes when I log in to each and every host. 

I downloaded a few themes from this repository: [https://github.com/lysyi3m/macos-terminal-themes](https://github.com/lysyi3m/macos-terminal-themes). Imported them to OS X terminal application.

Since I am using `zsh`, I added below code to `.zshrc`. If you are on `bash` please change `.bash_profile` on your mac.

```bash
function virt() {
  osascript -e "tell application \"Terminal\" to set current settings of front window to settings set \"Ubuntu\""
  ssh -Ap 5001 vuser@virtual-server
  osascript -e "tell application \"Terminal\" to set current settings of front window to settings set \"One Dark\""
}
```

Then I change `.zshrc` on my virtual server again. It calls my mac to change the active profile.

```bash
function prod() {
  ssh -A luser@laptop -C 'osascript -e "tell application \"Terminal\" to set current settings of front window to settings set \"Red Alert\""'
  ssh -A buser@bridge.company.org
  ssh -A luser@laptop -C 'osascript -e "tell application \"Terminal\" to set current settings of front window to settings set \"Ubuntu\""'
}
```

I use password-less login on all the servers. It makes it bit slower when you log-off and log-in.

> Missing Image

### Tags

- terminal
- mac
- osx
