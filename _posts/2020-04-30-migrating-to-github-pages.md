---
layout: post
title: Migrating to Github Pages
---

My blog has been living on self-hosted Wordpress, `wordpress.com` and `blogger.com`. But I have migrated it several times at the cost of losing posts and even domain names. But I have been holding `dedunu.info` since 2011. 

Recently Blogger is testing a new editor which doesn't support HTML editing. I started to worry about that.  I already had the personal site running on Github Pages. Moving to Github sounds sensible.  Github Pages offers HTTPS support for custom domains, just like the Blogger did.

If you want to do a blog on Github pages, [Jekyll](https://jekyllrb.com/) is the ultimate answer. Jekyll has out-of-the-box support for coding related blog posts. Using Markdown is cleaner than using Blogger editor. 

Migration was smooth. I could import all the blog posts with one command with blogger URLs.

```ruby
$ ruby -r rubygems -e 'require "jekyll-import";        
  JekyllImport::Importers::Blogger.run({
   "source"                => "/home/dedunu/blog-04-21-2020.xml",
   "no-blogger-info"       => false, 
   "replace-internal-link" => false, 
  })'
```

[Sidey](https://github.com/ronv/sidey) theme was my choice. A minimal theme for Jekyll with ultra-fast page loading. 

The only change, I had to do was enable pagination. Find [the Github repository here](https://github.com/dedunu/dedunu.github.io).

### Tags

- blog
- git
- github
- blogger
