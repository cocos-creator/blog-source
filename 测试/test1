
---
title: fhuewy
author: langker

---


## Fireball 官网

本文档介绍了如何维护和更新 Fireball 官网的内容，并在此基础上进行更多功能开发。

### 技术结构

Fireball 官网采用了以下 framework 和 library：
- [Meteor](https://www.meteor.com/) 作为完整的 webapp 驱动引擎，主要用来实现用户数据库的处理和用户信息页面的动态渲染。
- [MailChimp API](https://github.com/gomfunkel/node-mailchimp) MailChimp 邮件管理系统的 Nodejs API wrapper
- [Fibers](https://github.com/laverdet/node-fibers) 在 synchronous 环境中实现各种 async 回调功能。

其中静态页面使用 [Webflow](https://webflow.com/) 来生成，之后需要处理成 template 的形式，才能在 Meteor 中正确的渲染。

### 准备工作

Meteor 开发环境必须是 Mac。按照下面的步骤来完成配置。

#### 安装 git

http://www.git-scm.com/
请使用 git v1.9.5 以上的版本。

#### 安装 Meteor

```bash
 curl https://install.meteor.com | /bin/sh
```

#### 安装 NodeJS

http://nodejs.org/
这一步不用详细介绍，目前 Fireball 网站是在 Node v0.10.35环境下开发和部署的。

### 下载和运行

首先下载网站 repo 并切换到开发分支：

```bash
git clone git@github.com:fireball-x/fireball-site.git
cd fireball-site
git fetch --all
git checkout develop
```

确保你进入了网站项目文件夹，运行下面的命令在本地运行网站：
```bash
meteor
```

第一次运行时，会下载 Meteor 项目依赖的 npm 库，最好在 vpn 的环境下进行第一次运行。

之后就可以在浏览器中访问`localhost:3000`来预览网站了。

可以参考[Meteor文档](http://docs.meteor.com/)以获得更多信息。

### 项目结构说明

<pre>
fireball-site
 |--.meteor （存放 Meteor 的 package，以及本地运行时 build 出的临时文件）
 |--client （客户端使用的 html 模板、前端 js 程序）
 |   |--compatibility （第三方动态加载的 js 库）
 |   |--styles (所有 css 文件，也可以使用 stylus、less 等预编译 css 语言）
 |   |--templates（所有页面渲染相关的模板和功能程序）
 |       |--helpers（存放全局性质的 helper 功能）
 |       |--includes（存放 header、footer 等页面组成部分，或者叫 partial）
 |       |--users（用户信息相关的模板和 helper 脚本）
 |       |--hello.html（fireball 首页 html 内容）
 |       |--layout.html（所有页面都使用的结构模板，包括导航栏、内容、页脚等）      
 |
 |--deploy（部署相关的脚本配置）
 |--lib（前后端通讯用的模块，如路由、用户数据操作程序等，放在这个文件夹下的内容会在运行时优先执行）
 |--packages（自定义的 Meteor 包，我们要使用的原生 npm 包就会被下载到这个文件夹下）
 |--public（所有不需要编译的静态文件和资源，比如纯静态 html、图片、字体等等）
 |   |--fonts（存放 icon font 的字体和 css 定义）
 |   |--images（网站使用的所有图片文件）
 |
 |--server（只在服务器端运行的程序，包括数据库操作，后端 nodejs 库调用等等） 
 |
 |--package.json （需要使用的原生 npm 包要定义在这里面，然后运行 meteor 时就会进行下载和更新）
</pre>

### Spacebars Template 入门

Meteor 使用 [Spacebars](https://github.com/meteor/meteor/blob/devel/packages/spacebars/README.md) 作为他的模板渲染系统。Spacebars 使用类似[Handlebars](http://handlebarsjs.com/)的语法，但是整合了 html5 的 template 和 Meteor 中的 template helpers 功能，让模板开发更为方便。

首先阅读[Spacebars Readme](https://github.com/meteor/meteor/blob/devel/packages/spacebars/README.md)来了解基本语法。
重点需要注意的是以下两种语法：

```bash
{{> myTemplate}}
```
相当于在该行插入模板中的 html 内容：
```html
<template name="myTemplate">
   <!-- my html content -->
</template>
```

插入的内容不包括外围的`<template>`标签部分。

而 myTemplate 模板中出现的
```bash
{{myHelperFunction}}
```
会调用
```javascript
Template.myTemplate.helpers({
    myHelperFunction: function() {
        return something;
    }
});
```

并获得其中 function 的返回值。

### 静态页面融合和维护

掌握了 Spacebars 的基本原理，就可以开始合并 Webflow 生成的静态网页了。

- 首先获取 Webflow 生成的静态网页项目`fireball-web.webflow`
- 将`css`目录下的`fireball-web.webflow.css`和`webflow.css`放进 fireball 项目中的`client/styles`目录下。
- 将`images`目录下的所有文件放进 fireball 项目中的`public/images`目录下。

然后就可以开始合并 html 文件了。

#### 合并静态页面

纯静态页面内容中没有 spacebars 的语法，所以只要将页面 body 部分套上 template 声明就可以了。具体可以参考 fireball 项目中`client/templates/hello.html`首页的做法。

#### 修复图片链接

webflow 默认生成的 html 中，所有图片引用地址都是以 `src="images/xxx"` 打头的，这样的地址在通过路由进行跳转时可能会无法找到 `images` 文件夹，所以合并后的静态页面所有图片引用都应该改成 `src="/images/xxx"`，这样才能保证找到并使用网站唯一的`images`文件夹。


## 部署说明

网站部署在阿里云服务器上，采用了以下的结构：
<pre>
/
|--opt
|  |--fbsite (经过 meteor build 打包后的 nodejs app，运行在 http://127.0.0.1:3000)
|--etc
   |--nginx
      |--sites-available
         |--fireball-x.com.conf (nginx 反向代理设置文件）
</pre>

### 部署流程

安装[Meteor-Up](https://github.com/arunoda/meteor-up):
```bash
npm install -g nantas/meteor-up
```
（我们自己的 fork 版使用了国内适用的 npm 镜像文件，部署成功率更高）

进入`deploy`文件夹，执行以下命令：
```bash
mup setup
mup deploy
```

更多信息请查看：

https://github.com/arunoda/meteor-up

