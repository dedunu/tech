---
layout: post
title: macOS Catalina Disaster and how to recover
---

I upgraded to Catalina last week. I have three major issues with the new version.

- Screenshots app doesn't work
- Dock is gone
- Slack notifications don't work

***

**Screenshots app doesn't work**

I ruled down the screenshot issue is due to new permission scheme. But I couldn't find a fix. But I found a workaround. I use screenshots to share with Slack usually, but it might not work for you.

Press `CMD+Space`.

![screenshot1](https://1.bp.blogspot.com/-nEec3w4QOcU/Xa14EaCOziI/AAAAAAAAGc0/n_J9Hzz_sTU05z1WYiHdlHA_AgJJlk5lQCLcBGAsYHQ/s1600/image.png)

Click on "`Option`" and select Clipboard. Next time when you want a screenshot use usual shortcuts `CMD+Shift+3` or `CMD+Shift+4` and paste on Slack chatbox or Word document.

***

**Dock is gone**

There are two solutions to this problem. First is running below command in the shell.

```console
$ defaults delete com.apple.dock; killall Dock
```

or

`CMD+Option+D`

***

**Notifications don't work**

Open "`System Preferences`". Click on "`Notifications`". Select the application you want notifications from. Click "`Allow Notifications from <Application Name>`"

![screenshot2](https://1.bp.blogspot.com/-Jw_x4XbgRcs/Xa158L8S2bI/AAAAAAAAGdA/mpctBs0T144SgYj15Ym6ggIcuHmXZ7EdwCLcBGAsYHQ/s1600/image%2B%25281%2529.png)

### Tags

- osx
- Mac
- catalina