---
layout: post
title: "Remove all the followers from your twitter account"
---

You might use social networks more often. All of us know that it is really hard to do bulk operations on Facebook and Twitter.

I wanted to remove all the followers from my twitter account. So I googled it. Then I found there is no way to remove followers. The only way is blocking them and unblocking them. But this way if you are following that person, your subscription will be removed automatically.

I tried to do this with "tweepy" Python module. You can modify the program as you need. Please be careful when you run this script, you are going to lose all your followers. To get consumer and access token keys, please visit [https://apps.twitter.com/](https://apps.twitter.com/). Make your keys safe, never share your keys publicly.

```python
import tweepy

__author__ = 'dedunumax'

consumer_key = '<consumer_key>'
consumer_secret = '<consumer_secret>'
access_token = '<access_token>'
access_token_secret = '<access_token_secret>'

auth = tweepy.OAuthHandler(consumer_key, consumer_secret)
auth.set_access_token(access_token, access_token_secret)

api = tweepy.API(auth)

followers_list = api.followers_ids(api.me())

for user in followers_list:
    api.create_block(user)
    api.destroy_block(user)
    print user
```

### Gists

- <https://gist.github.com/dedunumax/91992ac6f1940be5d391>

### Tags

- remove followers
- python
- Twitter
- tweepy