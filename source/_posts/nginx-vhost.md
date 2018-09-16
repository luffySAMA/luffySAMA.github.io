---
title: 如何在一台服务器上部署多个网站或应用
date: 2018-09-16 22:51:00
tags: nginx
categories: 经验总结
---

最开始我租服务器的目的和许多人一样——想去看看“外面”的世界。当我实现这个小目标之后，我发现我对服务器的资源利用率  其实是非常低的，换句话说，我太浪费了。我开始思考我应该可以用这台服务器干更多的事情，比如在上面建个网站、写写博客、还可以搭一个私有云盘……等等等等

此时我遇到一个问题，我该怎样把这几个东西部署在同一个服务器上呢？如果我的网站是在 80 端口，博客是在 8080 端口，然后我的私有云盘是在 3000 端口，那我每次访问的时候，都得在我的域名后面接上一个端口号。这样不仅我自己用的时候不方便，而且我把链接发给别人的时候，也会让人感觉怪怪的……

我想要是我能用不同的域名指向不同的端口号就好了，然而事实上这种做法是行不通的，原因是域名解析的时候，只能将域名指向某个 ip，不能指定端口号。

后来我发现使用 **Nginx** 可以很轻松地解决上面的问题。

<!-- more -->

## 在一台服务器上部署多个网站

例如，在一个服务器上，托管了多个博客，类似于 github 的 gh-pages。当我  用 lucy.blog.com 访问的  时候，看到的是 lucy 的 blog，当我用 lily.blog.com 访问的时候，看到的是 lily 的 blog。

如果博客是静态的，那么很简单，不需要用到多个端口， 用 Nginx 的虚拟主机(virtual host)功能就可以 轻松搞定。

具体实现：

首先启动  Nginx，运行在 80 端口。此时访问 80 端口，看到的是 Nginx 默认的欢迎界面，它的源文件在服务器的 `/usr/share/nginx/html` 目录下。

在这个  目录的同级的地方，建两个新的文件夹分别为`/usr/share/nginx/lucy` 和 `/usr/share/nginx/lily`。 然后把 lucy 的博客文件传到 `lucy` 文件夹里，把 lily 的博客文件传到 `lily` 文件夹里。

接着打开 Nginx 的配置文件 `/etc/nginx/nginx.conf`，找到 `http` 部分，在最后加上下面这行（如果没有的话）

```nginx
http {
    include /etc/nginx/conf.d/*.conf;
}
```

然后在 `/etc/nginx/conf.d` 目录里面创建一个 `lucy.conf` 文件，在 `lucy.conf` 里面写上下面这段代码

```nginx
server {

  listen 80;
  server_name lucy.blog.com;

  location / {
    root   /usr/share/nginx/lucy;
    index  index.html index.htm;
  }

}
```

运行

```bash
nginx -s reload
```

重新加载配置

这样当浏览器访问 lucy.blog.com 时，就会返回`/usr/share/nginx/lucy/index.html` 的内容。

同理创建一个 `lily.conf`，在 `lily.conf` 里面写入

```nginx
server {

  listen 80;
  server_name lily.blog.com;

  location / {
    root   /usr/share/nginx/lily;
    index  index.html index.htm;
  }

}
```

运行

```bash
nginx -s reload
```

重新加载配置

这样当浏览器用 lily.blog.com 访问服务器时，就会返回 `/usr/share/nginx/lily/index.html` 的内容

## 在一台服务器上部署多个应用

另一种情况是，同一个服务器上部署了 2 个应用，分别运行在不同的端口，例如 tomcat 运行在 8080，nodejs 运行在 3000。这时候希望用域名而不是端口号来访问这两个应用，tomcat.abc.com 访问的就是 tomcat，nodejs.abc.com 访问的就是 nodejs。

做法一样很简单，和上面的情况类似， 在 `conf.d` 目录下创建两个配置文件

`tomcat.conf`

```nginx
server {

  listen 80;
  server_name tomcat.abc.com;

  location / {
    proxy_pass   http://localhost:8080;
  }

}
```

`nodejs.conf`

```nginx
server {

  listen 80;
  server_name nodejs.abc.com;

  location / {
    proxy_pass   http://localhost:3000;
  }

}
```

创建完成后运行

```bash
nginx -s reload
```

成功！
