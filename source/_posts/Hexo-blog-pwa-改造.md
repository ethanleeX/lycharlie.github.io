---
title: Hexo blog PWA 改造
date: 2018-09-01 21:18:30
tags: 
- hexo
- blog
- pwa
---

# 简介

Progressive Web App, 简称 PWA，是提升 Web App 的体验的一种新方法，能给用户原生应用的体验。
其实 PWA 的特点和好处网上有很多资料，这里不再赘述。

- [Google PWA 文档](https://developers.google.com/web/progressive-web-apps/)
- [百度 lavas PWA 文档](https://lavas.baidu.com/pwa/README)

# 改造要点

改造要要点主要包括下面这些，

- https 支持
- manifest 文件
- 缓存

# https 支持

支持 https 是使用 PWA 的必要条件，所以首先需要我们的blog 支持 https。
我的 blog 用的是 github page,所以需要在github的设置上开启 https 的支持。
![img](http://7xr3nz.com1.z0.glb.clouddn.com/image/blog/Hexo-blog-PWA-%E6%94%B9%E9%80%A0/Screen%20Shot%202018-09-01%20at%2023.28.47.png)

# manifest

manifest 文件是 PWA 的配置文件，可以配置桌面图标等，这样就可以像打开 app 一样打开 PWA.
在 hexo blog /source 目录下添加 manifest.json 文件

``` json
{
  "name": "EthanLee's blog",
  "short_name": "EthanLee",
  "theme_color": "#0097A7",
  "background_color": "#FFFFFF",
  "display": "standalone",
  "Scope": "/",
  "start_url": "/",
  "icons": [
    {
      "src": "images/icons/icon-72x72.png",
      "sizes": "72x72",
      "type": "image/png"
    },
    {
      "src": "images/icons/icon-96x96.png",
      "sizes": "96x96",
      "type": "image/png"
    },
    {
      "src": "images/icons/icon-128x128.png",
      "sizes": "128x128",
      "type": "image/png"
    },
    {
      "src": "images/icons/icon-144x144.png",
      "sizes": "144x144",
      "type": "image/png"
    },
    {
      "src": "images/icons/icon-152x152.png",
      "sizes": "152x152",
      "type": "image/png"
    },
    {
      "src": "images/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "images/icons/icon-384x384.png",
      "sizes": "384x384",
      "type": "image/png"
    },
    {
      "src": "images/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ],
  "splash_pages": null
}
```

有很多网站可以帮我们自动生成 manifest.json 文件

- [Web App Manifest Generator](https://app-manifest.firebaseapp.com/)
- [Web App Manifest Generator](https://tomitm.github.io/appmanifest/)

manifest.json 文件生成好之后需要在 header 引用，找到主题对应的 header 代码，在 header 中引用即可

``` html
<link rel="manifest" href="/manifest.json">
```

添加完 manifest 之后我们用 chrome 打开 blog 就能在桌面上添加快捷方式。（chrome 为了用户体验 只有在段时间内多次打开网页才会提示添加作业面快捷方式，如果想自己主动添加可以在设置中进行）
![img](http://7xr3nz.com1.z0.glb.clouddn.com/image/blog/Hexo-blog-PWA-%E6%94%B9%E9%80%A0/WechatIMG24.jpeg)

# 缓存资源

这个是 PWA 最重要的部分，是 PWA 可以离线浏览的原因,也是 PWA 体验优于普通 web app 的原因。我们需要生成一个 ServiceWorker 文件处理缓存相关逻辑。 hexo 有一个叫 [hexo-offline](https://github.com/JLHwung/hexo-offline#readme) 的插件可以帮我们做这部分工作，安装好后根据官网的提示操作即可。完成缓存之后我们就能够实现离线访问，即使在断网的情况下我们也能访问 blog 的内容。

# 总结

到这里为止我们的 blog 就改造成了 PWA. 我们用 lighthouse 跑个分
![img](http://7xr3nz.com1.z0.glb.clouddn.com/image/blog/Hexo-blog-PWA-%E6%94%B9%E9%80%A0/Screen%20Shot%202018-09-02%20at%2002.19.55.png)

如果发现文章中有错误，欢迎指正