---
title: Hexo博客的安装部署及多电脑同步
date: 2018-11-24 15:56:12
tags: hexo,blog,next
---

Hexo安装教程很多，我这里尽可能的讲的细一些，把容易踩坑的地方以及后期多电脑同步所遇到的问题列出来，以便给自己及大家参考。本文主要讲解安装部署后源文件同步问题，当然，你可以采用网盘方式进行同步，但是这种方式不够程序员，也不能进行版本控制，如果你是一个多系统（windows、mac、linux）爱好者，那我建议你还是和我一样，采用git的方式进行源文件管理。使用github和Hexo，在几秒内，即可利用靓丽的主题生成静态网页。

# 安装
<!--more-->
## 什么是hexo

首先，你能找到这篇文章，证明你已经知道什么是[hexo](https://hexo.io/)了，官方对这块讲解非常详细，我不做过多赘述，但是关于优缺点这块，还是有几个点要给大家说下。

> 优点： 基于node.js的高效博客框架，能让上百个页面在几秒内完成渲染 支持markdown撰写博客，极其轻量级，这很程序员 海量的主题，插件支持 很装逼，怪不得得到不少程序员的青睐 支持github pages，不用自己建服务器 可离线撰写文档，有网后上传 缺点： 麻烦，博客的源文件需要保存起来，不好同步（本文后面将解决这个问题） 学习成本高，没接触过markdown的同学很难上手 同上，没接触过开发的同学很难上手 写博客需要搭建环境，换电脑后浪费时间

优缺点我遇到的就这些，当然，因为是纯前端展示，所以加载速度比[Wordpress](https://cn.wordpress.org/)和[Typecho](http://typecho.org/)等博客速度快的多。而且完美支持markdown语言。但是缺点也很明显，不能在线编辑，需要您本地撰写后部署才行。就如同您写C语言后，还需要编译一样，Hexo将Markdown文件编译成Html文件在部署到服务器端（可以是自己的服务器，也可以是Github page的服务器）。

## 如何安装hexo

> 网上安装hexo的教程很多很多，官方也提供了hexo的安装[中文教程](https://hexo.io/zh-cn/docs/)，如我教程时间过长，请参考官方教程。

安装之前，需要你电脑安装好Node.js和[Git](https://git-scm.com/)，由于系统花样繁多，本文将仅介绍Windows、Mac、Ubuntu(linux)安装方法，其他系统请自行摸索或私信我[微博](https://weibo.com/zc754886197)。

### Node.js及git的安装

#### windows中Node.js及Git的安装

##### Node.js

打开[Node.js](https://nodejs.org/en/)的官网，点击8.9.4 LTS绿色按钮（本文撰写时的版本），下载好后一路下一步安装即可。

##### Git

打开[Git](https://git-scm.com/)官网，点击电脑显示器中的Download 2.16.2 for Windows（本文撰写时的版本）按钮，下载好后一路下一步安装即可。

#### Mac中Node.js及Git的安装

##### Node.js

打开[Node.js](https://nodejs.org/en/)的官网，点击8.9.4 LTS绿色按钮（本文撰写时的版本），下载好后一路下一步安装即可。

##### Git

Mac默认自带Git，若您系统版本过低，请打开[Git](https://git-scm.com/)官网下载安装。

#### Ubuntu中Node.js及Git的安装

##### Node.js

命令窗口输入以下命令

```js
sudo apt-get update
sudo apt-get install -y python-software-properties software-properties-common
sudo add-apt-repository ppa:chris-lea/node.js
sudo apt-get update
sudo apt-get install nodejs
sudo apt install nodejs-legacy
sudo apt install npm
sudo npm install n -g
sudo n stable
sudo node -v
```

如遇到安装错误或其他问题，请使用编译安装。

> 为保证nodejs版本及稳定性，下面安装是下载nodejs进行编译安装，可能耗时较长，请耐心等待。如您上面执行`sudo node -v`已经正常显示版本，则不用执行下面的代码。

```js
sudo git clone https://github.com/nodejs/node.git
sudo chmod -R 755 node
cd node
sudo ./configure
sudo make
sudo make install
```

##### Git

Ubuntu安装git，执行以下命令即可安装

```js
sudo apt-get install git
```

### Hexo的安装

hexo安装命令非常简单，只需要一步即可安装完成，具体命令窗口输入以下命令：

```js
sudo npm install -g hexo-cli
```

> 但是值得注意的是，**Windows**必须去掉`sudo`命令即`npm install -g hexo-cli`，windows如何打开命令窗口请点击[这里](https://jingyan.baidu.com/article/f3e34a12c284e8f5eb653517.html)学习。Ubuntu和Mac仍使用上述命令安装即可。

# 部署

关于部署，官方文档也写的非常详细，如有任何疑问详见[这里](https://hexo.io/zh-cn/docs/setup.html)，本文仅作最基础的部署介绍。

## 如何建站

安装完Hexo等相关依赖后，请执行以下命令创建您的网站

```js
sudo hexo init <folder>
cd <folder>
sudo npm install
```

> 同上，**Windows**须去掉`sudo`命令，Ubuntu和Mac仍使用上述命令安装即可。其中`<folder>`为你需要创建的网站的文件夹名称，名称无硬性要求，如我创建自己的网站，则可写为`sudo hexo init techeek`

没错，这样就完了，你的网站已经搭建完成。更多相关的命令解释请点击[这里](https://hexo.io/zh-cn/docs/commands.html)查看。

## 如何写文章

首先我们需要创建一个新的文章，默认Hexo已经为我们写了一篇为Hello Word的文章，但是为了熟悉撰写文章的过程，我们还是重头撰写一遍。

首先在您的命令窗口输入以下命令

```js
sudo hexo new <title>
```

> 同上，**Windows**须去掉`sudo`命令，Ubuntu和Mac仍使用上述命令安装即可。其中`<title>`为你需要创建的文章的名称，名称无硬性要求，如我创建自己的文章，则可写为`sudo hexo init hexo-tutorial`

这时，找到你创建的网站目录中创建markdown源文件的地方，位置在`你创建网站的名称\source\_posts`下，双击编辑该文件，打开后markdown格式如下：

```js
---
title: 这块写你文章的名称
date: 这块为创建文章的时间，可修改，格式为：年-月-日 时:分:秒
tags: [这块写你文章的标签，使用“,”隔开（注意去掉引号须包含中括号）]
---

这块写你的正文
```

如本文格式

```js
---
title: Hexo博客的安装部署及多电脑同步
date: 2018-02-26 13:47:02
tags: [hexo,git,同步]
---
Hexo安装教程很多，我这里尽可能的讲的细一些，把容易踩坑的地方以及后期多电脑同步所遇到的问题列出来，以便给自己及大……
```

## 如何部署

本次部署我们分为两类，第一种是部署到自己的服务器，第二种是部署到Github Pages上面，个人是推荐部署到Github Pages上面。不管是部署在自己的服务器还是部署在Github Pages上，都需要先生成网页文件才行，这块输入如下命令：

```js
sudo hexo generate
```

来生成静态网页文件，同上，Windows不需要输入`sudo`命令，这条命令可以简写为`sudo hexo g`后面也可加`-d或-w`选项，其中`-d`选项为文件生成后立即部署网站，`-w`选项为监视文件变动。

### 如何部署在自己的服务器上

当静态文件生成好之后我们需要使用如下命令部署网站，命令如下

```js
sudo hexo deploy
sudo hexo server
```

启动服务器。默认情况下，访问网址为： http://localhost:4000/

### 如何部署在Github Pages上

#### 创建Github仓库

首先你需要创建并登录Github账户，点击[这里](https://github.com/)注册，然后点击GitHub中的New repository创建新仓库。仓库名称必须命名为`你的GitHub用户名.github.io`，其中“你的GitHub用户名”使用你的github账户代替，比如我的仓库名称为`techeek.github.io`，这样，你就创建好你的Github Pages仓库了。

#### 生成ssh密钥文件

接下需要创建ssh密钥文件，为什么要创建呢，因为Hexo部署在github上是通过密钥配对上传的，所以我们需要创建公钥和私钥，什么是公钥和私钥请点[这里](https://www.alibabacloud.com/help/zh/faq-detail/42216.htm)。我们首先依然打开命令提示符，Windows请搜索打开Git Bash。然后输入如下命令配置git

```js
git config --global user.name "你的GitHub用户名"
git config --global user.email "你的GitHub注册邮箱"
```

配置完成后，输入如下命令生成ssh密钥文件

```js
ssh-keygen -t rsa -C "你的GitHub注册邮箱"
```

接下来按三下回车就行，不创建密码，然后我们使用

```js
cd ~/.ssh
```

命令打开ssh生成的密钥文件，Windows密钥文件在`C:/Users/你的用户名/.ssh`目录下。接下来打开[GitHub_Settings_keys](https://github.com/settings/keys) 页面，新建new SSH Key。Title为标题，任意填写。将刚刚复制的id_rsa.pub内容粘贴到key，最后点击Add SSH key。

#### 部署网站

部署前需要修改Hexo的配置文件，这里先放出[官方](https://hexo.io/zh-cn/docs/configuration.html)的配置方法，大家可以参考。我这里只讲如何配置git

修改_config.yml内容如下

```js
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy: 
  type: git
  repo: git@github.com:你的GitHub用户名/你的GitHub用户名.github.io.git
  branch: master
```

很多教程都将`repo:`写为`https://github.com/你的GitHub用户名/你的GitHub用户名.github.io.git`但是我个人不推荐这样写，因为有时候会因为蜜汁原因无法上传，别问问啥，我还没搞懂。所以我建议按照我上面的格式写。

这是执行如下命令，就可部署你的网站了

```js
sudo hexo deploy
```

部署完成后，打开https://你的GitHub用户名.github.io.git看看是不是能正常访问啦？

## 后话

以后，你写完博客后，只需要执行以下命令即可部署在你自己的服务器上或者Github Pages上面。

```js
sudo hexo generate
sudo hexo deploy
sudo hexo server #Github Pages不需要这行命令
```

可精简为

```js
sudo hexo g -d
sudo hexo server #Github Pages不需要这行命令
```

也就是说，如果你是使用Github Pages服务，则只用输入`sudo hexo g -d`命令即可部署你的服务器。

同时，你也可以将自己的域名指向你的Github Pages服务器，但是须在`source\`目录下创建CNAME文件，文件内容为你的域名地址，如我的内容则为`www.techeek.cn`，但是比较坑的是，使用自己的域名无法支持HTTPS，我这里采用的是腾讯云的CDN服务，在腾讯云申请免费的CA级证书，部署上去直接就支持了HTTPS，还加速了网站，一举两得。

# 同步

部署完成后，接下来该解决同步问题了，当然你可以上传到你自己的网盘中，比如微云，百度网盘等地方，但是这样不够程序员，也不能版本控制，那怎么办呢？我们需要Git！我这里方案很简单，网站文件走主分支，而源文件则新建分支，更换电脑后我只需要拉取新建的分支即可在新电脑上部署网站。在这里我们先假设两台电脑，A电脑（公司电脑：Windows）B电脑（家里的电脑系统：Mac），为了方便讲解，以及提现Hexo的可扩展移植性，我们分两个系统讲解。

## 如何上传博客工程到Github

首先在公司的A电脑搭建并部署完系统后，我们需要将项目上传到你的github上。在A电脑上执行如下命令

```js
git init #git初始化
git remote add origin https://github.com/用户名/你的GitHub用户名.github.io.git #添加仓库地址
git checkout -b 分支名 #新建分支并切换到新建的分支
git add . #添加所有本地文件到git
git commit -m "这里填写你本次提交的备注，内容随意" #git提交
git push origin 分支名 #文件推送到hexo分支
```

这里执行命令须在你创建的项目下执行，就是上文提到的`<folder>`目录。其中分支名需要你自己创建，名称随意，我这里以`hexo`为例。则我要上传自己的项目命令如下

```js
git init 
git remote add origin https://github.com/techeek/techeek.github.io.git 
git checkout -b hexo
git add . 
git commit -m "fix bug"
git push origin hexo
```

之后git会询问你的用户名和昵称，填写正确即可将博客工程文件上传到github的hexo分支下。

## 如何从另一台电脑下载博客工程

那B电脑我改如何下载项目文件呢？很简单，首先在B电脑上部署好Git和Node.js环境。然后输入以下命令

```js
git clone -b 分支名 https://github.com/用户名/你的GitHub用户
```

克隆下载完成后，进入到你项目的文件夹，重新配置你的hexo环境，命令如下

```js
sudo npm install -g hexo-cli #安装hexo,注意这里不需要hexo初始化,否则之前的hexo配置参数会重置
sudo npm install #安装依赖库
sudo npm install hexo-deployer-git #安装git部署相关配置
```

之后就如上文所示，创建撰写新的文章，并使用`sudo hexo g -d`命令创建并部署您的网站。值得注意的是，你的私钥文件需要携带，但极其不建议私钥文件放在Github，建议放在U盘或网盘中，使用时下载即可。然后拷贝到相关目录下（Windows目录在`C:/Users/你的用户名/.ssh`目录、Mac在`~/.ssh/`目录，Ubuntu也在`~/.ssh/`目录下）即可正常部署您的网站。使用密钥时需注意权限，使用`chmod 密钥名称 700`命令即可更改权限，不更改权限无法使用密钥。

## 撰写完后如何再次同步

写完后如何再次同步呢？

```js
git add .
git commit -m "这里填写你本次提交的备注，内容随意"
git push origin 分支名
```

没错，这个样就够了~你B电脑上的数据也已经同步到Github上面了。那第二天到A电脑跟前，只需要执行以下命令就行

```js
git pull
```

这样，你的数据就全部同步到A电脑了，以后在部署完后，再次执行

```js
git add .
git commit -m "这里填写你本次提交的备注，内容随意"
git push origin 分支名
```

到你的Github上就行。

## 总结

总的来说，这样可以来回控制你的版本，只要善用Git，你可以在任意电脑撰写你的博客。控制你的项目。

所以，部署完项目后A电脑和B电脑部署区别如下

A:

```js
git add .
git commit -m "这里填写你本次提交的备注，内容随意"
git push origin 分支名
```

B:

```js
git pull
hexo new 文章名
hexo g -d
git add .
git commit -m "这里填写你本次提交的备注，内容随意"
git push origin 分支名
```

A:

```js
git pull
hexo new 文章名
hexo g -d
git add .
git commit -m "这里填写你本次提交的备注，内容随意"
git push origin 分支名
```

循环执行即可，当然你也可以加入C电脑D电脑，数量不限。

好了，文章暂时就先结束了，不足之处请见谅。转载请注明原文出处，谢谢！

转载自[hexo安装及多台电脑同步](https://cloud.tencent.com/developer/article/1046404)

