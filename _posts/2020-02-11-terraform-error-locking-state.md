---
layout: post
title: "Terraform: Error locking state"
---

If you have Terraform state locks. Sometimes cancelling terraform commands ungracefully might leave the state file locked. This is the error you would usually see if the lock is not released.

```console
Acquiring state lock. This may take a few moments...

Error: Error locking state: Error acquiring the state lock: ConditionalCheckFailedException: The conditional request failed
 status code: 400, request id: L2CH7KK3QCAEHSC1TJ1VLBMNBRVV4CQNSO5AEMVJY66Q9ASUAAJN
Lock Info:
  ID:        21e2b2bb-c123-2383-eece-7a5eaab4f645
  Path:      s3/path/to/the/state/file
  Operation: OperationTypePlan
  Who:       username@hostname
  Version:   0.11.14
  Created:   2020-02-11 11:26:58.602608 +0000 UTC
  Info:


Terraform acquires a state lock to protect the state from being written
by multiple users at the same time. Please resolve the issue above and try
again. For most commands, you can disable locking with the "-lock=false"
flag, but this is not recommended.
```

If you want to release this lock. You should run below command. Then type "`yes`" and hit enter.

```bash
$ terraform force-unlock <LOCK ID>
```

For example: 

```bash
$ terraform force-unlock 21e2b2bb-c123-2383-eece-7a5eaab4f645
```

![screenshot](https://1.bp.blogspot.com/-FdxbUOvKOqk/XkLR2yPbJTI/AAAAAAAAGfU/0MSPTvCxqF4zHsDVEW7dmYAUeCjEB6AaACLcBGAsYHQ/s1600/Screenshot%2B2020-02-11%2Bat%2B1.29.08%2BPM.png)

> Warning: Please don't release this lock, unless you are the once who caused it. It might corrupt the state file.

### Gists

- <https://gist.github.com/dedunumax/19cbb46ed1bca17f9d9c49bf5dd44b4a>

### Tags

- aws
- terraform