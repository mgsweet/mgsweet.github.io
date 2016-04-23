---
layout: post
title: "jekyll博客文章生成器制作"
subtitle: "\"简便的文章模版运用\""
author: mgsweet
date: 2016-04-23 15:18:18 +0800
categories: jekyll rake
tag: jekyll
---


前言
---
```
---
layout: post
title:  "Welcome to Jekyll!"
date:   2016-03-04 10:52:19 +0100
categories: jekyll update
---
```
每次写文章，都要重新写一遍这种开头然后把文件重命名成固定的格式是不是很烦？这种重复性的东西我们就把它自动化，通过Rakefile去解决，它类似shell这样的脚本，可以使用交互模式。以下是 [pizida](http://pizida.com/technology/2016/03/03/use-jekyll-create-blog-on-github/)的Rakefile,可以复制后命名为Rakefile，放在站点根目录直接使用，也可以修改为适合自己的Rakefile：现在有了rakefile就可以直接生成了。


RAKEFILE
---

```
task :default => :new

require 'fileutils'

desc "创建新 post"
task :new do
  puts "请输入要创建的 post URL："
  @url = STDIN.gets.chomp
  puts "请输入 post 标题："
  @name = STDIN.gets.chomp
  puts "请输入 post 子标题："
  @subtitle = STDIN.gets.chomp
  puts "请输入 post 分类，以空格分隔："
  @categories = STDIN.gets.chomp
  puts "请输入 post 标签："
  @tag = STDIN.gets.chomp
  @slug = "#{@url}"
  @slug = @slug.downcase.strip.gsub(' ', '-')
  @date = Time.now.strftime("%F")
  @post_name = "_posts/#{@date}-#{@slug}.md"
  if File.exist?(@post_name)
      abort("文件名已经存在！创建失败")
  end
  FileUtils.touch(@post_name)
  open(@post_name, 'a') do |file|
      file.puts "---"
      file.puts "layout: post"
      file.puts "title: #{@name}"
      file.puts "subtitle: #{@subtitle}"
      file.puts "author: pizida"
      file.puts "date: #{Time.now}"
      file.puts "categories: #{@categories}"
      file.puts "tag: #{@tag}"
      file.puts "---"
  end
  exec "vi #{@post_name}"
end
```
*上面的内容可以更改，例如作者名，只要把file.puts后的东西改成你想要的就可以了。*

如何使用Rake,首先你要安装Rake
`gem install rake`
输入一下命令
`rake new`
rake会启动交互模式，让你依次输入title，subtitle，author，categories，tag等信息，并为你创建好具有头信息的markdown文件。如下一样:
```
请输入要创建的 post URL：
testurl
请输入 post 标题：
testpost
请输入 post 子标题：
subtitle    
请输入 post 分类，以空格分隔：
jekyll
请输入 post 标签：
技术
```

把这个makefile放在跟目录，运行后文件会自动保存到—post目录，很方便对吧
