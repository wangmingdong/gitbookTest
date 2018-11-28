 ## 一个Gitbook的小例子

### 安装 Node.js

GitBook 是基于 Node.js 的命令行工具，下载安装 [Node.js](https://link.jianshu.com/?t=http://nodejs.org/)。

检测安装是否成功：

``` bash
$ node -v
v10.5.0
```

### Gitbook 安装

Gitbook 是用 npm 安装的，命令行：

``` bash
$ npm install -g gitbook-cli
```

检测安装是否成功：

``` bash
$ gitbook -V
CLI version: 2.3.2
GitBook version: 3.2.3
```

更新最新版本：

``` bash
$ gitbook update
```

卸载：

``` bash
$ npm uninstall -g gitbook
```

### GitBook Editor

官方编辑器，下载 https://www.gitbook.com/editor ，大概如图：

![编辑器](http://7q5c2h.com1.z0.glb.clouddn.com/GitBook1.png?imageView2/0/format/png/q/75%7Cwatermark/2/text/5ZC05bCP6b6Z5ZCM5a24/font/5a6L5L2T/fontsize/1200/fill/IzIxOTZGMw==/dissolve/100/gravity/SouthEast/dx/10/dy/10%7Cimageslim)

关于 GitBook Editor 怎么使用和注册 GitBook 等步骤较简单，这里略。

### 插件

#### book.json

新建一个 book.json 文件，可以配置网站信息、在 ``plugins`` 和 ``pluginsConfig`` 字段添加插件等。

插件命名方式为：

``gitbook-plugin-X``: 插件；

``gitbook-theme-X``: 主题。

可以在 [npmjs](https://link.jianshu.com/?t=https://www.npmjs.com/) 或 [GitBook插件](https://link.jianshu.com/?t=https://plugins.gitbook.com/)  直接搜索插件或者主题。
book.json 内容大概如下：

``` js
{
    "gitbook": "3.2.3",
    "title": "Book",
    "description": "http://weqianduan.com/",
    "author": "wangmingdong",
    "language": "zh-hans",
    "links": {
    "sidebar": {
    
        }
    },
    "plugins": ["github",
        "donate",
        "splitter",
        "anchor-navigation-ex",
        "-sharing",
        "sharing-plus",
        "-highlight",
        "prism"
    ],
    "pluginsConfig": {
        "sharing": {
            "douban": false,
            "facebook": false,
            "google": false,
            "hatenaBookmark": false,
            "instapaper": false,
            "line": false,
            "linkedin": false,
            "messenger": false,
            "pocket": false,
            "qq": false,
            "qzone": false,
            "stumbleupon": false,
            "twitter": false,
            "viber": false,
            "vk": false,
            "weibo": false,
            "whatsapp": false,
            "all": [
                "weibo","qq","qzone","google","douban"
            ]
        },
        "github": {
            "url": "https://github.com/wangmingdong"
        },
        "donate": {
            "wechat": "http://static.weqianduan.com/wechat-pay.jpeg",
            "title": "",
            "button": "赏",
            "wechatText": "微信打赏"
        },
        "anchor-navigation-ex": {
        "associatedWithSummary":false,
        "showLevel":true,
        "multipleH1": true,
        "mode": "float",
        
        "pageTop": {
            "showLevelIcon": false,
            "level1Icon": "fa fa-hand-o-right",
            "level2Icon": "fa fa-hand-o-right",
            "level3Icon": "fa fa-hand-o-right"
            }
        },
        "theme-default": {
            "showLevel": true
        },
        "fontsettings": {
                "theme": "white",
                "family": "sans",
                "size": 2
            },
        "prism": {
            "css": [
                    "prismjs/themes/prism-tomorrow.css"
                ]
            }
        }
    
    }
```

说明：

* github：添加 GitHub 图标；
* Donate：添加赞赏按钮；
* splitter：使侧边栏的宽度可以自由调节；
* anchor-navigation-ex：添加Toc到侧边悬浮导航以及回到顶部按钮；
* theme-default：将 showLevel 设为 true， 就可以显示标题前面的数字索引，默认不显示。

#### 安装插件

``` bash
$ gitbook install ./
```

不要忘记这步，根目录 node_modules 文件下能看到安装那些插件。

或单独安装插件:

``` bash
$ npm install gitbook-plugin-anchor-navigation-ex --save
```

#### 默认插件

GitBook 默认带有5个插件：

* highlight

* search

* sharing

* fontsettings

* livereload

如果要去除自带的插件，可以在插件名称前面加 -：

``` bash
"plugins": [
"-search"
]
```

如果想配置直接在 pluginsConfig 配置。

### GitBook 输出

#### gitbook init

首先，创建如下目录结构：

``` bash
$ tree book/
book/
├── README.md
└── SUMMARY.md

0 directories, 2 files
```

README.md 和 SUMMARY.md 是两个必须文件，README.md 是对书籍的简单介绍：

``` bash
$ cat book/README.md 
# README

This is a book powered by [GitBook](https://github.com/GitbookIO/gitbook).
```
SUMMARY.md 是书籍的目录结构。内容如下：

``` bash
$ cat book/SUMMARY.md 
# SUMMARY

# Summary

* [介绍](README.md)
* [词集](speech/README.md)
    * [东坡词](speech/dongPo.md)
    * [东堂词](speech/dongTang.md)
* [诗集](poetry/README.md)
    * [万首唐人绝句](poetry/wangShouTangRen.md)
    * [三体唐诗](poetry/sanTi.md)
```
创建了这两个文件后，使用 gitbook init，它会为我们创建 SUMMARY.md 中的目录结构。

``` bash
info: create speech/README.md
info: create speech/dongPo.md
info: create speech/dongTang.md
info: create poetry/README.md
info: create poetry/wangShouTangRen.md
info: create poetry/sanTi.md
info: create SUMMARY.md
info: initialization is finished
```


#### 本地预览

进入你的 book 书籍目录，输入命令行：

``` bash
$ gitbook serve
```

然后浏览器打开 http://localhost:4000 就能预览了，control + c 停止。

输出静态网站

``` bash
$ gitbook build
```

以上都会在书籍目录生成 _book，前者能实时预览。