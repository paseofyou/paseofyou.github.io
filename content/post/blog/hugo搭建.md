+++
title = 'hugo博客搭建'

categories=["blog"]

tags=["misc"]

date = 2024-06-04T10:12:50+08:00

+++

> 原本搭建了hexo和hugo的，发现我还是喜欢美观和性能取中间值，就有了现在这个blog

## 环境准备

1、下载hugo的exe：
https://github.com/gohugoio/hugo/releases/latest

官方推荐选择扩展的版本。

将exe放到电脑本地上，推荐`D:/software/hugo/bin`。并配好cmd的系统环境变量。

2、下载git，并链接好自己的github账号，直到能上传项目到号上为止（自行摸索）

3、notepad++、vscode、typora

## 开始搭建

> 先说思路，我一开始是对其他博客教程中的 github 分支里， main 做主分支，page 做文章发布页是持怀疑态度的，最后经过我10多小时的踩坑时间，发现这样做居然是最省力的，最高效的。所以我也准备这样做。
>
> 当然我很乐意分享我的博客源码，如果对分享比较敏感的小伙伴，可以创建两个仓库，一个用作博客源代码仓库，一个做文章发布仓库，用 github ci 来对两个仓库进行连接和推送也是可以的。可以根据我最后提供的 ci 代码进行更改也是能实现的。

1、在自己的github上新建项目，取名为`<你的github名字>.github.io`，将克隆链接复制下来备用。

2、首先在本地选好项目位置，新建文件夹后，在这个位置打开cmd

```bash
git clone <你刚刚复制的链接>
cd <克隆的项目>
hugo new site <博客名字>
```

> - **archetypes**：存放用 hugo 命令新建的 Markdown 文件应用的 front matter 模版
> - **content**：存放内容页面，比如「博客」、「读书笔记」等
> - **layouts**：存放定义网站的样式，写在`layouts`文件下的样式会覆盖安装的主题中的 `layouts`文件同名的样式
> - **static**：存放所有静态文件，如图片
> - **data**：存放创建站点时 Hugo 使用的其他数据
> - **public**：存放 Hugo 生成的静态网页
> - **themes**：存放主题文件
> - **config.toml**：网站配置文件

3、安装喜欢的hugo主题，在以下链接中选择一个主题。

https://themes.gohugo.io/

推荐使用以下命令进行安装。

```bash
git submodule add <主题克隆地址> themes/<主题名称>
```

此时theme文件夹里就有了刚刚下载的主题。

注意：不要在这个文件夹内修改，因为主题一旦更新就会被覆盖你做的主题修改。如果需要更改主题部分，可以把主题的内容复制到根目录对应的文件，即可随便修改。

4、主题中有许多预定义的格式设置，可以把它复制到theme文件夹同级的其他文件中。比如主题的content可以复制到自己网站的content。**不要傻瓜式的一次性复制过来，会报错！**一点一点的复制过来，复制一下，用下面代码运行一下。运行不了的不要复制过来，删掉复制过来的报错内容，没必要去修。

注意：你每次做更改，需要按下`ctrl+c`后重新运行才会生效。

```bash
hugo server
```

5、把主题的hugo.yaml (也可能是其他的文件)，复制到根目录，按你自己的喜好来更改就行。

> 有空了再慢慢配置修改，我们进行下一步。

## 网站写作

这个比较根据主题的内容来配置。建议把theme的content里，依葫芦画瓢。里面是什么配置就怎么去做。这里说点通用的。

Hugo 允许在文章内容前面添加 `yaml`, `toml` 或者 `json` 格式的前置参数。（就是你的typora最上方灰色那部分配置）

- **title**: 文章标题.

- **subtitle**: 文章副标题.

- **tags**:  文章标签.

- **categories**：文章分类.

- **date**: 这篇文章创建的日期时间。它通常是从文章的前置参数中的 `date` 字段获取的，但是也可以在网站配置中设置.

- **lastmod**: 上次修改内容的日期时间.

- **draft**: 如果设为 `true`, 除非 `hugo` 命令使用了 `--buildDrafts`/`-D` 参数，这篇文章不会被渲染.

- **author**: 文章作者.

- **authorLink**: 文章作者的链接.

- **description**: 文章内容的描述.

- **license**: 这篇文章特殊的许可.

- **tags**: 文章的标签.

- **categories**: 文章所属的类别.

- **hiddenFromHomePage**: 如果设为 `true`, 这篇文章将不会显示在主页上，但是此行为可以在网站配置中设置的.

- **featuredImage**: 文章的特色图片.

- **featuredImagePreview**: 用在主页预览的文章特色图片.

- **toc**: 如果设为 `true`, 这篇文章会显示右侧目录.

- **autoCollapseToc**: 如果设为 `true`, 文章目录会自动折叠.

- **math**: 如果设为 `true`, 将自动渲染文章中的数学公式.

- **mapbox**: 和网站配置中的 `params.mapbox` 对象相同.

- **lightgallery**: 如果设为 `true`, 文章中的图片将可以按照画廊形式呈现.

- **linkToMarkdown**: 如果设为 `true`, 内容的页脚将显示指向原始 Markdown 文件的链接.

- **share**: 和网站配置中的 `params.share` 对象相同.

- **comment**: 如果设为 `true`, 将启用评论系统.

> 其他的可以自行摸索，上面这些配置就够用了，大多数可以当字典用，现用现查。

另外，文章都放在 content 的 post 文件夹中，如果没有这个 post 文件夹需要自己手动创建。

在 post 里面写 markdown 格式文本才能看到（这是个坑，如果不这样就不会显示）。一般 theme 文件夹的 exampleSite 里都有示例的，依葫芦画瓢就行。

不建议用hugo的命令生成默认初始文章，推荐复制以前写的文章自行修改即可。

## github部署

首先在根目录创建文件 `.gitignore` ，里面填写 `/public/` 即可，用于忽略多余文件加快推送速度。

环境准备：

- 在github 上配置 action secrets 密钥 PERSONAL_TOKEN ，这个可以在用户界面 Settings/Developer Settings ，选择Personal access tokens ，经典token，然后添加密钥。  密钥权限选择仓库所有权限和 workflow 权限。复制好令牌密钥备用。
- 返回到博客项目，在项目的设置找到 Secrets and variables，里面的 action secrets 中，设置 secrets：
  `PERSONAL_TOKEN`，密码为上面的令牌密钥。
- 在项目设置中找到rules，新建分支rule ，**记得启用**，把当前分支允许操作别的分支权限给打开。
- 在项目设置的 page 中，将 source 改为 github actions 即可

部署环节：

我这里研究了一下 github ci，你可以根据我的github ci 配置来自行修改。

~~学有余力的同学可以自行了解ci知识点，我也不太会，但配置出来能用就行。~~

> 这个 github ci 是个大坑。
>
> 1. 它的根目录是基于内置的ubuntu来的，而不是仓库根目录，不要混淆！
> 2. hugo 命令确实生成了 public 文件夹，但存放在内置的ubuntu 内，而不是直接生成在仓库内！
> 3. 一定要一点一点的去调试，不要一步到位！
> 4. 只要是操作其他分支的操作，都需要令牌，令牌权限以及分支权限
> 5. checkout是检出代码，意思是从 github 仓库拉出代码，而不是 git 的切换分支！

即创建 `.github\workflows\deploy.yml`，里面写以下内容。

```yaml
name: deploy

on:
  push:
    branches: ["main"]
  workflow_dispatch:
  schedule:
    - cron: "0 0 * * *"

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  手动推送:
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v4
        with:
          submodules: true
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest"

      - name: Build Web
        run: hugo

      - name: push Web
        uses: peaceiris/actions-gh-pages@v3
        with:
          PERSONAL_TOKEN: ${{ secrets.PERSONAL_TOKEN }}
          EXTERNAL_REPOSITORY: paseofyou/paseofyou.github.io
          PUBLISH_BRANCH: page
          PUBLISH_DIR: ./public
          commit_message: ${{ github.event.head_commit.message }}
      

  自动定时更新:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          ref: page
          
      - name: Setup Pages
        uses: actions/configure-pages@v5
        
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./

      - name: Deploy to GitHub Pages
        uses: actions/deploy-pages@v4

```

现在为止，部署环境完成。现在每次推送文章都会自行构建网站，免去了每次写作后很多很多部署的麻烦。

把这个推送上去就会自动部署。

写好文章后，直接运行以下命令，把代码推上去即可。

```bash
git pull
git add .
git commit -m "<备注你想要的提交信息>"
git push origin main
```

如果 git 有问题，可以根据以下命令来修复。

```bash
# 以下内容是 git 配置，不用随便使用以下命令。
# 配置 git push 默认分支，之后就能用 git push 推送就行，不用 git push -u origin main
git push --set-upstream origin main 
# 如果你是新建的本地仓库，虽然和github的名字一模一样，但上传总会报错。用下面这个命令来合并即可。
git pull origin main --allow-unrelated-histories
# git 查看远程分支
git remote -v
# git 添加分支，其中 origin 是本地分支名称
git remote add origin https://github.com/paseofyou/paseofyou.github.io.git
# git 删除远程分支
git remote remove origin
```

有问题欢迎在评论区问我。（这部分挺难的）

## 评论系统

建议跟着官方教程走。

我这里选择的方案是：

- [twikoo](https://twikoo.js.org/quick-start.html)
- [mongoDB Atlas](https://twikoo.js.org/mongodb-atlas.html) 的 `AWS / Oregon (us-west-2)`
-  [Hugging Face 部署](https://twikoo.js.org/backend.html#hugging-face-部署)

## 本文引用

本文参考了许多博客，并对字典部分进行了摘抄，方便自己回看和帮助别人搭建，由衷感谢。

- 网站搭建部分：[文章1](https://cuttontail.blog/blog/create-a-wesite-using-github-pages-and-hugo/#2-%E5%AE%89%E8%A3%85-hugo) ;

- 网站写作部分：[文章1](http://shuzang.top/2019/hugo-blog-article-write/) ;

- 以及没有提到的博客，在此统一感谢

  
