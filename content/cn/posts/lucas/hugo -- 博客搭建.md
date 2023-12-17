---
title: hugo -- 博客搭建教程
date: 2023-12-17
description: 博客搭建教程
---
## 背景

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217144947.png)

[Hugo](https://gohugo.io/) 是用 Go 实现的博客工具，采用 Markdown 进行文章编辑，自动生成静态站点文件，支持丰富的主题配置，也可以通过 js 嵌入像是评论系统等插件，高度定制化。当然还有很多其他的，如 notion ，WordPress 等等，我喜欢 hugo 的主题，且最简单「侧重内容输出而不是网站维护」。  

上篇文章分享之后，有同学好奇如何搭建，问的比较多，我就简单的花半小时整理下，为了方便自己，做个记录，也方便大家，在这个人人都可以发声的时代，又感觉人人的喉咙都被扼住了，所以有兴趣可以搞起来吧。

本次我整理一个免费的教程，不用花一分钱，和域名，代理什么都不需要，也就是github 版本，利用 github pages 的免费 host 和自动部署功能，大家按照如下步骤，可以在 20 分钟内搭建出来。 

## 环境

### Windows（以这个为例子）

需要：git 包管理，hugo 预编译文件，Node.js, vscode(推荐)

git 包管理：
[Git - Downloads](https://git-scm.com/downloads)
![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217145558.png)

Node. Js
[Download | Node.js](https://nodejs.org/en/download/current)
![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217145634.png)

安装环境后，然后可以打开终端，输入 CMD，找到 powershell，然后按照下面的步骤进行构建。

我使用 scoop 进行安装 hugo 的 extension 版本
```bash
scoop install hugo-extended
```

安装完之后，就可以看到当前的版本了

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217150206.png)

## 本地

### 创建一个新的 blog

使用命令 `hugo new site` 来创建一个博客，例如，我用‘lucasloveann_blog ’这个名字可以根据自己的需要改

```bash
hugo new site lucasloveann_blog
```

### 进入刚刚创建好的博客文件夹中

在命令行中使用`cd`命令

```bash
cd lucasloveann_blog
```

### 给博客加个主题

把当前目录进行**github仓库**的初始化

```bash
git init  
```

我选择下载 hugo-blog-awesome 主题，并存放在 themes 文件夹中

> 主题地址
[Hugo blog awesome | Hugo Themes](https://themes.gohugo.io/themes/hugo-blog-awesome/)

```bash
git submodule add https://github.com/hugo-sid/hugo-blog-awesome.git themes/hugo-blog-awesome
```

把主题改为 hugo-blog-awesome

```bash
echo theme = "hugo-blog-awesome" >> config.toml
```

>我们可以将主题仓库直接 `git clone` 下来进行使用，但这种方式有一些弊端，因为当之后自己对主题进行修改后，可能会与原主题产生一些冲突，不方便版本管理与后续更新，我之前踩了这个坑。所以后面我采用的是将原主题仓库 `fork` 到自己的账户，并使用 `git submodule` 方式进行仓库链接，这样后续可以对主题的修改进行单独维护。

如果是 clone 了其他人的博客项目进行修改，则需要用以下命令进行初始化：

```bash
git submodule update --init --recursive
```

如果需要同步主题仓库的最新修改，需要运行以下命令：

```bash
git submodule update --remote
```

这时候，可以进入主题文件夹，进行预览
```bash
hugo server --themesDir ../..
```

建议，直接进入文件夹将 exampleSite 的内容全部复制到根目录上。我的是这个位置：

```
D:\lucasloveann_blog\themes\hugo-blog-awesome\exampleSite
```
![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217151127.png)

然后放到根目录：

```
D:\lucasloveann_blog
```

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217151242.png)

都完成之后，就可以进行发布第一篇文章了

```bash
hugo new posts/blog-test.md
```

进行 ``

```bash
hugo sever
```

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217151803.png)

预览如下

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217151832.png)

具体后面如何修改，直接修改里面有一个 `config.toml` 上面的代码，就是前端展示了。

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217152025.png)

更改东西，在发布之前记得进行 hugo 一下

```
hugo
```

目的是将网站内容转化为 html，完成之后可以看到本地有一个 `public` 文件，上面就是 hugo 之后的内容

Hugo 默认会将生成的静态网页文件存放在 `public/` 目录下，我们可以通过将 `public/` 目录初始化为 git 仓库并关联我们的 `xlmm/lucasloveann_blog.github.io` 远程仓库来推送我们的网页静态文件。

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217152406.png)

## 发布

进行发布到 github

先去 github 创建一个仓库，为了承接自己的本地文件。然后上传上去，也很简单。这个是我最终上传的样子。

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217152137.png)

```bash
初始化
git init

查看变化
git status

添加缓存
git add .

提交缓存
git commit -m "add test"

创建分支
git branch -M main

链接远程
git remote add origin https://github.com/xlmm/lucasloveann.github.io

进行推送
git push -u origin main
```

## 自动

设置自动发布，就是当自己有新 post 的时候，可以自动提交到线上。

这里有完整步骤，我说关键的
[Host on GitHub Pages | Hugo](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

创建自动文件

```bash
.github/workflows/hugo.yaml
```

将这些代码放上去这个文件 hugo. yaml

```
# Sample workflow for building and deploying a Hugo site to GitHub Pages name: Deploy Hugo site to Pages on: # Runs on pushes targeting the default branch push: branches: - main # Allows you to run this workflow manually from the Actions tab workflow_dispatch: # Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages permissions: contents: read pages: write id-token: write # Allow only one concurrent deployment, skipping runs queued between the run in-progress and latest queued. # However, do NOT cancel in-progress runs as we want to allow these production deployments to complete. concurrency: group: "pages" cancel-in-progress: false # Default to bash defaults: run: shell: bash jobs: # Build job build: runs-on: ubuntu-latest env: HUGO_VERSION: 0.121.0 steps: - name: Install Hugo CLI run: | wget -O ${{ runner.temp }}/hugo.deb https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_linux-amd64.deb \ && sudo dpkg -i ${{ runner.temp }}/hugo.deb - name: Install Dart Sass run: sudo snap install dart-sass - name: Checkout uses: actions/checkout@v4 with: submodules: recursive fetch-depth: 0 - name: Setup Pages id: pages uses: actions/configure-pages@v4 - name: Install Node.js dependencies run: "[[ -f package-lock.json || -f npm-shrinkwrap.json ]] && npm ci || true" - name: Build with Hugo env: # For maximum backward compatibility with Hugo modules HUGO_ENVIRONMENT: production HUGO_ENV: production run: | hugo \ --gc \ --minify \ --baseURL "${{ steps.pages.outputs.base_url }}/" - name: Upload artifact uses: actions/upload-pages-artifact@v2 with: path: ./public # Deployment job deploy: environment: name: github-pages url: ${{ steps.deployment.outputs.page_url }} runs-on: ubuntu-latest needs: build steps: - name: Deploy to GitHub Pages id: deployment uses: actions/deploy-pages@v3
```

然后重新 push 一次

```bash
git status 
git add .
git commit -m "add yml file"
git push
```

成功后会看到 github 上有一个工作流

![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217153426.png)

我看到有人自己开发工作流自定义的也挺不错, 如下

```yml
name: deploy

on:
    push:
    workflow_dispatch:
    schedule:
        # Runs everyday at 8:00 AM
        - cron: "0 0 * * *"

jobs:
    build:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout
              uses: actions/checkout@v2
              with:
                  submodules: true
                  fetch-depth: 0

            - name: Setup Hugo
              uses: peaceiris/actions-hugo@v2
              with:
                  hugo-version: "latest"

            - name: Build Web
              run: hugo

            - name: Deploy Web
              uses: peaceiris/actions-gh-pages@v3
              with:
                  PERSONAL_TOKEN: ${{ secrets.PERSONAL_TOKEN }}
                  EXTERNAL_REPOSITORY: xlmm/lucasloveann_blog.github.io
                  PUBLISH_BRANCH: master
                  PUBLISH_DIR: ./public
                  commit_message: ${{ github.event.head_commit.message }}
```

>但是步骤会多一些，需要建立一个 token
> `on` 表示 GitHub Action 触发条件，他设置了 `push`、`workflow_dispatch` 和 `schedule` 三个条件：
> `push`，当这个项目仓库发生推送动作后，执行 GitHub Action
> `workflow_dispatch`，可以在 GitHub 项目仓库的 Action 工具栏进行手动调用
> `schedule`，定时执行 GitHub Action，如我的设置为北京时间每天早上执行，主要是使用一些自动化统计 CI 来自动更新我博客的关于页面，如本周编码时间，影音记录等，如果你不需要定时功能，可以删除这个条件
> `jobs` 表示 GitHub Action 中的任务，我们设置了一个 `build` 任务，`runs-on` 表示 GitHub Action 运行环境，我们选择了 `ubuntu-latest`。我们的 `build` 任务包含了 `Checkout`、`Setup Hugo`、`Build Web` 和 `Deploy Web` 四个主要步骤，其中 `run` 是执行的命令，`uses` 是 GitHub Action 中的一个插件，我们使用了 `peaceiris/actions-hugo@v2` 和 `peaceiris/actions-gh-pages@v3` 这两个插件。其中 `Checkout` 步骤中 `with` 中配置 `submodules` 值为 `true` 可以同步博客源仓库的子模块，即我们的主题模块。
> 首先需要将上述 `deploy.yml` 中的 `EXTERNAL_REPOSITORY` 改为自己的 GitHub Pages 仓库，如我的设置为 `xlmm/lucasloveann_blog.github.io`。
> 因为我们需要从博客仓库推送到外部 GitHub Pages 仓库，需要特定权限，要在 GitHub 账户下 `Setting - Developer setting - Personal access tokens` 下创建一个 Token。

经过上述配置，我们已经实现了 Hugo 博客本地搭建及版本管理、GitHub Pages 部署网站发布，Hugp 主题管理及更新等功能，实现了完整的系统。现在每当我们本地通过熟悉的 Markdown 语法完成博客内容编辑后，只需要推送代码，等待几分钟，即可通过我们的自定义域名访问更新后的网站。

>后记：我曾经踩过的坑
>1. 直接拉取别人的库来做，无法更新，然后一直报错，所以我都直接克隆到自己的库存，后面自己维护
>2. .gitmodules 文件丢失，一直不知道在哪解决，后面只能重建。
>3. 创建仓库的时候，先创建了 readme，然后忘记拉取到本地再同步，就同步不了。后面我直接忽略掉这个git pull origin main --allow-unrelated-histories

如这篇文章会以这样状态出现
![image.png|300](https://lucas-1317635493.cos.ap-nanjing.myqcloud.com/obsidian%E5%9B%BE%E5%BA%8A/20231217162558.png)

以上，就是我要分享的。