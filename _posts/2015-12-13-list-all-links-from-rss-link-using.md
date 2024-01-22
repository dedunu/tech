---
layout: post
title: List all the links from RSS link using Python
---

Blogs and news sites use RSS(Rich Site Summary) feeds. Python can be used to fetch updates. I have written a simple program which can fetch RSS feed and print links.

I have written the same application in both Python 2.7 and Python 3 both

```python
import urllib2
from xml.dom import minidom

__author__ = 'dedunu'


class Reader:
    def get_url_list(self, url_string):
        data = urllib2.urlopen(url_string)
        rss_string = ''
        for line in data:
            rss_string = rss_string + line

        doc = minidom.parseString(rss_string)
        article_list = doc.getElementsByTagName('item')

        link_list = []

        for item in article_list:
            link_list.append(item.getElementsByTagName('link')[0].firstChild.data)

        return link_list


# Example
reader = Reader()

url_list = reader.get_url_list('http://feeds.feedburner.com/TechCrunch/')
for url_item in url_list:
    print url_item
```

In Python 3, `urllib2.urlopen()` is replaced with `urllib.request.urlopen()`. Python 3 code is mentioned below.

```python
from urllib.request import urlopen
from xml.dom import minidom

__author__ = 'dedunu'


class Reader:
    def get_url_list(self, url_string):
        data = urlopen(url_string)
        rss_string = b''
        for line in data:
            rss_string = rss_string + line

        doc = minidom.parseString(rss_string)
        article_list = doc.getElementsByTagName('item')

        link_list = []

        for item in article_list:
            link_list.append(item.getElementsByTagName('link')[0].firstChild.data)

        return link_list


# Example
reader = Reader()

url_list = reader.get_url_list('http://feeds.feedburner.com/TechCrunch/')
for url_item in url_list:
    print(url_item)
```

#### Gistss

- <https://gist.github.com/dedunumax/4856150e6fc8a7fe5216>
- <https://gist.github.com/dedunumax/29858412bc0dd494520f>

### Tags

- python
- rss
- python3
