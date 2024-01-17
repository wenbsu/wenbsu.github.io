---
ifupdate: false
layout: post
title: Git同时配置Gitee和GitHub
subtitle: git针对仓库的一些操作
date: 2024-01-17
author: wenbsu
header-style: text
#catalog: true
tags:
- Git
---

## 清除git的全局设置
以下所有命令建议在 git bash 中完成。  
如果是之前没设置过的，就不用清除了。  
可以通过git config --global --list来查看是否设置过。  
```
git config --global --unset user.name "你的名字"
git config --global --unset user.email "你的邮箱"
```

## 生成新的 SSH keys
### GitHub 的钥匙
```
ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "xxx@qq.com"
```
邮箱写自己的，执行命令疯狂回车即可  

### Gitee 的钥匙
邮箱换一个。不要跟上面相同就行  
```
ssh-keygen -t rsa -f ~/.ssh/id_rsa.github -C "xxx@vip.qq.com"
```
疯狂回车即可  
完成后会在~/.ssh / 目录下生成以下文件：  
* id_rsa.github
* id_rsa.github.pub
* id_rsa.gitee
* id_rsa.gitee.pub

![/git/20240117/0-2.jpg](https://foruda.gitee.com/images/1705462172482829788/3ab1f50f_1002526.jpeg)

## 识别 SSH keys 新的私钥
默认只读取 id_rsa，为了让 SSH 识别新的私钥，需要将新的私钥加入到 SSH agent 中  
```
ssh-agent bash
ssh-add ~/.ssh/id_rsa.github
ssh-add ~/.ssh/id_rsa.gitee
```

## 多账号配置 config 文件
创建config文件  
```
touch ~/.ssh/config 
```
config 中填写的内容  
```
# github
Host github.com
    Port 443
    HostName ssh.github.com
    User git
    IdentityFile ~/.ssh/id_rsa.github

# gitee
Host gitee.com
    Port 22
    HostName gitee.com
    User git
    IdentityFile ~/.ssh/id_rsa.gitee
```

## 添加 ssh

https://github.com/settings/keys  
将 id_rsa.github.pub 中的内容填进去，起名的话随意。

https://gitee.com/profile/sshkeys  
将 id_rsa.gitee.pub 中的内容填进去，起名的话随意。

## 测试成功
```
ssh -T git@gitee.com
ssh -T git@github.com
```
如图成功设置  

![/git/20240117/0-1.jpg](https://foruda.gitee.com/images/1705462156221994668/50172665_1002526.jpeg)