---
# layout: post
# title:  更换评论系统之从多说到云跟帖
# date:   2017-06-08 00:00:00 +0800
# categories: document
# tag: 教程
---

* content
{:toc}


挥别			{#say-goodbyte}
====================================

从14年博客搭建起来，一直使用的是多说，期间很多人给我留言，有通过我的博客学到技术的，也有看到我博客模板然后拿去使用的，总之也积累了一定的评论量。期间想换Disqus，那时候还没有被墙，不过由于Disqus是国外产品，本地化做的不是很好。所以一直以来仰仗着多说来支撑着博客的评论。不过好景不长。也就大约17年的三月份左右，查看博客的时候，看到评论框上面有一个小链接，点击之后才知道6月1日，多说要永久的关闭了。前前后后使用了不到三年吧。还真的有那么点感情了，所以刚看到这个消息的时候还是很震惊的。不过也可以理解，一个无法成功商业化的项目，最后的结局也无非就是这样。但是由于心里的一些不舍，也就一直没有将多说替换下去，一直等到6月1号上班的那天早上10点多，我上线博客查看的时候还是正常可运行的。不过到6月2号，多说的域名就彻底无法访问了。这才知道，多说是真的走了！感谢这三年来的一路相伴，感谢多说团队曾经做过的努力。


选择			{#choose}
====================================

这几天就一直在寻找一个新的第三方品论，可供考虑的也无非就是畅言，友言，Disqus，云跟帖。

畅言要求必须有备案，这个不太好搞，所以就放弃了。

友言貌似也不稳定，今天查看他的服务的时候502了。

Disqus被墙，而我又极少翻墙。所以也不再考虑之列，最后也就只能选择云跟帖了。


网易云跟帖			{#yungentie}
====================================

由于云跟帖跟多说有一些小区别。对多说来说，安装完成之后，注册站点跟实际使用域名并没有硬性的要求必须一致，所以写完之后无论在什么地方都可以执行，而网易的这个云跟帖不同的是，会在每次页面加载的时候先获取当前访问的域名，然后跟你注册云跟帖时候的域名做检查，一致的话会放行并正确显示评论系统，不一致就会直接返回错误码，并且在页面不会显示任何内容。

所以，以后想要使用本Jekyll模板的小盆友们，`一定要记得修改自己的云跟帖导入代码`，才能让自己博客的评论系统生效。具体步骤如下：

登录云跟帖			{#login-yungentie}
---------------------

使用自己的账号登录[https://gentie.163.com/](https://gentie.163.com/)，然后点击右上角的`后台管理`

![/assets/img/yungentie/01.png]({{ '/assets/img/yungentie/01.png' | prepend: site.baseurl  }})

初始化			{#init-yungentie}
---------------------

如果是第一次登录云跟帖会提示完善站点基本信息。

![/assets/img/yungentie/01.png]({{ '/assets/img/yungentie/02.png' | prepend: site.baseurl  }})

完成之后点击`获取代码`，选择合适的皮肤进行设置，本博客是蓝色，固定位置。

![/assets/img/yungentie/01.png]({{ '/assets/img/yungentie/03.png' | prepend: site.baseurl  }})

复制引入代码			{#import-yungentie}
---------------------

点击`WEB代码`, 在右侧的`跟贴完整模块代码(Web单独版)`中复制展示框中的代码

![/assets/img/yungentie/01.png]({{ '/assets/img/yungentie/04.png' | prepend: site.baseurl  }})

修改模板代码			{#change-template-code}
---------------------

修改`_includes/LessOrMore/comments-providers/yungentie`文件中的内容，将文件中的代码全部删除，并粘贴刚刚从云跟帖网站复制的代码。

![/assets/img/yungentie/01.png]({{ '/assets/img/yungentie/05.png' | prepend: site.baseurl  }})
