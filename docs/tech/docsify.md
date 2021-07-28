## 关于Docsify

Docsify 是一个 **运行时** 的静态网站构建工具，它不会把 markdown 文件转换成 html 文件，不需要启动，不需要打包，只需要一个 index.html 和一堆 markdown 文件就可以完成你的静态网站搭建，就是这么简单。

**LINKS：**https://docsify.js.org

## 准备工作

#### 1、git环境+github账号

**教程：**[Git实用教程（二） | Git简介及安装详解](https://zhuanlan.zhihu.com/p/87679636)

**官网注册github的账号：**[Github](https://github.com/)

### 2、node环境

docsify框架需要有node环境的支持,在[**node.js**](https://nodejs.org)的官网下载安装包，此处下载Windows版本的，点下一步一路安装下去，配置下环境变量即可。

**教程：**[npm安装教程 ](https://www.cnblogs.com/goldlong/p/8027997.html)

### 3、步骤

- 搭建环境、注册账号
- 使用docsify命令生成文档站点
- 配置docsify
- 部署站点

## 正式开始

### 1、按照前面教程搭建所需环境和注册账号

这里就再不写了，前面的教程都很详细了。

### 2、使用docsify命令生成文档站点

#### 安装docsify-cli 工具

推荐安装 docsify-cli 工具，可以方便创建及本地预览文档网站。

```bash
npm i docsify-cli -g
```

因为我们已经安装了node环境，所以直接打开CMD窗口执行上面的命令就好了。

#### 初始化一个项目

然后我们选择一个目录，作为我们的站点目录。

这里我在E盘下新建了一个niegedoc的目录

**WIN+R**输入`CMD`执行如下命令：

```shell
e:
cd niegedoc
docsify init ./docs
```

执行完成后，会在niegedoc目录下生成一个docs目录及其下的三个文件

- index.html 入口文件
- README.md 会做为主页内容渲染
- .nojekyll 用于阻止 GitHub Pages 会忽略掉下划线开头的文件

这是目录结构就是这样的

```markdown
E:
└───niegedoc
    │
    └───docs
        │   .nojekyll
        │   index.html
        │   README.md
```



#### 启动项目，预览效果

到这里，就可以启动项目，然后看下效果了。 使用下面命令启动项目：

```bash
docsify serve docs
```

在浏览器输入：http://localhost:3000   就可以看到效果了。

### 配置docsify

这里贴一个完整配置文件index.html，直接复制代码到你的index.html文件里，按照注释修改相应配置就可以了。

```html
<!-->index.html<-->
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>docsify website sample</title>
  <link rel="shortcut icon" href="./favicon.ico" type="image/x-icon">
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="description" content="Description">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, minimum-scale=1.0">
  <!-- vue主题样式 -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
  <!-- 暗黑主题插件样式 -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/dist/style.min.css"
    title="docsify-darklight-theme" type="text/css" />
</head>

<body>
  <div id="app">loading...</div>
  <!-- 在github上编辑插件 -->
  <script src="//cdn.jsdelivr.net/npm/docsify-edit-on-github"></script>
  <script>
    window.$docsify = {
      basePath: '/', // 资源相对路径
      name: 'docsify website sample', // 文档标题，会显示在侧边栏顶部
      nameLink: '/', // 点击文档标题后的跳转地址
      repo: 'lexmin0412/docsify-website-sample', // 有repo属性则右上角会展示github图标，点击可进入
      loadSidebar: true, // 加载侧边栏
      externalLinkTarget: '_blank', // 外部链接的打开方式，默认_blank
      cornerExternalLinkTarget: '_blank', // 右上角链接的打开方式。默认为 _blank
      routerMode: 'hash', // 路由方式 默认hash
      coverpage: true, // 展示封面
      notFoundPage: true, // 在找不到指定页面时加载_404.md
      auto2top: true, // 切换页面后是否自动跳转到页面顶部
      search: { // 搜索插件配置
        paths: 'auto',
        placeholder: '🔍 搜索',
        noData: '😞 没有结果!'
      },
      count: { // 字数统计插件配置
        countable: true,
        fontsize: '0.9em',
        color: 'rgb(90,90,90)',
        language: 'chinese'
      },
      pagination: { // 分页插件配置
        previousText: '上一章节',
        nextText: '下一章节',
        crossChapter: true,
      },
      plugins: [
        EditOnGithubPlugin.create(
          'https://github.com/lexmin0412/docsify-website-sample/blob/master/docs/',
          null,
          function ( file ) {
            if ( file.indexOf( 'en' ) === -1 ) {
              return '在 GitHub 上编辑'
            } else {
              return 'Edit on Github'
            }
          }
        )
      ],
      themeColor: "#42b983", // 暗黑模式主题色
      darklightTheme: {
        siteFont: "PT Sans",
        defaultTheme: 'dark',
        codeFontFamily: 'Roboto Mono, Monaco, courier, monospace',
        bodyFontSize: '17px',
        dark: {
          accent: '#42b983',
          toogleBackground: '#ffffff',
          background: '#091a28',
          textColor: '#b4b4b4',
          codeTextColor: '#ffffff',
          codeBackgroudColor: '#0e2233',
          borderColor: '#0d2538',
          blockQuoteColour: '#858585',
          highlightColor: '#d22778',
          sidebarSublink: '#b4b4b4',
          codeTypeColor: '#ffffff',
          coverBackground: 'linear-gradient(to left bottom, hsl(118, 100%, 85%) 0%,hsl(181, 100%, 85%) 100%)',
          toogleImage: 'url(https://cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/icons/sun.svg)'
        },
        light: {
          accent: '#42b983',
          toogleBackground: '#091a28',
          background: '#ffffff',
          textColor: '#34495e',
          codeTextColor: '#525252',
          codeBackgroudColor: '#f8f8f8',
          borderColor: 'rgba(0, 0, 0, 0.07)',
          blockQuoteColor: '#858585',
          highlightColor: '#d22778',
          sidebarSublink: '#b4b4b4',
          codeTypeColor: '#091a28',
          coverBackground: 'linear-gradient(to left bottom, hsl(118, 100%, 85%) 0%,hsl(181, 100%, 85%) 100%)',
          toogleImage: 'url(https://cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/icons/moon.svg)'
        }
      }
    }
  </script>
</body>

<script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
<!--全局搜索插件-->
<script src="//unpkg.com/docsify-count/dist/countable.js"></script>
<!--字数统计插件-->
<script src="//cdn.jsdelivr.net/npm/docsify-copy-code"></script>
<!--代码段复制插件-->
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/zoom-image.min.js"></script>
<!--图片缩放插件-->
<script src="//unpkg.com/docsify-pagination/dist/docsify-pagination.min.js"></script>
<!-- 阅读进度条插件 -->
<script src="//cdn.jsdelivr.net/npm/docsify-darklight-theme@latest/dist/index.min.js"></script>
<!-- 暗黑主题切换插件 -->

</html>
```

下面就可以添加相应的.MD文件就OK了。

- _coverpage.md    封面配置文件
- _sidebar.md         侧边栏配置文件（也就是目录文件）
- _navbar.md          菜单栏配置文件

这时我的目录结构就是这样了

```markdown
E:
└───niegedoc
    │
    └───docs
        │   .nojekyll
        │   index.html
        │   README.md
        │   _coverpage.md
        │   _sidebar.md
        │   _navbar.md
        │   ...      //其他.md文件（文章文件可以放在这里也可以放到分目录下）
        │
        └─────────────也可以在这里建立各个分类目录存放.md文件
```

到这里docsify本地搭建及配置就完成了，后面只要不断的写文章并修改_sidebar.md目录文件就好。

## 部署docsify网站

这里我主要记录下部署到Github和Vercel。

### 一、部署到Github

- 登录到Github网站，或者直接[点击这里](https://github.com/new)新建一个公开项目。
- 