+++
css = []
date = "2017-07-01T23:35:17+08:00"
description = ""
draft = false
highlight = true
scripts = []
tags = ["hugo"]
title = "Migrate to Hugo"

+++

Due to some software issues not fixing for long time on logdown.com [2], I decided to finding other blog solutions for hosting my tech blog. After considering several options (Such as Hugo, Ghost, Octopress, Jekyll, Jekyll-Now). The final choice goes to Hugo. Hugo is a popular static website generator which built on top of Golang. The community support is actively. Over 18 thousands stars on Hugo github repository. And Debian/Ubuntu has hugo packages which is very easily for normal user to install.

For migrating to Hugo, I exported all my articles on logdown, which content is served with similar format to Octopress. And then dump all the markdown files into content/post/ folder in newly created hugo repository. Everything went well except two steps were needed.

1. I used sed script in [1] to change date format, otherwise the hugo will print parsing error.
2. Remove all the 

```
layout: post
```
line in the octopress markdown article

In fact I spent some time (more thant I expected) to select the Hugo theme. At begining none of the themes seems fit my need (Easy setup, Large font, Readibility, Clear article information such as date information).


hugo-geo

* Pro: Great design, Great Readibility.
* Cons: Lack of date and tag information in article page. Only summary in front page.

hyde-x

* Pro: Simple. Allow showing full article in index.html.
* Cons: Lack of hugo tag support.

Finally I decided to use [hugo-geo](https://themes.gohugo.io/hugo-geo/) theme which is great. And customized hugo-geo by adding my personal wanted features:

1. Show date information in article and list pages.
2. Show tag information in article
3. Show full article in front page.

Customized hugo-geo: https://github.com/swem/hugo-geo

Will file pull request about 1. feature to upstream later. (Which I think might benefit a lot users.)

[1] https://jaketrent.com/post/conversion-from-octopress-to-hugo/

[2] I can't login via facebook account. This feature have been broken for nearly half year. Another feature broken is url auto-generate.
