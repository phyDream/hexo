
---
title: Markdown图床的选择
date: 2017-9-12 11:39:01
tags: [blog,Markdown,图床]
categories: [技术探索]
---
![image](http://ow0s809ce.bkt.clouddn.com/youdao.png)  

<center>强烈推荐，[有道云笔记](http://note.youdao.com/semdl/markdown.html?vendor=unsilent14)的Markdown功能，实现多客户端同步编写，以及在线预览</center>

<!-- more -->

# 国内图床

- [七牛](https://www.qiniu.com) &emsp; 收费
- [微博图床](http://photo.weibo.com)
- [极简图床](http://jiantuku.com/#/)
- [贴图库](http://www.tietuku.com/)

# 其他解决方案

- 直接获取有道云笔记内的图片链接  （参考于两篇博客）


> 在Markdown文档的编辑中，图片需要一个资源地址，你可以使用网络链接也可以使用本地路径，但是本地路径在你更换电脑，或者云端浏览的时候就会失去作用，无法查看图片。针对这个问题，很多人的解决办法是使用一个图床，比如付费的七牛，免费的微博图床、极简图床等，就是将你的图片上传到这些网站，它们会生成一个此图片的URL，然后你就可以在Markdown中使用此URL来使用图片。由于我平时使用有道云笔记进行记载笔记，所以我采用了如下方法：在有道云笔记中单独建立一个资源文件，然后将所引用的图片粘贴进去，点击上方共享按钮，获得共享URL，在浏览器中打开这个链接，按F12,在源码中找到图片对应的链接。不过这个查找过程有点麻烦，还需要有一定的编程基础，所以下面链接的一位博主写了一个脚本，来自动做这件事。  

1. [实现原理介绍](http://www.tucao.tv/play/n6124/)  （转载）

2. [脚本下载以及使用说明](http://blog.csdn.net/u013119744/article/details/74898032)（转载）




