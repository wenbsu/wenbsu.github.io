![](https://raw.githubusercontent.com/wenbsu/wenbsu.github.io/main/img/md/check_my_home_page.jpg)

![](https://img.shields.io/badge/HTML-red)  ![](https://img.shields.io/badge/jekyll-green)  ![](https://img.shields.io/badge/Ruby-3.3.0-block)

![](https://img.shields.io/github/issues/carlosw0713/carlosw0713.github.io.svg?style=flat)  ![](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)  ![](https://img.shields.io/github/stars/carlosw0713/carlosw0713.github.io.svg?style=social&label=Star)  ![](https://img.shields.io/github/forks/carlosw0713/carlosw0713.github.io.svg?style=social&label=Fork)

## 关于

博客的模板是从 [Hux](https://github.com/Huxpro/huxpro.github.io) fork的。非常感谢这个这个作者。

详细教程参考 《[使用 GitHub Pages + Jekyll 搭建个人博客](https://wenbsu.github.io/2024/01/12/%E4%BD%BF%E7%94%A8-GitHub-Pages-+-Jekyll-%E5%BF%AB%E9%80%9F%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2%E7%BD%91%E7%AB%99/)》

### [点击查看博客详情 👆](https://wenbsu.github.io/)

## 部署

### 1. 本地安装 Jekyll

-  安装 Ruby和Devkit [Downloads](https://rubyinstaller.org/downloads/)
-  RubyGems 镜像源切换：`gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/`
-  Jekyll cmd命令：`gem install jekyll bundler`

### 2. 克隆到本地

- git clone git@github.com:wenbsu/wenbsu.github.io.git

### 3. 运行项目

- 在安装好jekyll的前提下，cmd命令切换到仓库文件目录下，执行以下命令来启动 Jekyll 服务器：

```
bundle install
bundle exec jekyll serve
gem update jekyll # 更新jekyll
gem update github-pages #更新依赖的包
```

- 在浏览器中访问 [http://localhost:4000](http://localhost:4000/) 就可以看到你的 Jekyll 网站了，你对本地博客的修改都会在这个地址进行显示，修改配置后网址要`强制刷新`才会展示

## 更多

1. 更多博客模板 [点击这](http://jekyllthemes.org/)。
2. Github Pages文档 [点击这](https://docs.github.com/zh/pages)。
3. Jekyll文档 [点击这](https://www.jekyll.com.cn/docs/)。