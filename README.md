[![Build Status](https://travis-ci.org/luffySAMA/luffySAMA.github.io.svg?branch=source)](https://travis-ci.org/luffySAMA/luffySAMA.github.io)


本博客创建于`2018-08-28`，用 [Hexo](https://hexo.io/zh-cn/) + [Github Pages](https://pages.github.com/) + [Travis](https://travis-ci.org/) 搭建，目的是分享自己的技术，也敦促自己要多多学习。

`source` 分支：博客的源码

`master` 分支：使用 Hexo 编译后的代码，用于部署到 Github Pages 上

每次 source 分支有新的 commit，travis 就会自动调用 Hexo，然后把编译后的代码 push 到 master 分支，这样网站就自动更新了。