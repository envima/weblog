---
layout: post
date: 2019-07-15 14:40
title: Build a Jekyll page
tags: jekyll marvin
category: tutorial
---

Jekyll runs on ruby. A good installation guide can be found here: [https://jekyllrb.com/docs/installation/](https://jekyllrb.com/docs/installation/)


### Jekyll Templates

The easiest way to set up a webpage is using a jekyll site template.
Here are some links with free themes:

[http://jekyllthemes.org/](http://jekyllthemes.org/)
[https://jekyllthemes.io/free](https://jekyllthemes.io/free)


This site uses the [MatJek Theme](http://jekyllthemes.org/themes/matjek/). 


### Get the site on GitHub

Create a new repository in your GitHub account and initialize it with a readme. GitHub offers a .gitignore template for jekyll pages - use it.  The name of the repository will be part of the link to the webpage. In our case, the repository is called **weblog**, so the webpage is accessible under [envima.github.io/weblog](http://envima.github.io/weblog)

Clone the repositiory to your local drive. 

```bash
git clone https://github.com/envima/weblog.git
```
Copy and paste the downloaded jekyll theme into the repository. Locally we can already build the webpage now with `bundle exec jekyll serve` and entering the adress ` http://127.0.0.1:4000/weblog/` in a browser.

Commit the changes and push them to GitHub.

```bash
git add --all
git commit -a -m "page skeleton"
git push origin master
```

On GitHub, go to the repository settings. In the section GitHub pages choose the master-branch as the source for page building.

### _config.yaml

Now we need to do some changes in the **_config.yaml** file that came with the template. Most of the entries are self explainatory and differs from theme to theme. The most important change to get the site running is the **url** and **baseurl**.

```yaml
baseurl: "/weblog"
url: "https://envima.github.io"
```










