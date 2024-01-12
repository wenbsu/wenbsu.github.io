---
ifupdate: false
layout: post
title: 使用 GitHub Pages + Jekyll 快速搭建个人博客网站
subtitle: 模板
date: 2023-07-15
author: Carlos
header-img: img/head-photo/post-sample-image.jpg
catalog: true
tags:
 - 博客模板
---

[我的博客在这里 →](https://carlosw0713.github.io/)
## 前言
现在市面上的博客很多，比如如CSDN，博客园，简书等平台，可以直接在上面发表，用户交互做的好，写的文章百度也能搜索的到。缺点是比较不自由，会受到平台的各种限制要求和烦人的广告。
而自己购买域名和服务器，搭建博客的成本实在是太高了，对于一个学生党不光是这些购买成本，单单是花力气去自己搭这么一个网站，还要定期的维护它，对于我们大多数人来说，实在是没有这样的精力和时间。
那么本文章就可以解决你目前的烦恼，本文章针对于不懂技术、还不想花钱，还能简单快速的搭建属于自己的博客网站。

## 准备工作

1. 创建 GitHub 账户 
- 访问 [https://github.com](https://github.com) 并创建一个 GitHub 账户。
2. 本地安装 Git 
- 根据操作系统下载并安装 Git：[https://git-scm.com/download](https://git-scm.com/downloads)
3. 本地安装 Jekyll
- 安装 Ruby和Devkit [https://rubyinstaller.org/downloads/](https://rubyinstaller.org/downloads/) 
- 安装 Jekyll  cmd命令：`gem install jekyll bundler`

 
## 快速搭建

1. 创建新的 Repository
- 登录 GitHub，点击页面右上角的 "New" 按钮，创建一个新的 Repository，名称为 [你的用户名.github.io](http://xn--6qqv7i14ofosyrb.github.io/) （注意：这里的用户名指的是你的 GitHub 用户名，carlow0713（账号名）/carlosw0713.giithub.io（仓库名））。
2. 获取我的仓库文件
-  搜索栏搜索  **carlosw0713.github.io** 进入[我的仓库](https://github.com/carlosw0713/carlosw0713.github.io )，点击右上角的 **Fork** 将我的仓库拉到你仓库下。
3. 运行查看
- 点击仓库 setting  再点击 Pages 当出现如下画面，可以点击 Visit site 查看或者直接浏览器输入`你的Github账号名.github.io`
- ![](https://raw.githubusercontent.com/carlosw0713/carlosw0713.github.io/master/img/Art_img/blog/github_setting.png#id=J4LA8&originHeight=441&originWidth=1021&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)
- 如果网页打开如下恭喜你完成了一半了！如果没用不是该页面请重新检查操作问题。
- ![](https://raw.githubusercontent.com/carlosw0713/carlosw0713.github.io/master/img/Art_img/blog/home_me.png#id=fNnaH&originHeight=317&originWidth=674&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

Ps：

- 如果没有出现Visit site 可能是你仓库名设置错误或者仓库没有公开导致
- 网页打开但是显示内容不一致，可能是你设置展示分支错误，可以修改Pages 中的 Branch 设置为 项目所在分支的（root）根目录。

## 本地修改
### 结构了解
网站GitHub Pages + Jekyll实现的静态网页，Jekyll 网站基础结构如下
```
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
├── _data
|   └── members.yml
├── _site
├── img
└── index.html
```

看起来很复杂但是不做二次开发的吧，只需要了解以下模块就行了。

- _config.yml 全局配置文件
- _posts 放置博客文章的文件夹
- img 存放图片的文件夹

二次开发可以参考 [《Jekyll中文文档》](https://www.jekyll.com.cn/docs/structure/)

#### _config-基础配置
```yaml
# Site settings
title: Carlos Blog  #home 页面 博客标题
SEOTitle: Carlos的博客 | Carlos Blog #浏览器显示标签&名称
header-img: img/home-bg.jpg # home 页面 名称
email: carlos.w.0713@oulook.com  #邮箱
description: "Every failure is leading towards success."
keyword: "carlos, carlos Blog, carlos的博客, carlos, github, gitee, csdn, 测试" #自定义关键词
url: "http://carlosw0713.github.io"          # 博客地址
baseurl: ""      # for example, '/blog' if your blog hosted on 'host/blog'
github_repo: "https://github.com/carlosw0713/carlosw0713.github.io.git" # 博客地址
```

#### _config-社交平台账号
```yaml
# SNS settings
RSS: false
# weibo_username: carlos111
# zhihu_username: carlos1
github_username: carlosw0713
# twitter_username: carlos1
#facebook_username:  carlos1
#linkedin_username:  carlos1
```

如果需要添加或者修改可以到_includes/sns_links.html 进行添加修改
不需要显示的话直接注释掉。效果图如下
![](https://raw.githubusercontent.com/carlosw0713/carlosw0713.github.io/master/img/Art_img/blog/_post_code.png#id=GQRgX&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

#### _config-侧边栏
```yaml
# Sidebar settings
sidebar: true # whether or not using Sidebar.
sidebar-about-description: "乐观的悲观主义者 <br> Email:Carlos.w.0713@outlook.com" #个人描述（可以使用html语法）
# sidebar-avatar: https://github.com/carlos.png #个人头像 可以设置为网页链接或者路径 
sidebar-avatar: /img/about-Carlos1.jpg #个人头像 可以设置为网页链接或者路径
```
![](https://raw.githubusercontent.com/carlosw0713/carlosw0713.github.io/master/img/Art_img/blog/home_side.png#id=iDtQ3&originHeight=325&originWidth=675&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)


#### _config-好友
```yaml
friends:
  [
    { title: "Carlos", href: "https://github.com/carlosw0713" },
    { title: "Gtihub", href: "https://github.com/carlosw0713" },
    { title: "Gitee", href: "https://gitee.com/carlos_w_0713" },
    { title: "篮球", href: "https://baike.baidu.com/item/%E7%A7%91%E6%AF%94%C2%B7%E5%B8%83%E8%8E%B1%E6%81%A9%E7%89%B9/318773" },
    { title: "漫画&动漫", href: "https://zhuanlan.zhihu.com/p/584071572" },
    { title: "自由", href: "https://zhuanlan.zhihu.com/p/443866356" },
    { title: "ChatGTP", href: "https://c.binjie.fun/" },
  ]
```
![](https://raw.githubusercontent.com/carlosw0713/carlosw0713.github.io/master/img/Art_img/blog/home_friends.png#id=RstRb&originHeight=326&originWidth=675&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

#### img-图片配置

1. 应用场景：
   - 文章的 head 图片展示
   - 页面的 head 图片展示
   - md文件调用的 图片展示
2. 使用方法：
   - 调用图片一般相对路径方式获取例如 img/文件夹名（可以零个至多个）/图片名称

#### _posts-md文件设置（划重点！！！）
效果展示：
![](https://raw.githubusercontent.com/carlosw0713/carlosw0713.github.io/master/img/Art_img/blog/_post_settings_introduce.png#id=yRb9C&originHeight=327&originWidth=675&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

_post可以说的上是整个博客最重要的部分了，应为文章都统一存放在这个页面。需要注意点如下：

1. 文章抬头设置
```
---
ifupdate: false #是否需要更新配合初始化代码使用
layout: post     
title: Jekyll-博客模板	#文章标题
subtitle: 模板	#文章副标题
date: 2023-04-03	#文章日期
author: Carlos	#作者
header-img: img/bg-cook.jpg	#文章 head 图片
catalog: true	
tags:	#  网页 tags 标签
 - 博客模板
 - 博客入门	
---
```

2. 文件名称和路径设置
   - 文件名称需要设置为` yyyy-MM-dd-文件名格式`。格式不正确jekyll将不会解析该md文件
   - 路径可以设置在根目录下或者子目录下都行，建议设置为 大类/小类/文件名 ，例如 Python/Python高级操作/2023-05-21-Python日志操作

Ps：
因为在jekyll 中，Markdown文件可以包含HTML代码。Jekyll会自动将Markdown文件转换为HTML页面，并保留其中的HTML标签。如果你在Markdown文件中使用了Liquid模板语法，可以会导致网页找不到对应的数据，需要使用{% raw %}和{% endraw %}标记来避免Liquid解析其中的内容。例如：
```
{% raw %}
这是一段包含Liquid模板语法的代码：{{ variable }}
{% endraw %}
```

#### _post-md文件 批量初始化或更新操作
看完上述md文件所需要的模板格式设置， 内容好像有点多又比较麻烦，对于没用写过博客和已经写过博客的同学需要花费时间去重新创建和修改，这边提供了一种思路，就是用代码对文件实现批量操作。
**文件路径格式：**//大类/小类/文件名 例如// Python/Python高级操作/Python日志操作
**代码思路：**

- 使用python的文件操作依次遍历获取_post下的md文件。
- tags取值为根目录名称，subtitle取值为子目录名称，title取文件名，date取当天或指定时间。
- 将内容插入文件的首行，并且再对文件名赋值为 date-文件名。
- 如果需要修改同样可以指定路径下文件，对某内容进行替换操作。

代码已经写好，可以参考一下 [《Python批量修改文件内容操作》](https://carlosw0713.github.io//2023/07/31/Python批量修改文件内容操作/)。
![](https://raw.githubusercontent.com/carlosw0713/carlosw0713.github.io/master/img/Art_img/blog/about_blog_init.png#id=mKw71&originHeight=266&originWidth=675&originalType=binary&ratio=1&rotation=0&showTitle=false&status=done&style=none&title=)

### 本地运行

1. 克隆 Repository
   - 在命令行中执行以下命令，克隆刚刚创建的 Repository 到本地：
```
Copy Codegit clone https://github.com/你的用户名/你的用户名.github.io.git
```

2. 启动 Jekyll 服务器
- 在安装好jekyll的前提下，cmd命令切换到仓库文件目录下，执行以下命令来启动 Jekyll 服务器：
```
bundle exec jekyll serve
```
- 在浏览器中访问 [http://localhost:4000](http://localhost:4000/) 就可以看到你的 Jekyll 网站了，你对本地博客的修改都会在这个地址进行显示，修改配置后网址要`强制刷新`才会展示。


## 致谢

1. 博客模板是 [Hux](https://github.com/Huxpro/huxpro.github.io) fork 的, 非常感谢这个作者。
2. 感谢 Jekyll、Github Pages 和 Bootstrap。

