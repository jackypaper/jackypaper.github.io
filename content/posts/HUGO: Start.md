---
title: "HUGO: Start"
date: 2018-03-11T17:28:23-04:00
draft: false
tags: [hugo]
categories: [tech]
---
Basically follow the **hugo** official [Quick Start](https://gohugo.io/getting-started/quick-start/).
```bash
# for MacOS
brew install hugo
# check hugo version
# Hugo Static Site Generator v0.37.1 darwin/amd64 BuildDate:

# step 1
hugo new site <Username>.github.io
cd <Username>.github.io
git init
# git add .
# git commit -m 'create github page repo'
# git push origin master

# step 2
git branch dev
git checkout dev
# theme: code-editor
git submodule add https://github.com/aubm/hugo-code-editor-theme.git themes/code-editor
# or git clone ...
# Be careful! the theme name should be consistent with the one in config.toml.
echo 'theme = "code-editor"' >> config.toml
# or as the theme owner suggests
```
```toml
baseurl = "http://your-site.com"
languageCode = "en-US"
title = "Your site"
theme = "code-editor"

[params]
    author = "name"
    locale = "en-US"
    # rootlink = "/"
    # rootlink specifies where Root in menu.html links to. If it's not set then baseurl will be used.
```
```bash
# step 3
hugo new posts/my-first-post.md
# preview including drafts
hugo server -D
# if everything's ready, edit `draft: true`
# control + c to exit local preview
```
```bash
# step 4
# remove `public` folder if it exists
hugo --theme=code-editor --baseURL=https://<username>.github.io/
# update dev branch if you want

# step 5
# move all files & folders of `public` folder to master branch
git checkout master
# overwrite master branch!
git add .
git commit -m 'my first post'
git push origin master
```
reference:
- [**code-editor** theme page](https://themes.gohugo.io/hugo-code-editor-theme/)
