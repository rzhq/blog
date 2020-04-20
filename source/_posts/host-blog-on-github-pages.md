---
title: Host blog on Github Pages
date: 2020-04-19 14:35:51
tags:
---

This article describes how the blog was generated using Hexo and hosted by Github Page.

### Setup Hexo

The tutorial on Hexo’s home page is pretty intuitive.

``` bash
$ npm install hexo-cli -g
$ hexo init blog
$ cd blog
$ npm install
$ hexo server
```

Now everything needed with Hexo is stored in the `blog` folder and the blog can be accessed via [http://127.0.0.1:4000](). Configurations can be set to `_config.yml` as needed. Noted now the blog only can be locally accessed for testing.

### Setup Github Pages

To host a website on Github Pages, a repository named `<user>.github.io` needs to be created on Github. `<user>` is the username on Github.
By default, a repo on Github only has one branch `master`. This branch is where the contents of the website will be placed and hosted by Github Pages. Another branch `hexo` will be created to store all the Hexo codes.

After the `hexo` branch was created. Cloned this branch from Github to local. `<user>` is the username on Github.

``` bash
$ git clone git@github.com:<user>/<user>.github.io.git -b hexo hexo
```

Copy everything inside the `blog` folder to the newly created `hexo` folder.

``` bash
$ cp -r blog/. hexo/
$ cd hexo
```

All the following work will be conducted within the `hexo` folder. The `blog` folder can be deleted.
After setting up the branches it's time to publish the contents for Github Pages to host the website.
Modify the `deploy` section in the `_config.yml` file adding the following information. `<user>` is the username on Github.

``` yml hexo/_config.yml
deploy:
  type: git
  repo: git@github.com:<user>/<user>.github.io.git
  branch: master
  message: update blog
```

This section is to tell Hexo to use git as deployment method and publish the content generated to this repository's master branch. In order to deploy via git, another package `hexo-deployer-git` need to be installed via npm. After which the content can be deployed to `master` branch with `hexo deploy`. Execute the following command in the `hexo` folder.

``` bash
$ npm install hexo-deployer-git
$ hexo deploy
```

Now the generated content had already been deployed to the repo and automatically hosted by Github Pages. The blog can be accessed via `http://<user>.github.io`
At this stage the blog is fully functional. The command `hexo deploy` needs to be executed every time a new post was created, to update the repo hence update the website.
