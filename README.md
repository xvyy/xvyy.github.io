# [vpromise's blog](https://vpromise.github.io)
<https://vpromise.github.io/>

thanks to [Voyager](https://github.com/redVi/voyager)

edit by [vpromise](https://github.com/vpromise)


### Feathures:

All HTML files are compressed (see `_layouts/compress.html`).

**Post**

All post settings can be changed. Example:

```
---
layout: post
bg: 'photo01-77.jpg'
title: "Post Heading"
crawlertitle: "page title"
summary: "post description"
date: 2019-06-29 00:00:00 +08000
tags : "Ubuntu deep-learning markdown ..."
slug: post-url
categories: "tech life paper code knoeledge ..."
author: "vpromise"
---
```

`bg` is a path to background of your article. By default backgrounds are placed in the `assets/images` directory.

**Page**

If page contains `active` tag, it will be show on site menu.

```
---
layout: page
title: "About"
permalink: /about/
active: about
---
```
Archive page is sorting posts by tags. No more than one tag in one post.


