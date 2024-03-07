---
ifupdate: false
layout: post
title: 使用 GitHub Pages + Jekyll 搭建个人博客
subtitle: 手把手教你撸个人博客
date: 2024-01-12
author: wenbsu
header-img: https://foruda.gitee.com/images/1705471447391412998/4fddf9a6_1002526.jpeg
catalog: true
tags:
 - 博客模板
---

[我的博客在这里 →]({{ site.baseurl }}/)
## 前言
现在市面上的博客很多，比如如CSDN，博客园，简书等平台，可以直接在上面发表，用户交互做的好，写的文章百度也能搜索的到。缺点是比较不自由，会受到平台的各种限制要求和烦人的广告。
而自己购买域名和服务器，搭建博客的成本实在是太高了，作为一个上班族不光是这些购买成本，单单是花力气去自己搭这么一个网站，还要定期的维护它，对于我们大多数人来说，实在是没有这样的精力和时间。
那么本文章就可以解决你目前的烦恼，本文章针对于不懂技术、还不想花钱，还能简单快速的搭建属于自己的博客网站。

## 准备工作

1. 创建 GitHub 账户 
- 访问 [https://github.com](https://github.com) 并创建一个 GitHub 账户。
2. 本地安装 Git 
- 根据操作系统下载并安装 Git：[https://git-scm.com/download](https://git-scm.com/downloads)
3. 本地安装 Jekyll
- 安装 Ruby和Devkit [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/) 
- RubyGems 镜像源切换：`gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/`
- 安装 Jekyll  cmd命令：`gem install jekyll bundler`

 
## 快速搭建

1. 创建新的 Repository
- 登录 GitHub，点击页面右上角的 "New" 按钮，创建一个新的 Repository，名称为你的 [用户名.github.io](https://wenbsu.github.io/) （注意：这里的用户名指的是你的 GitHub 用户名，wenbsu（账号名）/wenbsu.giithub.io（仓库名））；最终在浏览器中访问的地址就是你填写在Repository name 中的地址。
  ![/blog/20240112/0-1.jpeg](https://foruda.gitee.com/images/1705471497555951955/5c6081c4_1002526.jpeg)
2. 获取我的仓库文件
-  搜索栏搜索  **wenbsu.github.io** 进入[我的仓库](https://github.com/wenbsu/ )，点击右上角的 **Fork** 将我的仓库拉到你仓库下。
  ![/blog/20240112/0-2.jpeg](https://foruda.gitee.com/images/1705471594642086545/6ea8c4cc_1002526.jpeg)
3. 运行查看
- 点击仓库 setting  再点击 Pages 当出现如下画面，可以点击 Visit site 查看或者直接浏览器输入`你的Github账号名.github.io`
  ![/blog/20240112/0-3.jpeg](https://foruda.gitee.com/images/1705471629016250899/9aa1f1d7_1002526.jpeg)
- 如果网页打开如下恭喜你完成了一半了！如果没用不是该页面请重新检查操作问题。
  ![/blog/20240112/0-4.jpeg](https://foruda.gitee.com/images/1705471661226703002/01ebe004_1002526.jpeg)

Ps：

- 如果没有出现Visit site 可能是你仓库名设置错误或者仓库没有公开导致
- 网页打开但是显示内容不一致，可能是你设置展示分支错误，可以修改Pages 中的 Branch 设置为 项目所在分支的（root）根目录。

## 本地修改
### 结构了解
网站GitHub Pages + Jekyll实现的静态网页，Jekyll 网站基础结构如下
```
.
├── _config.yml
├── _data
|   └── members.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
├── .jekyll-metadata
└── index.html # 也可以是带 front matter 的 'index.md' 文件
```

看起来很复杂但是不做二次开发的吧，只需要了解以下模块就行了。

- _config.yml 全局配置文件
- _posts 放置博客文章的文件夹
- img 存放图片的文件夹

二次开发可以参考 [《Jekyll中文文档》](https://www.jekyll.com.cn/docs/structure/)

#### _config-基础配置
```yaml
# Site settings
title: Wenbsu Blog  #home 页面 博客标题
SEOTitle: 文水水的博客 | Wenbsu Blog #浏览器显示标签&名称
header-img: img/head-photo/home-bg-o.jpg # home 页面 名称
email: wenbsu@gmail.com  #邮箱
description: "The future belongs to those who believe in the beauty of their dreams."
keyword: "wenbsu, Wenbsu Blog, 文水水的博客, github, gitee, Wenbsu"
url: "http://wenbsu.github.io"          # your host, for absolute URL
baseurl: ""      # for example, '/blog' if your blog hosted on 'host/blog'
github_repo: "https://github.com/wenbsu/" # you code repository
```

#### _config-社交平台账号
```yaml
# SNS settings
RSS: false
# weibo_username: wenbsu
# zhihu_username: wenbsu
github_username: wenbsu
# twitter_username: wenbsu
#facebook_username:  wenbsu
#linkedin_username:  wenbsu
```

如果需要添加或者修改可以到_includes/sns_links.html 进行添加修改
不需要显示的话直接注释掉。效果图如下
![/blog/20240112/0-5.jpeg](https://foruda.gitee.com/images/1705471740665256112/1b5f99a8_1002526.jpeg)

#### _config-侧边栏
```yaml
  # Sidebar settings
  sidebar: true # whether or not using Sidebar.
  sidebar-about-description: "The Pursuit of Happiness <br> Email:wenbsu@gmail.com  <br> Wechat:wenbxu"
  sidebar-avatar: /img/wenbsu.png # use absolute URL, seeing it's used in both `/` and `/about/`
```
![/blog/20240112/0-6.jpeg](https://foruda.gitee.com/images/1705471795159828635/fb85c8e8_1002526.jpeg)


#### _config-好友
```yaml
friends:
  [
    { title: "github", href: "https://github.com/wenbsu" },
    { title: "gitee", href: "https://gitee.com/wenbsu" },
    { title: "csdn", href: "https://blog.csdn.net/wenbsu" },
    { title: "blog", href: "http://wenbsu.github.io" }
  ]
```
![/blog/20240112/0-7.jpeg](https://foruda.gitee.com/images/1705471827594316592/0d4f74b1_1002526.jpeg)

#### img-图片配置

1. 应用场景：
   - 文章的 head 图片展示
   - 页面的 head 图片展示
   - md文件调用的 图片展示
2. 使用方法：
   - 调用图片一般相对路径方式获取例如 img/文件夹名（可以零个至多个）/图片名称

#### _posts-md文件设置（划重点！！！）
效果展示：
![/blog/20240112/0-8.jpeg](https://foruda.gitee.com/images/1705471861298923656/669917fb_1002526.jpeg)

_post可以说的上是整个博客最重要的部分了，应为文章都统一存放在这个页面。需要注意点如下：

1. 文章抬头设置
```
---
ifupdate: false
layout: post
title: 使用 GitHub Pages + Jekyll 搭建个人博客 #文章标题
subtitle: 模板  #文章副标题
date: 2024-01-12 #文章日期
author: wenbsu #作者
header-img: img/head-photo/post-bg-rwd.jpg #文章 head 图片
catalog: true
tags: #  网页 tags 标签
 - 博客模板
---
```

2. 文件名称和路径设置
   - 文件名称需要设置为` yyyy-MM-dd-文件名格式`。格式不正确jekyll将不会解析该md文件
   - 路径可以设置在根目录下或者子目录下都行，建议设置为 大类/小类/文件名 ，例如 Python/Python高级操作/2024-01-12-Python日志操作

Ps：
因为在jekyll 中，Markdown文件可以包含HTML代码。Jekyll会自动将Markdown文件转换为HTML页面，并保留其中的HTML标签。如果你在Markdown文件中使用了Liquid模板语法，可以会导致网页找不到对应的数据，需要使用{% raw %}和{% endraw %}标记来避免Liquid解析其中的内容。例如：
```
{% raw %}
这是一段包含Liquid模板语法的代码：{{ variable }}
{% endraw %}
```

### 本地运行

1. 克隆 Repository
   - 在命令行中执行以下命令，克隆刚刚创建的 Repository 到本地：
```
git clone https://github.com/你的用户名/你的用户名.github.io.git
```

2. 本地安装 Jekyll
-  安装 Ruby和Devkit [Downloads](https://rubyinstaller.org/downloads/)
-  RubyGems 镜像源切换：`gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/`
-  Jekyll cmd命令：`gem install jekyll bundler`

3. 运行项目
- 在安装好jekyll的前提下，cmd命令切换到仓库文件目录下，执行以下命令来启动 Jekyll 服务器：
```
bundle install
bundle exec jekyll serve  
gem update jekyll # 更新jekyll
gem update github-pages #更新依赖的包
```
- 在浏览器中访问 [http://localhost:4000](http://localhost:4000/) 就可以看到你的 Jekyll 网站了，你对本地博客的修改都会在这个地址进行显示，修改配置后网址要`强制刷新`才会展示。如果想修改IP访问，启动命令指定本机IP：bundle exec jekyll serve -w --host=[本机IP]


## 更多

1. Jekyll文档 [点击这](https://www.jekyll.com.cn/docs/)。
2. 更多博客模板 [点击这](http://jekyllthemes.org/)。
3. Github Pages文档 [点击这](https://docs.github.com/zh/pages)。
4. 博客模板是 [Hux](https://github.com/Huxpro/huxpro.github.io) fork 的, 非常感谢这个作者。
