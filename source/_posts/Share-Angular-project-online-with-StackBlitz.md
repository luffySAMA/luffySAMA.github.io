---
title: 在线分享 Angular 项目 —— StackBlitz
date: 2018-08-29 21:32:50
tags:
---

![stackblitz](/images/Share-Angular-project-online-with-StackBlitz/stackblitz.png)

上一篇博客，我介绍了 codepen，那是一个很棒的网站，我能用它来分享静态页面，但是如果想分享一个复杂一点的东西，比如说，一个 Angular 插件，那 codepen 可能就显得力不从心了。过去一般使用 [http://plnkr.co/](http://plnkr.co/) 这个网站来分享 Angular 的代码。但是要让 Angular 在这个网站上运行，又是引用 system.js，又是加载 UMD 模块，跟平时我们开发的时候有点不太一样，说实话我还是有点懵逼，我还是喜欢 `ng serve` 这样的方式来启动 Angular。

这个时候，**[stackblitz](https://stackblitz.com)** 横空登场……

<!-- more -->

它是一个基于 vscode 的在线代码编辑器。它不仅能在网页上编辑代码，更重要的是，它自带了 npm 和 ng-cli，直接在上面运行 Angular 代码完全没有问题，不需要做任何修改。

![angular-code](/images/Share-Angular-project-online-with-StackBlitz/angular-code.gif)

在这里，我可以获得和 vscode 差不多((¬_¬)~~真的吗~~)的体验，自动提示，热更新等。

它甚至还可以直接把 github 上的项目直接拿过来运行，只需要简单地修改一下 url。WOW！简直太不可思议了！

![github](/images/Share-Angular-project-online-with-StackBlitz/github.gif)

---

嗯……上面几张图都是从 stackblitz 官方博客中拷过来的，下面放一个我自己写的，一个特别特别简单的轮播图……

<iframe src="https://stackblitz.com/edit/angular-simple-carousel?embed=1&file=src/app/app.component.html&hideNavigation=1" width="100%" height="500" scrolling="no" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>

等我以后写出什么开源的 Angular 插件的时候，再来分享给大家。
