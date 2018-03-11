---
title: "HUGO: Add Tags & Categories"
date: 2018-03-11T18:08:36-04:00
draft: false
tags: [hugo]
categories: [tech]
---

In `config.toml`, add
```toml
[taxonomies]
   tag = "tags"
   category = "categories"
```
In your posts, add the following lines in the config header.
```markdown
tags: [hugo]
categories: [tech]
```
Try more complicated nested tag structures if you have more energy...


reference:
  - [taxonomies](https://gohugo.io/content-management/taxonomies/)
  - [Hugo support: how to add tags](https://discourse.gohugo.io/t/how-to-add-tag-and-category/3202/6)
