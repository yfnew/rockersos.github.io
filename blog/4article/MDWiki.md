# 使用 MDWiki 搭建个人轻博客、知识库、或文档中心

NOTE:本文介绍了结缘MDWiki的历程，接着阐述了 Leansoft 文档中心转换到MDWiki的过程，最后介绍了MDWiki的使用及部署。当我们要创建轻博客、笔记、知识库，甚至是产品/项目的文档时，MDWiki将是一个不错的选择。

## 背景

**个人知识库的惨痛经历**

在七、八年前，曾经用过一个知识库客户端工具，我将电子书、收藏的文章、笔记，全都放在了这个知识库中，随着时间的推移，数据文件越来越大，后来由于重装系统，久而久之数据文件损坏，所有数据都没了，欲哭无泪。后来想想这类工具其实不太适合自己。

**BlogEngine历险记** 

后来想搞个人博客，考虑过 `WordPress` 和 `BlogEngine`，最终还是选择了 `BlogEngine` (一个基于Asp.Net的开源博客系统)，然后在 Godaddy 买了域名、虚拟空间，花了不少时间折腾。使用一段时间后发现编辑文章还是挺麻烦（原谅我是一个比较懒的人~_~）,最关键的是要花钱续空间，已经失去了动力，坚持 一年多最后还是放弃。

在往后，大概在2014年左右，发现亚马逊AWS上有免费云主机可申请，1刀可用一年，于是继续折腾（生命在于折腾~），用了一年时间，过期后，信用卡还差点就被扣了一波费用，最终还是放弃。

**为什么不选择托管博客？**

可能有的同学问，怎么不用托管的在线博客，比如博客园，其实曾经也想过，一方面这种博客太重，编辑略麻烦，做为一名程序员，还是希望有自己的域名，有自己独立的博客站点，个人觉得这样会比较酷~，难道不是吗？

**程序员的曙光**

从2013年开始，使用 **Markdown格式的文档** 的机会多了起来，慢慢的喜欢上了这种格式，优点这里不多说了，看看维基百科上的介绍：

```
Markdown 是一种轻量级标记语言，John Gruber于2004年创建。它允许人们 使用易读易写的纯文本格式编写文档，然后使用其他工具转换成有HTML、其他RTF文档（如 Word、PPT）。

MD的目的是希望大家使用“易于阅读、易于撰写的纯文字格式，并选择性的转换成其他文档。 其中最重要的设计是可读性，也就是说这个语言应该要能直接在字面上的被阅读，而不用被一些格式化指令标记（像是RTF与HTML）。 因此，它是现行邮箱标记格式的惯例，虽然它也借鉴了很多早期的标记语言（Setext、Texile、reStructuredText）。 

由于 MD 的轻量化、易读易写特性，并且对于图片，图表、数学公式式都有支持，目前许多网站都广泛使用 Markdown 来撰写帮助文档或是用于论坛上发表消息。例如：GitHub、reddit、Diaspora、Stack Exchange、OpenStreetMap 、SourceForge等。甚至Markdown可以用来编写电子书、翻译书籍。
```

**无论是用来写文章、记笔记、PPT、写电子书，MD格式都是最睿智的选择。**

**基于MD格式的工具**

围绕MD格式，也涌现了很多基于MD格式的转换工具（比如比较流行的有：`jekyll`），有基于Nodejs、Python、Go、PHP等等，结合持续集成工具可以让我们更加专注于编写文档本身。

但是，这些始终都依赖后端语言和第三方工具来生成静态HTML。感觉还是有点麻烦（前面我说过自己有点懒，说得没错吧？~），要搭一个轻博客还需要找一个持续集成平台或构建工具。于是我想：

**有没有一种基于纯前端技术的工具——只需把MD文件部署在一个Web Server 就可以了，访问时即时解析并渲染成HTML？在本地编辑完MD文件后，只需运行 `git push`命令 ，刷新网页就可以查看奋战成果了？而且本地永远都会有一份完整的MD原文件，甚至还可以同步到网盘，走到哪写到哪，永远不会丢失，不亦乐乎？**

## MDWiki 隆重登场 

最后，大概在2015年左右，在 `交友网站－Github`上 终于找到了想要的工具，没错就是 开源工具：**MDWiki** ，简直开森得不要不要的~。

官方地址：

- 源码仓库地址：https://github.com/mdwiki/mdwiki
- 帮助文档： https://dynalon.github.io/mdwiki

NOTE:帮助文档本身就是 MDWiki 使用的一个例子，使用Github Pages 部署在 github.io 上。

**MDWiki技术栈：**

- marked
- jQuery
- Bootstrap
- Bootswatch
- colorbox
- highlightjs
- TypeScript（0.6.x版本之后使用TS重写了）

MDWiki 使用了前端框架 `Bootstrap`,所以手机端也是有很好的体验的哦，不信继续往下看。

MDWiki 提供的保存和部署方法：

  * [Hosting MDwiki on GitHub](https://dynalon.github.io/mdwiki/#!tutorials/github.md)
  * [Hosting MDWiki on Google Drive](https://dynalon.github.io/mdwiki/#!tutorials/drive.md)
  * [Using MDwiki with Dropbox](https://dynalon.github.io/mdwiki/#!tutorials/dropbox.md)
  * [Set up MDwiki with IIS Server](https://dynalon.github.io/mdwiki/#!tutorials/iis/iis.md)

后来，我用 `MDWiki + Github Pages`,创建了自己的轻博客，关键是没有任何成本，只要愿意折腾即可.目前已经有三个年头，欢迎 Flow，地址：

- 源码地址：https://github.com/liminany/m/
- 预览地址：https://liminany.github.io/m


部署其实很简单,只需要把这四个文件和MD文件放到Web Server的目录下即可

**站点创建步骤**

 - 创建github 仓库
 - 从本站获取四个文件
    - config.json: 站点配置文件
    - index.html : 整合和压缩后的解析文件
    - index.md: 首页
    - navigation.md: 顶部导航配置
 - 创建目录 site,在目录中添加md文件，可以规划一下自己的目录结构
 - 修改navigation.md站点导航文件内容，建议规划一下站点的导航
 - 使用 `git push` 推送到 github
 - 在自己 github 仓库中,依次进入 `Setting -> GitHub Pages-> Source` 选择主分支保存。[设置参考地址](https://pages.github.com/)

**就是这么简单，在本地用Notedpad++ 或者是VS Code编辑好MD文件，推送，站点立马更新好了！！！**

## DevOps 文档中心 的 MDWiki 升级之旅

后来，有幸加入 [leansoft](https://leansoftx.com/) 团队, 发现已经写了很多很棒的文档，采用的是 `reStructuredText`格式, 使用 `sphinx-build` 生成HTML，具体可参考（不建议采用下面的方式）：

- reStructuredText 文档发布流水线： 

https://devopshub.cn/2017/01/06/markdown-rest-release-pipeline/


我也试着用`reStructuredText`写了一些文档，发现这语法使用起来有点别扭，毕竟已经习惯MD格式了，而且MD格式在业界使用得更广泛，于是我向`徐老师` 建言，推荐了MDWiki，后面一发不可收拾了，后来才发现是在给自己"挖坑"了—_—。


最后我们决定，把现有`reStructuredText`格式的文档全面转成MD格式，并通过MDWiki来渲染和展示。哇，这可是个不小的工程啊，“坑”就是这样形成的~。

**文档转换神器 Pandoc**

所幸的是，后来发现了一个超级转换工具（命令行工具）：`pandoc` ，可在全平台运行，支持非常多的文档格式之间的转换：

- 官网：http://www.pandoc.org/

- 支持的格式(太多了请查看图片):  
http://www.pandoc.org/diagram.jpg


- 转换命令：`pandoc +RTS -V0 -RTS $RstFile -f rst -t markdown -o $MDFile`

使用这个命令，我们很快就完成了格式的转换。另外，可以看看这篇文章：[DevOps文档中心的技术实践演进](https://mp.weixin.qq.com/s?__biz=MzA5NzU3Njc5Mw==&mid=2651201876&idx=1&sn=b374dc2a93c6498eb80f2f6298cb02d2&chksm=8b6c3362bc1bba74c8d39569e6a06c2201067793139b1becc4d0fa3c5bab79bbf670d13aca50&mpshare=1&scene=1&srcid=0107gfrrFLsThvVmcfF4KLrX#rd)

下面附上 文档中心2.0地址：

- https://docs.devopshub.cn/home

## MDWiki 扩展之路

文档中心2.0上线之后，我们的培训也采用了新的配套文档，后来发现还是有一些扩展的需求，比如：

- 添加评论功能
- 集成 ApplicationInsights，监控网站的访问情况
- 为改善学员在做动手实验时的体验，在文章底部添加了 `上一篇` 和 `下一篇` 两个导航链接


**集成评论系统**

对于评论系统，之前偿试过以下方案：

- Disqus
- Commentit
- 多说、友言（不用多说了，现在已经关闭）
- Gitment

**Disqus**

MDWiki 默认集成了 `Disqus` 第三方评论系统，在 访问底部添加 `[gimmick:Disqus](申请的Disqus标识)` 即可实现，可惜的是`Disqus`国内用不了，原因`你懂的`。


**Commentit**

比较适合使用`Jekyll` 来生成HTML的博客，这个工具会把评论插入到页面中，对于使用MDWiki轻博客不太适合，官方地址：https://commentit.io/

**gitment**

Gitment 结合 Github Issue 来实现评论，地址：

https://imsun.github.io/gitment/

目前来说，就这个合适些了，就准备用这个了。


除了第1个评论功能，后面两个（集成ApplicationInsights、添加导航链接）我们已实现（在分支0.6.x中），如果有需要，请留言或联系我们，晚些时候同步到Github仓库中去。

Git仓库地址：https://github.com/lean-soft/mdwiki


**扩展说明**

如果您想扩展MDWiki功能，在本地修改源码，`master` 分支可能构建不了，MDWiki官方采用的是 `travis-ci`来构建的，虽然显示构建成功，但是构建Release包没有上传，就算在本地构建成功了，生成的文件是有问题的，无法解析MD文件，蛋疼~，所以我们选择了 `0.6.x`分支进行扩展。

本地构建环境：

- nodejs
- npm
- typescript
- bower

构建命令：

- npm install
- npm install grunt-cli
- bower install
- grunt release `or` ./node_modules/.bin/grunt debug release

可参考源码中的 `.travis.yml` 文件或是 `makefile`文件。

## 尾声，敬请期待后续文章

至此，MDWiki介绍完毕，这些工作其实都是在之前就完成了，说来惭愧，去年的时候就想写这篇文章了，一直拖到现在才写，这么好的东西应该早点分享出来的，是吧？~_~! 

到今年，由于写文章的机会更多了，感觉开VS Code离线工作的方式，比较适合写原创文章，对于记笔记，还是在线编辑的方式比较简便，于是发现了 `https://prose.io/`,很方便，偶尔也用这个写一下。

直到今年，Azure DevOps Server（TFS）发布了一项新功能：即 Wiki功能，在TFS Wiki中记笔记也是很方便，可视化编辑，插入图片时，抓图后直接 `Crtl+V` 即完成，非常方便。

Azure DevOps Server（TFS）Wiki 本质是一个Git仓库，所以，下一篇文章，准备介绍一下 Azure DevOps Server（TFS）Wiki，并着重分享与 Mdwiki 的集成，在结合 `Azure DevOps Server (TFS) Pipieline `，自动发布文章到 `WordPress` 博客 ，敬请期待 [Azure DevOps Server (TFS) 之 Wiki知识库使用实践]()！