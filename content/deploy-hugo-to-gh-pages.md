---
title: "Deploy Hugo to Gh Pages"
date: 2022-11-29T22:19:37-06:00
draft: false
tags: ["til", "hugo", "github", "git"]
---

Today I learned how to share my hugo site with the internet using the free hosting provided by github (aka github pages). It wasn't the most intuitive process, but I got it setup after a little effort and googling.

1. The first step was to setup git in the project using `git init`.
2. Commit and push code.
3. Fork the theme.
4. Replace old lugo theme and clone the forked theme repo.
5. Add theme as a submodule `git submodule add https://github.com/bsheps/lugo.git themes/lugo`

   _Note 1: if git is complaining about submodule already existing, remove it and re-add themes/lugo. `git rm --cached themes/lugo`_

   _Note 2: if [cloning the project](https://git-scm.com/book/en/v2/Git-Tools-Submodules#_cloning_submodules) for first time after awhile, run `git submodule init` to initialize and `git submodule update` to fetch the data._

6. In config.toml set theme `theme = 'lugo'`
7. On the github website for the repo, select settings > Pages. In source dropdown, select github actions and work through the prompt.
8. Commit the created hugo.yml github action file.
9. Voila! The site should be automatically build and publish publicly to the world.
