---
layout: post
title: "微信小程序 navigate页面跳转问题解决方案"
subtitle: "\"微信小程序开发问题与解决\""
author: mgsweet
date: 2017-08-29 15:30:18 +0800
categories: 微信小程序
tag: 微信小程序
---

最近在跟着别人做外包小程序，在跳转的时候遇到很大的问题 ，由于微信小程序的`navigateBack`是不会刷新原来页面的，所以当我要做到如下逻辑时，感到十分困惑，同时觉得无法控制后退按钮指向页面这一设定十分不科学。

先来看看问题所在，例如我要实现如下页面逻辑
![问题](http://img.blog.csdn.net/20170829151119454?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbWdzd2VldA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)
*星号表示添加了数据的地址管理页*

要做到能回退（回退的意思是指点击左上方按钮回到上一页面），我们不能用`redirectTo`去实现跳转，因为这个函数会把当前页面pop出页面栈，导致我们不能回退到正确的页面，而又不能在第三到第四阶段使用`navigateTo`或者`redirectTo`，因为这样的话回退不能直接回退到index，而是只会不断回退，再加上微信最多只能有5个页面，所以不能频繁使用`navigateTo`（保留当前页面跳转新页面），所以综合各种考虑，最后逻辑如图：

![这里写图片描述](http://img.blog.csdn.net/20170829152214236?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbWdzd2VldA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

那么问题来了，微信的`navigateBack`函数不但不刷新数据，而且也没有success回调函数提供，这里不得不自行调用页面刷新，例如：

```
//更新旧页面
var pages = getCurrentPages();
var prePage = pages[pages.length - 2];
prePage.getLocInfo();

wx.navigateBack ({
	url: '../locMan/locManView',
})
```

但在实际应用中可能就是存在另外一个问题，就是该段处理中，页面栈到底保留的是什么页面，一定要确保数据异步存储后再跳转页面，不然如果异步还没结束，页面就已经转移了的话 ，该解决方案会失败。
