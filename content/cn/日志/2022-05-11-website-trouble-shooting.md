---
title: "技术：小白从零用Hugo搭建个人网站遇到的问题一览"
date: 2022-05-11T19:37:47+08:00
author: "张晶|孟维琦"
slug: website-building-trouble-shooting
draft: false
toc: true
---

**初衷：**搭建一个个人网站来应对入学Master、做简历等。首先，在用服务器条件下， 看起来很简单很容易上手的Typecho，Halo都被排除了，剩下的只有Hexo和Hugo。这两个都是静态网页，能够落到github上也比较符合实际需求。

**开始：**我就开始研究怎么搭建一个Hugo个人网页。

大体过程基本上基于[郝鸿涛个人博客中这篇《如何零基础免费搭建个人网站》](https://hongtaoh.com/cn/2021/03/02/personal-website-tutorial/) ，特别感谢！

## 开始搭建之前

我是一个彻彻底底的零基础，对编程的了解仅限于大学的基础编程课，which means我不知道HTML是什么、没有GitHub账号、没有用过git、也不会用markdown。

因此，先要做四件事情。

1. 注册一个GitHub账号
2. 下载一个Markdown的文本编辑器并学习Markdown的基础语法
   - 原因是之后所有的网站内容都会用Markdown来书写和搭建。我在尝试了几种编辑器之后，选了Markdown最好用的编辑器Typora，它有几个优点：文本和大纲可以同时显示；敲下来的语法，可以立刻显示为最终想要呈现的样子，对于初学者特别友好。
   - 关于Markdown的基础语法，我还是找了[B站视频](https://www.bilibili.com/video/BV1hJ411X75X?spm_id_from=333.337.search-card.all.click)，从代码块开始学，并且在Typora上面反复写几遍。反复写几遍也不能保证不出错，我在最后出现错误的时候才发现我一开始练习的插入图片的语法就是错误的。所以多练习是没错的。
3. 下载一个用于html的文本编辑器（推荐sublime text），方便修改后面的html
4.  （optional）这一步optional，但如果你是一个像我一样彻底的编程小白，是很有必要看一下这一步的。我在运行安装的时候，总是出现一串错误代码：

```java
xcrun: error: unable to load libxcrun (dlopen(/Library/Developer/CommandLineTools/usr/lib/libxcrun.dylib, 0x0005): tried: '/Library/Developer/CommandLineTools/usr/lib/libxcrun.dylib' (mach-o file, but is an incompatible architecture (have 'x86_64', need 'arm64e')), '/usr/lib/libxcrun.dylib' (no such file)).
```

这段让人比较困惑，我就拿到Stackoverflow上查了一下，发现我根本没有安装xcode开发展工具。解决这个问题需要在终端输入：

```java 
xcode-select --install 
```
下载 Xcode Command Line Tools

然后就可以用git了。

5. 为了正确地使用博客中的comment功能，需要提前安装utteranc.es，可以根据[这份指南](https://mscipio.github.io/post/utterances-comment-engine/)来做，只需要坐到第三步即可。在原本的partial—>footer文件中已有需要的script。需要注意的是：第一次开通评论区功能时需要严格按照[郝鸿涛个人博客中这篇《如何零基础免费搭建个人网站》](https://hongtaoh.com/cn/2021/03/02/personal-website-tutorial/)中对于评论区部分更改网址的步骤来操作，否则就会把评论接口调用到其他Github的issue模块中，那就只能再重新部署了。![孟小柒同学seven-图床图片-image](https://cdn.staticaly.com/gh/Archiemeng7/ARCHIE_personal-space-2022-2024@main/图床图片/孟小柒同学seven-图床图片-image.4z4tg4d05000.png)

6. 新建博客/日志时，只需参考[郝鸿涛个人博客中这篇《如何零基础免费搭建个人网站》](https://hongtaoh.com/cn/2021/03/02/personal-website-tutorial/)中复制content中的文件即可，但是需要注意的是：开头部分的内容修改不当，可能导致文件在Github的repository中的action能正常更新（不报错）：![孟小柒同学seven-图床图片-image](https://cdn.staticaly.com/gh/Archiemeng7/ARCHIE_personal-space-2022-2024@main/图床图片/孟小柒同学seven-图床图片-image.6mebmgau784.png)。但是，网页更新不出来那篇博文，可能原因如下：

   ```html
   title: "记录：小白狗子"
   date: 2023-01-15T17:07:45-05:00
   author: "孟维琦"
   slug: 小白狗子
   draft: false
   toc: true
   ```

   ①：data的日期还没到（比如今天的博文，日期写的是未来的某天的）。原因算法正常识别的话需要对应日期才能更新出来，哈哈哈哈哈·，这个功能有心人可以考虑给未来的自己写的日志（未来某天它就出现在自己网页上了）。

   ②：尽量在Typora的非源代码模式上直接编辑（可以直接使用Typora上的![孟小柒同学seven-图床图片-image](https://cdn.staticaly.com/gh/Archiemeng7/ARCHIE_personal-space-2022-2024@main/图床图片/孟小柒同学seven-图床图片-image.yngg8ivwy2o.png)操作排版)，当然打开源代码模式也行（如果你很了解Markdown代码语言)，但是某个小的操作可能会导致出现莫名其妙的Bug（开发者模式功能大，但是犯错几率也高😠)，当然出现的几率小，但遇到那种问题就很恼火。具体怎么个模式个人而定吧！

   ③：
7. Action出现Quened的时候，需要更新一天多会报错{deploy This request was automatically failed because there were no enabled runners online to process the request for more than 1 days. *github pages*: .github#L1
The ubuntu-18.04 environment is deprecated, consider switching to ubuntu-20.04(ubuntu-latest), or ubuntu-22.04 instead. For more details see https://github.com/actions/virtual-environments/issues/6002}
;解决办法：更改Workflow文件，{Workflows using the ubuntu-18.04 image label should be updated to ubuntu-latest, ubuntu-20.04, or ubuntu-22.04}，打开{gh-pages.yml}中直接改。

## 在set和deploy中需要注意

在搭建中同样有一些需要注意的地方。

1. 如果你像我一样在中国大陆地区使用了VPN并进行git更新，那么在建立过程中可能会屡次出现以下的错误代码：

   ```java
   Fatal: fatal: unable to access 'https://github.com/xxx': OpenSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443
   ```

   这是由于使用了代理。我们需要输入:

   ```java
   git config --global --unset-all remote.origin.proxy
   ```

   这个代码可以消除behind a proxy的影响。

2. 如果出现使用git获取github上代码时报错：OpenSSL SSL_read: Connection was reset, errno 10054

   (此时又必须开着[vpn](https://so.csdn.net/so/search?q=vpn&spm=1001.2101.3001.7020)才能访问到github)

   **参考网上的回答，成功解决问题：**

   ```java
   git config --global http.sslVerify "false"
   ```

2. 如何查看自己的deploy失败的原因

   如果你有绑定GitHub至自己的邮箱，或者你本来就是用自己某一邮箱注册的GitHub，那么出现失败，你会直接收到一份邮件，并打开邮件查看自己run失败的原因，然后进行修改。

   此外，还可以通过在repository—>code处点击commit，看自己失败还是成功。绿色的对勾代表已经部署成功，红色的叉号代表部署失败了。
   
4. 如果Hugo文件（电脑端）删除了文件，Gthub旧文件还在repository中，这时候deploy出现错误（记得git界面是几行标红的代码），经本人在“[stak overflow](https://stackoverflow.com/questions/28429819/rejected-master-master-fetch-first)”中查找到解决方案如下：

   Then follow these steps to merge:

   ```java
   git pull origin master
   ```

   注意以上代码，运行之后git会类似卡住，无法操作，Don't worry，只需将git关闭即可，之后再运行deploy命令：

   ```html
   bash deploy.sh
   ```

   即可正常部署，delete原Github库中的无用文件。

   <span style="display:block;text-align:left;color:purple;">**总结：**</span>🙆其实，目前**问题1**和**问题2**本质上都是网络原因导致的，只能说采用对应的解决方法可以起到缓解作用，但是如果网速真的不行，两个解决办法不发挥作用，也正常，只能多试试了，或者错时段再部署。

## 如果有需要修改layout

1. 我遇到的第一个需要修改的问题就是在搭建完网页之后，首页下方的评论中依然是郝鸿涛网页中的评论。这个原因是在`layouts` -> `partials` -> `footer.html` 里用的是他的 repo，这里需要把这行链接换成自己的。

2. 方便增加图片的方法：

   可以在`static` （static放在根目录下即可）中新建一个文件夹， 比如image或者picture之类的，挑自己喜欢的名字。之后再加入图片的话可以在帖子中这样加：
   ```java
   {{figure src= "/images/image.jpg" title = "blablabla" caption = "blablabla" width = "xxx"}}
   ```

   2.1 增加图片的方法也可以参考**图床**[^Picx图床神器]的方式实现，本质原理是将复制的图片上传到Github的repository中，通过图床平台生成Md外链，直接调用显示，超级超级方便，直接复制图片上传图床生成外链，复制外链到日志相应位置即可（详细检索即可查到教程，推荐[**Picx图床神器**](https://picx-docs.xpoet.cn/tutorial/get-start.html#%E8%BF%9B%E8%A1%8C%E5%9B%BE%E5%BA%8A%E9%85%8D%E7%BD%AE)）。

   **流程如下：**

   ```mermaid
   flowchart LR;
   A((复制需要使用的图片Ctrl+C)) -->|Copy| B(设定的图床平台,并直接上传Ctrl+V)
   B --> C{图床外链https}
   C -->|One| D[复制外链到.md文件中]
   C -->|Two| E[其他支持md语言的文件中,Eg:Obsidian等]
   ```
   
   
   
3. 需要修改Logo

   在建完网站后，网站默认的是左上角的Hugo-logo，但是可能我们并不喜欢。这时需要找到文件夹themes—>static—>media，并找到其中的Hugo-logo.png。这时你需要自己建一个新的png（保证透明底，可以使用APP**醒图**操作）的文件，即设计一个你自己的logo。我打开photoshop然后随便画了个自己的。

   然后把config.toml文件中params中的favicon中的hugo-logo.png改为你新建的这个png文件。params.logo这里同步改。

   

4. 需要修改网站的名字

      依然是在params.logo这里，修改alt这行

5. 高级绘图示例：

      ```mermaid
      gantt
      
      dateFormat YYYY-MM-DD
      title 开发计划
      
      section 需求文档
      	登录注册:done,login,2021-06-25,2021-06-28
      	添加好友与分组:add, 2021-06-29,3d
      	单聊 :active ,chat, 2021-07-01,2d
      	群聊 :groupChat,after chat,5d
      	朋友圈 :crit,5d
      	其他:3d
      section 开发
      	开发登录注册:done,d-login,2021-06-25,24h
      	开发添加好友与分组:active,d-add,after d-login,5d
      	开发单聊与群聊:crit,d-chat,after d-add,7d
      	开发朋友圈:d-friend,after d-chat,7d
      	
      section 测试
      	测试用例与玩耍:active,test,2021-06-25,10d
      	开始测试部分接口:crit,start-test,after test,11d
      ```
      
      ```mermaid
      	pie
              title 今天晚上吃什么？
              "火锅" : 8
              "外卖" : 60
              "自己煮" : 8
              "海底捞" : 9
              "海鲜" : 5
              "烧烤" : 5
              "不吃" : 5
      ```
      
      
      
      
      
      
      
      ```mermaid
      journey
          title 我的一天
          section 早上
            吃饭: 5: Me,Her
            跑步: 3: Me
          section 工作时间
             坐地铁到公司: 5 :Me
             上班: 1:Me
          section 晚上
            睡觉: 5: Me,Her
      ```
      
      
      
6. 如果出现使用git获取github上代码时报错：OpenSSL SSL_read: Connection was reset, errno 10054

   (可以参考某blog中方法修改文件内容（If it were me, I’d try to upgrade everything and see what happens. In .github/workflows/gh-pages.yml…），[vpn](https://discourse.gohugo.io/t/build-failed-because-it-uses-a-deprecated-version-of-actions-upload-artifact-v3/53335)依次修改即可解决问题)

   **参考网上的回答，成功解决问题：**

| Old value | New value |
| --- | --- |
| actions/cache@v3 | actions/cache@v4 |
| actions/configure-pages@v3 | actions/configure-pages@v5 |
| actions/deploy-pages@v2 | actions/deploy-pages@v4 |
| actions/upload-pages-artifact@v2 | actions/upload-pages-artifact@v3 |
| peaceiris/actions-hugo@v2 | peaceiris/actions-hugo@v3 |
      
     
7. How to develope academic personal website?
   可以参考某MIT中open-source repository [academicpages.github.io](https://github.com/academicpages/academicpages.github.io)
   Detailed Chinese version of instructions can be found in this csdn blog: [手把手教你用github制作学术个人主页（学者必备）](https://blog.csdn.net/qd1813100174/article/details/128604858)
     Noted: 注意：_config.yml文件中的"url: username.github.io"这个地方要修改，不然你的照片会无法显示（笔者在这里踩坑了快一个小时）
     
      



[^Picx图床神器]: https://picx-docs.xpoet.cn/tutorial/get-start.html#%E8%BF%9B%E8%A1%8C%E5%9B%BE%E5%BA%8A%E9%85%8D%E7%BD%AE
