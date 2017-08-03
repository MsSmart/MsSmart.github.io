---
layout: post
title: Jekyll搭建Blog
date: 2017-08-03 11:11:11.000000000 +09:00
tags: 打怪练级
---

每次逛大神们的Blog，都特别崇拜，语言表述清楚，样式简约大方。后来发现一般喜欢折腾技术、喜欢分享的大神都是自己搭建Blog，折腾自己搭建东西顺手且显得高大上。于是乎，我在网上找了些搭建的教程，也开始折腾一番。有了自己的窝，督促自己养成写作和积累习惯。下面是我记录的搭建过程，分享给大家，也许你也会用得到。

​	**预达到效果**：通过域名访问自己的博客。

### 一、github创建仓库

#### 1. create仓库

在自己的github账户创建仓库

![1](http://mssmart.top/assets/blogimg/20170804/1.jpg)

![2](http://mssmart.top/assets/blogimg/20170804/2.jpg)

**注意**：仓库名字一定要用 [你的github账号名].github.io

#### 2. clone仓库

![2](http://mssmart.top/assets/blogimg/20170804/3.jpg)



复制git地址，打开terminal，cd你要存储远程仓库的文件夹，运行`git clone [远程仓库git地址]`
也可以用sourcetree，随你自己偏好。

#### 3.访问测试

我们先测试一把，二级域名能否正常访问。在仓库文件夹新建index.html， 内容如下：

```html
<!DOCTYPE html>
	<html>
		<body>
			<h1>Hello World</h1>
			<p>I'm hosted with GitHub Pages.</p>
		</body>
</html>
```



保存好上传到github刚刚新建好的仓库。

![2](http://mssmart.top/assets/blogimg/20170804/4.jpg)



在浏览器输入`[你的github账号名].github.io`，就可以看到index.html的内容。

### 二、Jekyll环境搭建

> [Jekyll中文文档](http://jekyllcn.com/)
>
> [Jekyll英文文档](https://jekyllrb.com/)
>
> [Jekyll主题列表](http://jekyllthemes.org/)

　　

GitHub Pages为了提供对HTML内容的支持，选择了Jekyll作为模板系统，Jekyll是一个强大的静态模板系统，作为个人博客使用，基本上可以满足要求，也能保持管理的方便。

Jekyll是一种简单的、适用于博客的、静态网站生成引擎。它使用一个模板目录作为网站布局的基础框架，支持Markdown、Textile等标记语言的解析，提供了模板、变量、插件等功能，最终生成一个完整的静态Web站点。说白了就是，只要安装Jekyll的规范和结构，不用写html，就可以生成网站。

#### 1. Jekyll基本结构
Jekyll的核心其实就是一个文本的转换引擎，用你最喜欢的标记语言写文档，可以是Markdown、Textile或者HTML等等，再通过layout将文档拼装起来，根据你设置的URL规则来展现，这些都是通过严格的配置文件来定义，最终的产出就是web页面。
```
|-- _config.yml
|-- _includes
|-- _layouts
|   |-- default.html
|    -- post.html
|-- _posts
|   |-- 2007-10-29-why-every-programmer-should-play-nethack.textile
|    -- 2009-04-26-barcamp-boston-4-roundup.textile
|-- _site
 -- index.html
```
将主题 [vno-jekyll](https://github.com/onevcat/vno-jekyll)下载到本地，解压到刚刚的代码仓库目录下，可以把文件夹里的文件都删了。

#### 2. 准备模板

下载模板 [vno-jekyll](https://github.com/onevcat/vno-jekyll)，解压到你的git仓库文件夹下（文件夹的内容可以在解压前都删除掉）。

![2](http://mssmart.top/assets/blogimg/20170804/5.jpg)

#### 3. 安装Jekyll

（1）先装ruby，如何安装ruby可以google或者baidu一下。

（2）参考[Jekyll](http://jekyllcn.com/)安装。

```sh
~ $ gem install jekyll bundler
~ $ cd [仓库的本地地址]
~/[仓库的本地地址] $ bundle install
~/[仓库的本地地址] $ bundle exec jekyll serve

```

解释：这里没有用这个命令， `jekyll new [新建blog名字]` ，是因为拷贝的主题模板已经包含了博客目录。

此时teminal提示：

```sh
Server address: http://127.0.0.1:4000/
Server running... press ctrl-c to stop
```

在浏览器访问http://mssmart.top

![6](http://mssmart.top/assets/blogimg/20170804/6.jpg)

（3）将文件都上传到远程github仓库。浏览器输入：`[你的github账号名].github.io`，可以看到自己的博客啦。

#### 4. 主题配置

（1）博客描述、个人介绍修改的文件在根目录下： `_config.yml`

（2）修改头像和背景：`仓库目录->assets->images`，直接替换掉头像、背景图片，不要改变文件名。

#### 5. 写博客

（1）文章路径

文章存储路径：仓库目录->_posts。文件名格式：`YYYY-MM-DD-文章标题.markdown，后缀.md也可以。

文章上传前可以在本地服务器上看效果。`~/[仓库的本地地址] $ bundle exec jekyll serve`，然后在浏览器输入：http://mssmart.top。

（2）书写工具

我使用的是Typora或者macDown，也可以根据自己的喜好选一款顺手的markdown工具。

（3）书写格式

在文章的开头，我们需要先设置头信息。头信息需要根据[YAML](http://yaml.org/)的格式写在两行三虚线之间。

```
---
layout: post
title: 这个是标题
date: 2017-08-03 11:11:11.000000000 +09:00
tags: 打怪练级
---
```

> `layout`：指文章布局的类型，需要使用指定的模版文件，模版文件放在`_layouts`目录下，暂时用`post.html`。`page.html`模板比`post.html`模板少了`更早的文章`和`评论模块`。有能力的也可以自己写一个文章页面的布局模板文件。
> `title`：文章的标题。
> `date`：发布文章的时间。（后面的一串零零零好像不能省）
> `tags`：标签，一篇文章可以设置多个标签，使用空格分割。

  基本上一篇文章只要用到以上一些信息就可以了，当然还有其它的变量可以设置，具体用法可以在[Jekyll网站](http://jekyllrb.com/docs/frontmatter/)上查看。

#### 6. 设置评论功能

1. 登录[Disqus](https://disqus.com/)网站注册一个账号（开vpn比较快点）
2. 点击Setting`图标`，选择`Add disqus to site`
3. 点击`Start Using Engage`
4. 设置自己的Disqus的URL
5. 设置根目录下`_config.yml`文件的disqus的属性

```objective-c
# Comment
comment:
    disqus: MsSmart
```

​

### 三、绑定个人域名

#### 1.创建CHAME文件

在本地仓库的根目录创建CHAME文件，将域名写入文件，`MsSmart.top`。push到远程仓库。

![8](http://mssmart.top/assets/blogimg/20170804/8.jpg)

![9](http://mssmart.top/assets/blogimg/20170804/9.jpg)



#### 2.买域名

在[万维](https://wanwang.aliyun.com/)购买域名，名字可以与github用户名不同。

#### 3.添加A记录

购买完，进入`管理控制台` -> `云解析` -> `解析` -> `添加解析` -> 添加`A`记录 :
`192.30.252.153`
`192.30.252.154`

![10](http://mssmart.top/assets/blogimg/20170804/10.jpg)

#### 4.等待DNS解析生效

> 大概十分钟内吧，奇葩情况可能要0-72小时都有可能。
> 可以在终端输入：`dig mssmart.top +nostats +nocomments +nocmd`，查看解析生效没。如果看到下面两条记录说明就解析好了。快输入你的域名看看效果吧。

```
stelladeMacBook-Pro:MsSmart.github.io stella$ dig mssmart.top +nostats +nocomments +nocmd

; <<>> DiG 9.8.3-P1 <<>> mssmart.top +nostats +nocomments +nocmd
;; global options: +cmd
;mssmart.top.			IN	A
mssmart.top.		530	IN	A	192.30.252.153
mssmart.top.		3530	IN	NS	dns1.hichina.com.
mssmart.top.		3530	IN	NS	dns2.hichina.com.
```

参考文献：

> http://louisly.com/2016/04/used-jekyll-to-create-my-github-blog/
>
> http://baixin.io/2016/10/jekyll_tutorials1/
>





