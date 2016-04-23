---
layout: post
title: "Git 与 GitHub使用指南汇总"
subtitle: "\"有人说...看过很多git教程，依然过不好此生.....\""
author: mgsweet
date: 2016-04-23 15:54:55 +0800
categories: git
tag: git
---

*有人说...看过很多git教程，依然过不好此生.....*

*好啦，不要灰心，其实很简单的，不过我不是要自己写一篇git与github使用教程，本帖纯粹分享优秀教程地址。*

最近还发现了一个问题，不知道大家有没有相同的问题，不知道是不是装了极路由的缘故还是校园网的缘故，我只有用手机热点才能与github连接，如果连wifi的话会弹出一下信息,就是说你见到以下报错可能不是你的ssh出问题，而是....你用了校园网？持续更新

>fatal: 'origin' does not appear to be a git repository
fatal: Could not read from remote repository.
>
Please make sure you have the correct access rights
and the repository exists.

自我学习过程中还是遇到不少问题的，如果下载了客户端的话貌似会自动生成一个github_rsa公钥，反正我是删了重建的，那些公钥会放在隐藏文件夹，可以在命令行内进入再输入cat 加那个public的公钥名字就可以见到里面的内容了。然后，作为一个mac用户，强烈推介大家把终端的bash换成oh-my-zsh，高亮的字体和快捷键tab功能的改进都很有助于命令行上解决问题，大大提高效率，或者在安装的时候你还会用到homebrew什么的，也是很强大，极力推荐（mac用户）。最后呢，大家遇到问题多点百度谷歌知乎必应stack overflow咯，我也是新手，大家互相指教。

>这里先安利一下我的github:https://github.com/mgsweet，欢迎互粉互相学习，里面有一个今天打的改进eden输出的小程序，欢迎fork和pull request哈哈
>https://github.com/mgsweet/Eden-Answer-Improvement

**1.强烈推荐廖雪峰老师的git与github教程，我也是在那里学的，重点是....中文版！生动有趣，通俗易懂。**
>http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000

**2.git使用简易指南，这个更加简洁，方便指令查找**
>http://www.bootcss.com/p/git-guide/

**3.github常见操作和常见错误！错误提示：fatal: remote origin already exists.(这个是本人在连接本地库和github库时遇到的问题，在这里找到了解答)**
>http://blog.csdn.net/god_wot/article/details/10522405
另外查看当前传输状态可能会用到 git remote -v指令

**4.Git配置技巧**
>http://blog.csdn.net/wirelessqa/article/details/8572928
>配置你的用户名邮箱什么的，反正我也是用到了

**5.制造公钥，同一台电脑设置多个公钥与不同GITHUB帐号交互，重命名公钥**
>http://jingyan.todgo.com/shuma/2161775tdu.html
>之前设置了多个公钥导致ssh连接不上，坑爹


**6.最后分享下自己的整理**
git 命令
1.创建版本库
mkdir learngit(创建目录)
cd learngit
pwd(显示当前目录)
git add
git commit -m “what change you have make”
git status(显示结果)
git diff(显示不同)
git log (查看变化) —pretty=oneline(显示在一行)
HEAD 当前版本
HEAD^上一版本
HEAD~100上一百个版本
git reset —hard HEAD
git reset 1231244124
git reflog 纪录每次命令（后悔药）
git diff HEAD — readme.txt对比当前编辑版本与原来版本的区别
git checkout — file （可以丢弃工作区的修改）
git reset HEAD read.txt(可以清理暂存区)
git rm (git的删除，算是一种修改)
ssh-keygen -t rss -C “mgsweet@126.com”
git remote add origin git@github.com:mgsweet/learngit.git
git push -u origin master
git push origin master
git pull origin master

git clone git@github.com:mgsweet/gitskills.git
git checkout -b dev = git branch dev + git checkout dev + switched to branch ‘dev’(创建切换分支)
git branch(查看当前分支)
git merge ＋想合并的分支 (合并分支)
git branch -d 删除分支
git —graph —pretty=oneline —abbrev-commit
git merge —no-ff -m “merge with no-ff” dev (no-ff表示禁止fast forward)
git stash 暂时存储工作区
git stash list 列出暂存区
git stash apply 恢复
git stash drop删除
git stash pop恢复同时删除
git stash apply stash@{0}恢复指定的stash
git branch -D feature-vulcan强制删除没合成的分支





