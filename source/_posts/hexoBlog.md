
---
title: 属于你自己的博客
date: 2017-09-07 11:47:55
tags: [blog,github,hexo]
categories: [技术探索]
---
![image](http://ow0s809ce.bkt.clouddn.com/github_hexo.png)

<center>利用hexo在github上快速搭建个人博客</center>
<!-- more -->
# 方案选型
## 主流的三种博客搭建方案：

```
1. Git+Github+Markdown+jekyll （免费）
2. Git+Github+Markdown+hexo （免费）
3. 虚拟主机＋插件＋Wordpress （付费）
```


### 我的选择： **Git+Github+Markdown+hexo**

#### 优点：
- 不需要自己购买服务器资源，也就不需要考虑备案，第三种方案则需要自己购买服务器资源，目前国内主流服务器资源大概是200元一年，小的服务商可能会便宜很多，但服务质量不敢恭维，具体价格自行百度
- 利用hexo生成的静态网页，相比于第三种方案显得更轻量级
- hexo 对比 jekyll搭建操作更简单、命令少、易于记忆，更容易快速上手
- 可以直接在github上编辑和发布博客

#### 缺点：
- 经常切换电脑编写博客时，会比较麻烦，所有电脑都需要重新配置环境
- 相比于拥有自建服务器的Wordpress，hexo的功能和可扩展性有限
- Github国内访问速度比较慢
- （最坑）不做处理的话，博客内容百度检索不到


---



# 搭建步骤

## 1. 环境的搭建，软件安装：

需要安装的软件有：
- node.js &emsp; hexo需要用到的语言环境
- git &emsp; 静态网页上传到服务器需要用到的版本控制工具
- hexo &emsp; 静态网页生成工具

### （1）node.js的下载与安装：
&emsp;[node.js官网下载地址](https://nodejs.org/en/)  

![image](http://ow0s809ce.bkt.clouddn.com/node.js%E4%B8%8B%E8%BD%BD.png)

安装时全部选默认配置就是了

node.js安装成功验证：    

#### 1. 打开控制台：

![cmd](http://ow0s809ce.bkt.clouddn.com/node_check.png)  

#### 2. 验证node.js是否安装成功:  
```
node -v
```


![cmd](http://ow0s809ce.bkt.clouddn.com/node_check2.png)  

#### 3. 验证npm是否安装成功: 
```
npm -v
```


![cmd](http://ow0s809ce.bkt.clouddn.com/npm_check.png)

### （2）git的下载与安装：

- 地址1：[官网下载地址](https://git-scm.com/download/win) &emsp;国内访问比较慢  

![image](http://ow0s809ce.bkt.clouddn.com/git.png)  

- 地址2：[百度云盘：](http://pan.baidu.com/s/1c2rQHcW) 密码：el5c  &emsp;版本号 : Git-2.8.1-64-bit ( 非最新 )
- 安装过程： 

全选

![image](http://ow0s809ce.bkt.clouddn.com/git1.png)  

选择图中第二项

![image](http://ow0s809ce.bkt.clouddn.com/git2.png)  

- 安装成功验证： 

1. 打开控制台：
  
![cmd](http://ow0s809ce.bkt.clouddn.com/node_check.png)  
2.验证git是否安装成功：

```
git --version
```

![cmd](http://ow0s809ce.bkt.clouddn.com/git_check.png )

### （3）hexo的安装
#### 1. 在任意位置打开Git Bash
![image](http://ow0s809ce.bkt.clouddn.com/git_use.png)
#### 2. 使用npm命令安装hexo   
输入命令：


```
$ npm install -g hexo
```


  
由于国内网络环境问题，使用上面的命令可能安装会遇到问题，这时我们使用淘宝NPM镜像,把命令换成以下，耐心等待安装：


```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```


![image](http://ow0s809ce.bkt.clouddn.com/hexo1.png)  

然后使用淘宝NPM安装Hexo，耐心等待  

```
$ cnpm install -g hexo-cli
```
![image](http://ow0s809ce.bkt.clouddn.com/hexo2.png)
#### 3. 出现的WARN可以不用理会,继续输入以下命令：

```
$ cnpm install hexo --save
```
#### 4. 安装完成后，在输入命令，验证是否安装正确：

```
$ hexo -v
```
![image](http://ow0s809ce.bkt.clouddn.com/hexo_check.png)

## 2. hexo本地生成博客：

### 1. 创建文件夹
创建放置hexo源文件的文件夹
（命名随意，只是作放置用途）  

![image](http://ow0s809ce.bkt.clouddn.com/hexo_init1.png)

### 2.运行Git Bash：  
  
 在该文件夹下右键运行Git Bash：  
 
![image](http://ow0s809ce.bkt.clouddn.com/hexo_init2.png)

### 3.hexo初始化

输入以下命令,耐心等待初始化完成：

```
$ hexo init
```

![image](http://ow0s809ce.bkt.clouddn.com/hexo_init3.png)

完成后打开该文件夹会看到  

![image](http://ow0s809ce.bkt.clouddn.com/hexo_init4.png)

### 4.使用编辑器（我使用的是editplus）打开配置文件 &emsp;**_config.yml**,可以配置个人博客的基本信息  


![image](http://ow0s809ce.bkt.clouddn.com/hexo_init5.png)

### 5.生成博客

输入以下命令，生成本地博客文件

```
$ hexo g
```

![image](http://ow0s809ce.bkt.clouddn.com/hexo_init6.png)

### 6.本地部署测试

输入以下命令，把生成的博客部署到本地，并测试访问


```
$ hexo s
```

![image](http://ow0s809ce.bkt.clouddn.com/hexo_init7.png)

使用上图标注的网址进行本地访问  http://localhost:4000/&emsp;（**注意：在git bash界面，不能用ctrl+C复制，只能右键copy**）结果应该如下图，看到博客页面（界面样式和下图肯定不一样，下图主题修改过，不要在意）：

![image](http://ow0s809ce.bkt.clouddn.com/hexo_init8.png)  


至此hexo本地部署就完成了。

## 3. github服务器部署
将hexo托管到github服务器上，实现远程访问：
### 1.注册github账号
(已经有了就忽略这一步)  

  详细注册流程就不多说了，差不多就是邮箱注册，再邮箱验证     
  
  [github官网地址](https://github.com/)&emsp; [github入门教程](http://jingyan.baidu.com/article/a17d5285f99dd48099c8f247.html)
  
### 2.新建仓库
在github上新建一个放置博客静态页面文件的仓库：  

![image](http://ow0s809ce.bkt.clouddn.com/github1.png)

命名规则如下图，红线圈住的位置为你的github用户名  

```
username.github.io
```

![image](http://ow0s809ce.bkt.clouddn.com/github2.png)

然后点击创建仓库

### 3.部署配置
在hexo本地的配置文件_config.yml中关联上刚才在github上新创建的仓库：

在_config.yml最底部找到deploy配置，进行如下图的配置，**配置完成记得保存**  


```
deploy:
  type: git
  repo: git@github.com:github账户名/github账户名.github.io.git
  branch: master
```


![image](http://ow0s809ce.bkt.clouddn.com/github3.png)

### 4.安装hexo发布插件
用于把本地生成的博客，通过上面配置的地址，发布到github上的仓库中  

还是在hexo源文件夹下打开git bash,输入以下命令：

```
$ npm instal lhexo-deployer-git  --save
```

![image](http://ow0s809ce.bkt.clouddn.com/github4.png)

### 5.配置SSH key  

在你的电脑上生成ssh秘钥并添加到github账号上（个人理解是绑定该电脑到github上，避免每次部署博客都要输入github的账号和密码）

还是在hexo源文件夹下打开git bash,输入以下命令：

```
$ ssh-keygen -t rsa -C "你的github注册邮件地址"
```

然后连续3次回车，最终会生成一个文件在用户目录下

![image](http://ow0s809ce.bkt.clouddn.com/github5.png)  

打开用户目录，找到.ssh\id_rsa.pub文件，记事本打开并复制里面的**全部内容**

![image](http://ow0s809ce.bkt.clouddn.com/github6.png)  
打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key：  

![image](http://ow0s809ce.bkt.clouddn.com/github7.png)  


![image](http://ow0s809ce.bkt.clouddn.com/github8.png)  

添加该ssh key  ：title随便取，key就填刚刚复制的那一段

![image](http://ow0s809ce.bkt.clouddn.com/github9.png)

  
  最后测试是否添加成功
  
  在gitbash中验证是否添加成功：
  

```
$ ssh -T git@github.com
```

看到以下信息就说明SSH已配置成功！
  
  ![image](http://ow0s809ce.bkt.clouddn.com/github10.png)
  
    
### 6.账号和邮箱设置
为git配置github的账号和邮箱：

```
$ git config --global user.name "liuxianan"// 你的github用户名，非昵称
$ git config --global user.email  "xxx@qq.com"// 填写你的github注册邮箱
```
 
 
###  7、博客上传

正式把博客上传到github上，并可以网络访问

依次执行以下命令：清理 - 生成 - 部署


```
$ hexo clean
```



```
$ hexo generate
```



```
$ hexo deploy
```


然后在浏览器中输入http://yourgithubname.github.io就可以看到你的个人博客了，是不是有点小激动

**大功告成！！！**

> 感觉gitbash中东西太多的时候输入clear命令清空。


---

# 其他
## 域名绑定
博客每次都要使用githubname.github.io这么一个长串的域名来访问显得太low了，这时我们可以考虑绑定我们自己的域名，这一点github是支持域名绑定的

### 1.购买域名：
>  **[参考网址](http://www.cnblogs.com/penglei-it/p/hexo_domain_name.html)**

域名供应商有很多，首推阿里的万网，大公司可靠，相对于服务器昂贵的价格，域名一年也就几十元钱，选个可靠的更好，可以省去不必要的麻烦。个人建议选择:&emsp;.com 结尾的域名（大众化，贵不了多少，具体的看个人需求），购买后大概6个小时就能生效
，尽快进行实名认证

[万网链接](https://wanwang.aliyun.com/)

### 2.设置域名解析：  

![image](http://ow0s809ce.bkt.clouddn.com/%E5%9F%9F%E5%90%8D1.png)    

点击添加解析，记录类型选A或CNAME，A记录的记录值就是ip地址，github(官方文档)提供了两个IP地址，192.30.252.153和192.30.252.154，这两个IP地址为github的服务器地址，两个都要填上，解析记录设置两个www和@，线路就默认就行了，CNAME记录值填你的github博客网址。如: username.github.io。  

![image](http://ow0s809ce.bkt.clouddn.com/%E5%9F%9F%E5%90%8D2.png)

![image](http://ow0s809ce.bkt.clouddn.com/%E5%9F%9F%E5%90%8D3.png)

这些全部设置完成后，此时你并不能要申请的域名访问你的博客。接着你需要做的是在hexo根目录的source文件夹里创建CNAME文件，<span style="color:red">不带任何后缀</span>，里面添加你的域名信息，如：name.com。实践证明如果此时你填写的是www.name.com那么以后你只能用www.name.com访问，而如果你填写的是name.com。那么用www.name.com和name.com访问都是可以的。重新清理hexo,并发布即可用新的域名访问。  
![image](http://ow0s809ce.bkt.clouddn.com/%E5%9F%9F%E5%90%8D4.png)  
### 3.出现404：
- 绑定了个人域名，但是域名解析错误。
- 域名解析正确但你的域名是通过国内注册商注册的，你的域名因没有实名制而无法访问。
- 你认为配置没有问题，那么可能只是你的浏览器在捣鬼，可尝试清除浏览器缓存再访问或者换个浏览器访问。
- 也有可能是你的路由器缓存导致的错觉，所以也可以尝试换个局域网访问你的网站。
- 最有可能的原因是你下载的hexo有问题，导致所有的东西都上传到了github,而导致index页面在主域名的下一级目录。你可以尝试查看上传的内容，找到index页面，在域名后面添加下一级目录。若能访问index页面（此时样式可能是乱的），则证明是hexo安装有问题，笔者当时遇到的就是这个问题。可卸载重新安装。
> 注：1，2默认你的CNAME文件配置没有问题，如果没有绑定个人域名，则不需要CNAME文件。

## 主题修改
### 如何更换主题
[参考教程](http://www.jianshu.com/p/469e985288b3?from=jiantop.com)  

主题下载：
例子：next主题

点到博客源文件右键打开git bash，把主题克隆到本地themes文件夹中
```
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
![image](http://ow0s809ce.bkt.clouddn.com/themes1.png)

![image](http://ow0s809ce.bkt.clouddn.com/themes2.png)

配置文件_config.yml中把默认主题landscape修改为next

![image](http://ow0s809ce.bkt.clouddn.com/themes3.png)

然后就可以输入以下命令本地部署看一看效果了


```
hexo s
```
呈现效果应该如下：  

![image](http://ow0s809ce.bkt.clouddn.com/themes4.png)


### next基本配置

next 是hexo中用户量比较大的一个主题，国内文档比较多，界面样式比较简洁

[参考教程](http://theme-next.iissnan.com/getting-started.html)  

进入next文件夹中打开主题配置文件_config.yml配置主题样式

#### 选择 Scheme

Scheme 是 NexT 提供的一种特性，借助于 Scheme，NexT 为你提供多种不同的外观。同时，几乎所有的配置都可以 在 Scheme 之间共用。目前 NexT 支持三种 Scheme，他们是：

- Muse - 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
- Mist - Muse 的紧凑版本，整洁有序的单栏外观
- Pisces - 双栏 Scheme，小家碧玉似的清新

Scheme 的切换通过更改 主题配置文件，搜索 scheme 关键字。 你会看到有三行 scheme 的配置，将你需用启用的 scheme 前面注释 # 去除即可。

#### 设置语言
站点配置文件， 将 language设置成你所需要的语言。建议明确设置你所需要的语言，例如选用简体中文：language: zh-Hans


语言 | 代码
---|---
简体中文 | zh-Hans
English	 | en
日本語 |ja
Korean	 | ko

#### 设置菜单


```
menu:
  home: 首页
  archives: 归档
  categories: 分类
  tags: 标签
  about: 关于
  search: 搜索
  commonweal: 公益404
  something: 有料
```



### 其他主题
[知乎推荐主题](http://note.youdao.com/)  

[官网推荐主题](https://hexo.io/themes/)

## 文章发布

hexo 支持的是markdown格式文件的文章，hexo文件夹里source文件夹里_post文件夹 就是用来存放博客文章的


![image](http://ow0s809ce.bkt.clouddn.com/post1.png)    

![image](http://ow0s809ce.bkt.clouddn.com/post2.png)   

![image](http://ow0s809ce.bkt.clouddn.com/post3.png)

  [极简MarkDown排版介绍](http://www.cnblogs.com/math/p/se-tools-001.html)

其中 .md 文件就是你的博客文件，相当于Word生成的.doc文件，为了方便你博客排版。你可以利用各种markdown编辑器生成.md文件，并进行博客编写，然后复制到_post文件夹下，再调用git bash命令进行部署发布，最后就可以在你的博客上看到了文章了
  