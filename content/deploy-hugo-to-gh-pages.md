---
title: "Deploy Hugo to Gh Pages"
date: 2022-11-29T22:19:37-06:00
draft: false
tags: ['til', 'hugo', 'github', 'git']
---

Today I learned how to share my hugo site with the internet using the free hosting provided by github (aka github pages). It wasn't the most intuitive process, but I got it setup after a little effort and googling.

1. The first step was to setup git in the project using `git init`.
2. Commit and push code. 
3. Fork the theme.
4. Add theme as a submodule `git submodule add https://github.com/bsheps/lugo.git themes/lugo`

    *Note: if git is complaining about submodule already existing, remove it and re-add themes/lugo. `git rm --cached themes/lugo`*

5. Setup a github action to trigger on pushes to master branch.
6. Specify site url in config.toml: `baseURL = 'https://bsheps.com/til'`
