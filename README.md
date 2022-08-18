# [vpromise's blog](https://xvyy.github.io)
<https://xvyy.github.io/>
<https://vpromise.xyz>

Thanks to [Voyager](https://github.com/redVi/voyager)
Demo: <http://redvi.github.io/voyager>

edit by [vpromise](https://github.com/vpromise)

![My GitHub](https://github-readme-stats.vercel.app/api?username=vpromise&bg_color=00f2fe,00f2fe,4facfe&title_color=fff&text_color=fff)


### Feathures:

All HTML files are compressed (see `_layouts/compress.html`).

**Post**

All post settings can be changed. Example:

```
---
layout: post
bg: 'photo***.jpg'
title: "Post Heading"
crawlertitle: "page title"
summary: "post description"
date: 2019-06-29 00:00:00 +08000
slug: post-url
categories: "tech life paper code knoeledge ..."
tags : "Ubuntu deep-learning markdown ..."
author: "vpromise"
---
```

`bg` is a path to background of your article. By default backgrounds are placed in the `assets/images` directory.

categories: "technology academic life others"
tags : "any detailed tags: ubuntu, ssh, samba ..."

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

Good:

```
tags : ['front-end']
```

Bad:

```
tags : ['front-end', 'jekyll']
```

Don't forget to change `_config.yml`.

**Relative paths**

If your blog is not in the root directory, you can include images with a relative path. For example:

```
![my_image]({{ site.images | relative_url }}/image.jpg)
```

## Production environment

Build for production:

`JEKYLL_ENV=production jekyll build`
