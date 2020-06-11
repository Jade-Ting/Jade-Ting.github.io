---
layout: post
title:  "搭建githubPage的一些记录"
date: 2020-01-02 19:56:16 +0800
tags: githubPage
color: rgb(241,148,131)
cover: '../assets/image/2020-01-02.jpg'
subtitle: '从零开始搭建（搬运）githubPage'
---
### 一、搭建github pages
> [参考](https://www.cnblogs.com/sqchen/p/10757927.html)

> [参考 - 个人网站的搭建 - 我的致命问题是这个解决的！](https://blog.csdn.net/qq_19799765/article/details/80869363)

#### 将项目设置为 github pages
##### 1. 选择需要设置为 github pages的项目，

**注意：项目名称必须为 `你的github用户名.github.io`！！！比如我的用户名是 Jade-Ting ，那这个仓库名就应该是 Jade-Ting.github.io ！！！否则网站会请求不到css跟js文件导致完全没有样式！**

![设置githubpages_1.png](https://i.loli.net/2020/01/08/PzSH2j6X4QNIbeo.png)

##### 2. 进入settings后找到 GitHub Pages将source选择为 master branch，就会出现page的地址。点击进入就是该项目的地址啦~

![设置githubpages_2.png](https://i.loli.net/2020/01/08/TMPwRJif5s2GDmX.png)

#### 在空项目中加入 jekyll 模板，实现个人博客
> 又想偷懒又想美化项目！就只能找模板了！
> Github Pages基于Jekyll构建，Jekyll可以帮助我们把纯文本转换为静态博客网站

##### 1. 下载主题：可以在 [Jekyll Themes](http://jekyllthemes.org/) 中选择自己喜欢的主题。进入home(github)下载主题。
##### 2. 将下载的主题解压到项目文件夹中。（原项目主要保留 .git 文件）
##### 3. 熟悉 Jekyll 的目录结构
```
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```
##### 4. 添加博客内容，更新后push到github上即可。


    进入 _posts目录，所有的文章都必须放在_posts文件夹下
    创建markdown文档，如根据时间和内容命名 yyyy-MM-dd-filename.md
    
##### 5. 修改主题
    


    1. 可以在 _config.yml 文件中将网站信息改成自己的
    2. 可以在 _includes 文件中修改html文件，修改网站样式


##### 6. 可以将个人博客的项目在github上设置为私有：进入 setting，设置Danger Zone， 点击 Make Private
![image](https://img-blog.csdnimg.cn/20190423172927155.jpg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzI2OTA3MjUx,size_16,color_FFFFFF,t_70)


##### 7. 注意：要安装ruby环境，运行 jekyll 主题才会出现！具体安装操作见下文 【安装ruby和jekyll】

### 二、安装ruby和jekyll
> [参考 - windows10安装jekyll和ruby环境](https://mojotv.cn/2019/07/13/install-jekyll-in-windows10) - 下文多处摘自该文章。

#### 安装Ruby
##### 1. 下载ruby, 到 [RubyInstaller](https://rubyinstaller.org/downloads/) 中下载 Ruby+Devkit X.X.X版本 （版本可自行选择，注意区分 32/64 位）。
##### 2. 安装ruby, 点击下载好的 rubyInstaller 直接安装。 注意：勾选添加到PATH选项

![安装界面](https://mojotv.cn/assets/image/ruby_01.png)

##### 3. 安装完成后会出现 RubyInstaller 界面。选择 3 (安装MSYS2 and MINGW development toolchain)
![安装完成](https://mojotv.cn/assets/image/ruby_02.png)


#### 下载gem 安装jekyll
##### 1. 下载 RubyGems, 到[Download RubyGems](https://rubygems.org/pages/download)下载 zip 版。
##### 2. 安装gem，在解压文件夹中最外层安装 jekyll
```bash
// 在解压文件夹中最外层打开cmd

gem install jekyll
gem install jekyll-paginate
jekyll -v                   // 检查版本
```
##### 3. 安装bundle
```bash
gem install bundler

// 如果安装完成后使用 bundle 报错，有可能是版本问题，根据提示重新安装制定版本

gem install bundler:1.16.2
```

#### 在项目文件夹中执行
> 打开项目所在文件夹的cmd

##### 1. 安装依赖
```bash
bundle install
```

##### 2. 启动jekyll服务
```bash
bundle exec jekyll serve
```
![jekyll启动成功.png](https://i.loli.net/2020/01/08/iWebtXz92xMHwpI.png)


### 添加评论
> [在jekyll中使用disqus](https://blog.zxbing0066.com/jekyll/2014/11/12/disqus.html)

### 遇到的问题
##### 1. 在执行 `bundle exec jekyll serve` 时，提示以下错误。
```bash
// 节选部分
Could not find gem 'ruby (< 2.6)', which is required by gem 'ffi (>= 0.5.0, < 2)', in any of the relevant sources: the local ruby installation
```
原因：bundle不兼容当前ruby版本。
解决：所以重新安装小于2.6的版本。


##### 2. 在部署到github之后，页面获取不到css/js等文件，导致页面没有样式等问题。

原因：在设置本项目的仓库名时要设置为 `username.github.io`，也就是 `你的github用户名.github.io`！！！

![报错1.png](https://i.loli.net/2020/01/09/U4lhzXOmdeNRWuQ.png)

![报错.png](https://i.loli.net/2020/01/09/RkdLnsiKTQHr84p.png)


##### 3. 导航条上的 favicon 图片没有显示出来，正确的应该如下所示。

![favicon.png](https://i.loli.net/2020/01/09/aIoF6V4hsnrNz2S.png)

原因：本项目中该图标命名为 `profile.jpeg`

解决：将图标改命名为 `favicon.png`, 如果还是不显示则加上 `type="image/png"`

```html
<!-- Favicon -->
<link href="/assets/favicon.png" rel="shortcut icon" type="image/png"/>
<link href="/assets/favicon.png" rel="apple-touch-icon-precomposed"  type="image/png"/>
```
补充：网络上的各种做法（还未一一验证）
```html
// 1.
<link rel="shortcut icon" type="image/png" href="/favicon.png">

// 2.
<link rel="shortcut icon" type="image/x-icon" href="/favicon.ico?">

// 3.
<link rel="shortcut icon" type="image/png" href="{{ "/favicon.png" | prepend: site.baseurl }}" >

// 4. 使用的是.ico
<link rel="shortcut icon" type="image/x-icon" href="{{ "/favicon.ico" | prepend: site.baseurl }}" >

// 5.
<link rel="shortcut icon" type="image/x-icon" href="{{ site.baseurl}}/images/favicon.ico" >

// 6.
<link rel="shortcut icon" type="image/png" href="{{ '/favicon.png' | relative_url }}" >

// 7.
<link rel="shortcut icon" type="image/png" href="{{site.url}}/favicon.png">
```