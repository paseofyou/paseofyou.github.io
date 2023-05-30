---
title: "记录hugo建站全流程"
draft: false
date: 2023-05-30T12:00:48+08:00
cover:
  image: 
  alt: 
  caption: 
tags: ["hugo"]
---

## 简介

这里是个人选择hugo的背景故事，如果想快速搭建hugo，请跳过这一章节。

想着做技术，还是要一个属于自己的博客，记录笔记，记录日常，总结和规划等等。其实主要目的是：搭建自己的博客知识库，方便系统的学习以及随时复习~~（以及供某人随时监管学习的进度）~~。

其实在搭建本博客（hugo）之前首先是用的hexo，这个好是好，社区丰富，主题又好看，当初就是被他的炫酷的主题所吸引，花了许多时间搞那些花里胡哨的功能搭建hexo博客，用的butterfly主题。但是，使用了一段时间，总结了一点，太花里胡哨了，反而不适合当技术博客，看上面的技术贴也感觉非常奇怪。于是我又想寻找一种可以专注于个人知识库的技术网站搭建，然后找到了vuepress，因为它做的知识库，非常好看而且看起来就很舒服。我也用了一段时间。发现，它只适合做很完善的教程，个人虽然也能做，但是样式和目录等等配置起来非常难受，又要改这样又要改那样~~，虽然每个静态博客都少不了折腾，又没钱买云主机搭wordpress~~。而且我也想放一些个人的看法等等文章，这个框架就力不从心了。其实最致命的问题是，每次更改文章，构建一次慢的要死！推到git上面，还经常提交失败，他是先构建，后push，才构建成功。如果push的时候网络连接失败，就全部重来，就很搞心态。下来后，我感觉我犯了一个错误，就是博客不知不觉就想要去弄的花里胡哨的，主要单纯为了好玩才弄的花里胡哨，搞着搞着就忘了搭建博客的初心了。所以现在我追求简约，快速，功能少，分类详细就好了，所以我找到了这个hugo框架，听说是专业团队造的，很适合搞技术博客。我也看了很多教程，对比了gitbook，eleventy，docsify，大多都是bug太多，停止维护，编译很慢；还有wordpress以及typecho，这两个需要运维的经济成本，就不考虑了。好了，废话不多说了，开始搭建。

在搭建之前，可以看一下官方的示例：[https://adityatelange.github.io/hugo-PaperMod/](https://adityatelange.github.io/hugo-PaperMod/)。再决定是否选择该主题。



## 开始搭建

1. 准备工作

   1. 下载软件

      1. hugo的程序包：点击链接可以进入官网下载: [https://github.com/gohugoio/hugo/releases/latest](https://github.com/gohugoio/hugo/releases/latest)。

         （注意，官网推荐选择扩展版（extend版），如果后续需要功能扩展，选择这个版本更好。这里以0.112.5版本为例，比如windows64位，我就选择[hugo_extended_0.112.5_windows-amd64.zip](https://github.com/gohugoio/hugo/releases/download/v0.112.5/hugo_extended_0.112.5_windows-amd64.zip)。）

      2. git程序包：点击链接可以进入官网下载: [https://git-scm.com/download/win](https://git-scm.com/download/win)。然后自行配置到能正常使用github的push功能。
   
   2. 将hugo程序包放到某个地方，比如：`D:\hugo\bin`。然后将这个路径放到系统环境变量，使得在cmd能够直接使用hugo命令。
   
2. 开始建站

   1. 在你想放置网站源代码的文件夹，打开cmd，输入命令。(请详细看注释，再改命令代码为你需要的样子)

```bash
      hugo new site quickstart # quickstart换成你想要的网站项目名
      cd quickstart # quickstart换成你想要的网站项目名
```

   2. 安装paperMod主题包。

```bash
     git init #git仓库初始化
     git submodule add --depth=1 https://github.com/adityatelange/hugo-PaperMod.git themes/PaperMod
```

   3. 将theme文件夹里面的paperMod文件夹中，`layouts`,`i18n`,`assets`都复制到你的网站根目录中，也就是theme文件夹平级的地方。

   4. 将根目录中的hugo.toml删除，新建config.yml，并在里面写入，请根据自己的需要自行更改内容：

```yaml
     baseURL: http://example.org/
     languageCode: zh-cn
     title: paseofyou's blog
     theme: PaperMod
     
     
     params:
     # 你可以尝试着把profileMode以及以下的内容删除，刚刚那个样式怎么样，这是样式1
         profileMode:
             enabled: true
             title: 星痕 # 在这里更改站点名
             subtitle: "👏🏼这里是个人记录的地点。" # 在这里更改子标题
             imageUrl: "http://q.qlogo.cn/headimg_dl?dst_uin=863630017&spec=640&img_type=jpg" # 在这里更改头像名，也可以把863630017改为你自己的QQ号。
             imageTitle: 
             imageWidth: 150
             imageHeight: 150
             buttons:
               - name: ⏱️ 时间轴
                 url: archives
     # profileMode没有删除时，这是样式2
         homeInfoParams:
             Title: "Hello"
             Content: "welcome"
     #社交按钮
         socialIcons: 
             - name: github
               url: "https://github.com/paseofyou"  
     
     
         cover:
             linkfullImages: true
         
         showBreadCrumbs: true
         showReadingTime: true
         showShareButtons: false
         showPostNavlinks: false 
         
         
         env: production 
         author: paseofyou
         # author: ["Me", "You"] # multiple authors
         defaultTheme: dark  # defaultTheme: light or  dark 
         disableThemeToggle: false
         DateFormat: "2006-01-06"
         # disableSpecialistPost: true
         displayFullLangName: true
         ShowCodeCopyButtons: true
         hideFooter: false # 页脚
         ShowWordCounts: true
         VisitCount: true
         ShowLastMod: true #文章更新时间
         ShowToc: true # 目录
         TocOpen: true # 自动展开目录
         comments: true
         DateFormat: "2006-01-02" #这个别改！
     
     
     menu:
         main:
           - identifier: search
             name: 🔍搜索
             url: search
             weight: 1
           - identifier: home
             name: 🏠主页
             url: /
             weight: 2
           - identifier: posts
             name: 📚文章
             url: posts
             weight: 3
           - identifier: archives
             name: ⏱时间轴
             url: archives
             weight: 20
           - identifier: tags
             name: 🔖标签
             url: tags
             weight: 40
     
     
     
     enableInlineShortcodes: true #允许内联短码
     enableEmoji: true # 允许使用 Emoji 表情
     enableRobotsTXT: true # 允许爬虫抓取到搜索引擎
     
     hasCJKLanguage: true # 自动检测是否包含 中文日文韩文
     
     buildDrafts: false
     buildFuture: false
     buildExpired: false
     
     #googleAnalytics: UA-123-45 # 谷歌统计
     # Copyright: Sulv
     
     paginate: 15    # 每页显示的文章数
     
     minify:
         disableXML: true
         # minifyOutput: true
     
     permalinks: #浏览器链接显示方式
       post: "/:title/"
       # post: "/:year/:month/:day/:title/"
     
     defaultContentLanguage: zh-cn # 最顶部首先展示的语言页面
     defaultContentLanguageInSubdir: true
     outputs:
         home:
             - HTML
             - RSS
             - JSON
     markup:
         goldmark:
             renderer:
                 unsafe: true
         highlight:
             noClasses: false
             # anchorLineNos: true
             # codeFences: true
             # guessSyntax: true
             # lineNos: true
             # style: monokai
         
     
     
     privacy:
         vimeo:
             disabled: false
             simple: true
     
         twitter:
             disabled: false
             enableDNT: true
             simple: true
     
         instagram:
             disabled: false
             simple: true
     
         youtube:
             disabled: false
             privacyEnhanced: true
     
     services:
         instagram:
             disableInlineCSS: true
         twitter:
             disableInlineCSS: true
```

​     

   5. 启动网站，使用`Ctrl+C`可以终止网站，你每一次更改配置文件都需要重启：
```bash
      hugo server
```


## 分类配置

1. 从这里开始，每一次更改大多可以不用重启hugo服务，不过还是经常要重启来排除问题。可以参考以下的文章分类结构，在网站根目录的`content`文件夹下：

```bash
content
├─archives
│      _index.md
│
├─posts
│  └─大分类1
│      │  _index.md
│      │
│      ├─分类1
│      │  _index.md
│      │       
│      └─分类2
│         _index.md
│
├─search
│      _index.md
│
└─tags
       _index.md
```

其中tags是网站自带的，如果想自定义页面，则只能将其放在根目录新建`_index.md`才能使用，这个名字`_index.md`是约定的，不能换成别的，其他都可以换。

2. 每个分类都需要新建`_index.md`来自定义，自定义配置如下，请自行修改：
```markdown
   ---
   title: "分类名1" # 分类名
   hidemeta: true # 隐藏作者发布时间
   description: 这里将展示所有的文章。
   url: 
   ---
   
```

3. 其他的特殊分类，比如`archives  tags   posts  search` ，则需要以下的`_index.md`配置

```markdown
   ---
   title: "搜索" 
   layout: search # 改为对应的特殊分类：archives，tags，posts，search，categories
   url: search  # 改为对应的url路径
   ---
   
```

## 写文章

1. 开始编写文章，请注意，这里的文章都是markdown，请自行了解其编写语法，但是首先使用以下命令来创建文章

```bash
# 命令需要在网站根目录路径下使用，posts/my-first-post.md也可以改为自己需要的路径，以及更改文章名
hugo new posts/my-first-post.md
```



2. 更改文章的配置文件

```markdown
---
title: "标题" #标题
date: 2023-05-30T00:00:00+08:00 #创建时间
lastmod: 2023-05-30T00:00:00+08:00 #更新时间
author: ["me"] #作者
categories: 
- 分类1
- 分类2
tags: 
- 标签1
- 标签2
description: "" #描述
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true #是否展示评论
showToc: true # 显示目录
TocOpen: true # 自动展开目录
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
showbreadcrumbs: true #顶部显示当前路径
cover:
    image: "" #图片路径
    caption: "" #图片底部描述
    alt: ""
    relative: false
---

## 测试

测试文本
```

## 网站发布

发布的途径很多，比如用网站托管服务：vercel，Netlify。或者直接本地编译后，将打包后的静态网站发布到github，用page跑起来。不过我还是推荐github自带的actions的持续集成和持续交付(CI/CD) 。其他的方法我就不展示了，直接开弄github actions。

1. 首先在你的github新建一个公开仓库，推荐使用：paseofyou.github.io 其中，paseofyou换为你的github名字。这样搭建的网站的链接非常简化。点击以下内容进行复制

<img src="image-20230530111820260-1685416708183-1-1685416710398-3-1685416710979-5.png" alt="image-20230530111820260" style="zoom:67%;" />

2. 将你的网站源代码推到github上面。
```bash
# 把以下内容git@github.com:paseofyou/paseofyou.github.io.git 换为你复制的链接！
git remote add origin git@github.com:paseofyou/paseofyou.github.io.git # 警告！这里必须修改
git add .
git commit -m "inital"
git push -u origin master
```

3. 打开**github仓库**的**Settings**，点击pages，改为github actions

<img src="image-20230530112430155.png" alt="image-20230530112430155" style="zoom:67%;" />

4. 点击旁边的静态配置，会跳转到输入页面，将文件名改为`static.yaml`，内容编写如下，并保存。
```yaml
# Sample workflow for building and deploying a Hugo site to GitHub Pages
name: Deploy Hugo site to Pages

on:
  # Runs on pushes targeting the default branch
  push:
    branches:
      - master

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued.
# However, do NOT cancel in-progress runs as we want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Default to bash
defaults:
  run:
    shell: bash

jobs:
  # Build job
  build:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.111.3
    steps:
      - name: Install Hugo CLI
        run: |
          wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \
          && sudo dpkg -i ${{ runner.temp }}/hugo.deb          
      - name: Install Dart Sass Embedded
        run: sudo snap install dart-sass-embedded
      - name: Checkout
        uses: actions/checkout@v3
        with:
          submodules: recursive
          fetch-depth: 0
      - name: Setup Pages
        id: pages
        uses: actions/configure-pages@v3
      - name: Install Node.js dependencies
        run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true"
      - name: Build with Hugo
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo \
            --gc \
            --minify \
            --baseURL "${{ steps.pages.outputs.base_url }}/"          
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v1
        with:
          path: ./public

  # Deployment job
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v2
```
5. 保存成功后，返回仓库主页面，等待自动构建完成即可

<img src="image-20230530112549425.png" alt="image-20230530112549425" style="zoom:50%;" />

6. 访问你的网站吧，然后自己按照自己的需求更改即可。

<img src="image-20230530112734377.png" alt="image-20230530112734377" style="zoom: 80%;" />

7. 后续写文章，只需要写好保存后，输入以下命令，然后他就自己部署好了，记住要等几分钟，才能生效：

```bash
git add .
git commit -m "新增了一篇文章，测试文本"
git push -u origin master
```



## 踩坑

1. 配置域名时，要先把域名输入github的settings里面，再随便修改一下设置，使得运行一次自动构建，不然，就会无限循环重定向！而且config里面的baseUrl，似乎没啥用。

## 参考文章

我搭建过程中，主要想着两下造完，简约可用，整体美观就行，所以找了很多教程文章。每个教程写的很详细，但是问题就是太详细了，反而有点花里胡哨的感觉。所以我自己又找了很多教程。

1. Sulv  的建站建站教程：[https://www.sulvblog.cn/posts/blog/build_hugo/](https://www.sulvblog.cn/posts/blog/build_hugo/)
	这个就是太详细了，我只是想简单的使用博客写文章，并不想深入配置，而且他的配置文件有bug，我配置的时候，profileMode总是让我的项目报错。
2. git actions的官方搭建流程：[https://gohugo.io/hosting-and-deployment/hosting-on-github/](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
	只能说简单粗暴，实用。
3. 油管搭建视频（用魔法才能观看）：[https://www.youtube.com/watch?v=hjD9jTi_DQ4&t=2389s](https://www.youtube.com/watch?v=hjD9jTi_DQ4&t=2389s)
	这个视频帮助我理解了项目和搭建的基本知识和使用，不过最后他部署的时候使用的是Netlify，我更换成了githubActions。