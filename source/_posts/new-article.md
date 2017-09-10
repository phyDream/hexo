
---
title: 搭建属于你自己的博客
date: 2017-09-07 11:47:55
tags: [blog,github,hexo]
---
![image](http://ow0s809ce.bkt.clouddn.com/github_hexo.png)
利用hexo在github上快速搭建个人博客  

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

> 1. 打开控制台：

![cmd](http://ow0s809ce.bkt.clouddn.com/node_check.png)  

> 2. 验证node.js是否安装成功:  
```
node -v
```


![cmd](http://ow0s809ce.bkt.clouddn.com/node_check2.png)  

> 3. 验证npm是否安装成功: 
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

> 1. 打开控制台：
  
![cmd](http://ow0s809ce.bkt.clouddn.com/node_check.png)  
> 2.验证git是否安装成功：

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

使用上图标注的网址进行本地访问  ++http://localhost:4000/（注意：在git bash界面，不能用ctrl+C复制，只能右键copy）结果应该如下图，看到博客页面（界面样式和下图肯定不一样，下图主题修改过，不要在意）：

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
## 主题修改
## 文章发布
## 界面修改


---


# 附录
## 图片的引用
## markdown的使用



