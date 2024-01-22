---
layout: post
title: "How to fix InsecurePlatformWarning on Ubuntu?"
---

Python modules sometimes give issues. We got below warning from a python application.

```python
/usr/local/lib/python2.7/dist-packages/requests/packages/urllib3/util/ssl_.py:120: 
  InsecurePlatformWarning: A true SSLContext object is not available. This 
  prevents urllib3 from configuring SSL appropriately and may cause certain SSL 
  connections to fail. For more information, 
  see https://urllib3.readthedocs.org/en/latest/security.html#insecureplatformwarning.
  InsecurePlatformWarning
```

After small research we found out, this might be an issue related to the outdated module. We ran below commands in that server. After that warning didn't occur.

```console
$ sudo apt-get install build-essential python-dev libffi-dev libssl-dev
$ sudo pip install --upgrade ndg-httpsclient
```

### Tags

- Ubuntu
- pip
- python
