---
layout: post
title: Python: Using MFA Cache with boto3 and botocore
---

I wanted to develop a CLI tool using `boto3`. If MFA is enabled, it will keep asking for a token every time application tries to create a new session. It is a bit annoying to enter the token every time. I found a way to reuse the credential cache.

We will need both `boto3` and `botocore` modules. `boto3` no longer has the ability to create a session alone from the cache.  

```python
#!/usr/bin/env python3
import os

from boto3 import Session
import botocore

PROFILE_NAME = 'staging'
REGION = 'eu-west-1'


def print_all_the_buckets(profile_name, region):
    boto_core_session = botocore.session.Session(
        profile=profile_name
    )

    provider = boto_core_session.get_component('credential_provider').get_provider('assume-role')

    cache = os.path.join(
        os.path.expanduser('~'),
        '.aws/' + profile_name + '/cache'
    )

    provider.cache = botocore.credentials.JSONFileCache(cache)

    boto_session = Session(
        botocore_session=boto_core_session,
        profile_name=profile_name
    )

    client = boto_session.client('s3', region_name=region)

    bucket_list = client.list_buckets()

    for bucket in bucket_list['Buckets']:
        print(bucket['Name'])


print_all_the_buckets(PROFILE_NAME, REGION)
```

### Tags

- python
- aws
- boto
- credentials
- cache