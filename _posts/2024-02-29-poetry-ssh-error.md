---
layout: post
title: "Poetry fails with an SSH error"
---

One of my collegues has an issue with poetry. Error message is mentioned below.

```console
ssh: Could not resolve hostname https: Name or service not known
```

We found out that `.gitconfig` has an empty `http.proxy` section.

```ini
[user]
	name = John Doe
	email = John.Doe@example.com
[http]
	proxy = 
```

We removed last two lines. It worked! 

### Tags

- git
- python
- poetry
