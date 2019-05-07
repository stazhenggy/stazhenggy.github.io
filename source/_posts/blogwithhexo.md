---
title: Windows:利用Hexo搭建个人博客
date: 2019-02-27
tags: hexo
categories: 
- tools
- hexo
top: false
mathjax: true
---

本文介绍利用Hexo搭建个人博客，并将该博客部署至git。以及对于Hexo主题，页面等的设置方法。

<!--more-->

## 需要安装git和nodejs
+ [git](https://gitforwindows.org/)
+ [nodejs](https://nodejs.org/en/download/) 

安装完成后，<span id="inline-green">git bash</span>中使用以下命令检查是否安装成功。
```bash
node -v 
npm -v
```

git安装成功后，就可以使用<span id="inline-green">git bash</span>敲命令了，不再用windows<span id="inline-green">cmd</span>了。

## 安装hexo
在安装好**git**和**nodejs**后，继续安装**hexo**。 
+ 创建一个文件夹，如命名为<span id="inline-purple">blog</span>
+ <span id="inline-green">git bash</span>中, `cd`到这个文件夹下(或在这个文件夹下右键git bash打开)
+ 输入`npm install -g hexo-cli` 安装 
+ 使用`hexo -v`检查是否安装成功

至此，hexo安装结束

## 初始化hexo
使用以下命令初始化**hexo**。`hexo init [subdirname]`

## 新建博客文章(post) 
使用以下命令新建博客文章。
```bash
hexo new post_name
hexo n post_name
```
之后就可以在<span id="inline-purple">.md</span>中尽情写文章了。

## 生成静态网页
文章写完后，使用以下命令生成静态网页。
```bash 
hexo generate 
hexo g
```

## 启动预览服务
使用以下命令，本地预览。<span id="inline-green">localhost:4000</span>中打开。
```bash 
hexo server 
hexo s
```

或本地测试 
```bash 
hexo debug
```

## 发布网站

### 站点配置文件中部署blog位置
<span id="inline-purple">blog</span>文件夹下 `_config.yml`为<span id="inline-purple">站点配置文件</span>。打开该文件，新增部署语句如下：
```bash
deploy:
	type: git 
	repo: https://github.com/username/username.github.io.git
	branch: master
```

### 安装git部署插件
```bash 
npm install hexo-deployer-git --save
```

### 部署
```bash 
hexo deploy
hexo d 
```

至此，blog上线。 如果是内容重新更新，则在`deploy`之前先`clean`。 

```bash
hexo clean
```

## Hexo个性化设置

### 更换theme

`cd`到<span id="inline-purple">blog</span>文件夹，<span id="inline-green">git bash</span>中继续输入
```bash 
git clone https://github.com/iissnan/hexo-theme-next themes/next
```
找到<span id="inline-purple">站点配置文件</span>中的`theme: landscape` 修改为`theme: next` 

### 导航栏设置

{%btn https://hexo.io/zh-cn/docs/front-matter.html, 分类和标签设置, hand-o-right fa-fw %}

#### 添加"分类"
+ `cd` 到<span id="inline-purple">blog</span>下，执行命令`hexo new page categories`
+ 成功后会提示`INFO Created: d:/blog/source/tags/index.md`
+ 找到<span id="inline-purple">index.md</span>,添加`type: "tags"`
+ 注意<span id="inline-purple">主题配置文件</span>配置以下内容。打开首页`categories`

```bash
menu:
  home: / || home
  about: /about/ || user
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat

```

+ 打开需要添加标签的文章，为其添加categories属性。

{%note info%}
下方的`categories:tools`表示添加这篇文章到"tools"这个分类下。注意：hexo中一篇文章只能属于一个分类，也就是说如果在"-tools"下方添加"-xxx",hexo不会产生两个分类，而是把分类嵌套，即该文章属于"-tools"下的"-xxx"分类
{%endnote%}

```
---
title: 利用Hexo搭建个人博客
date: 
categories:
- web 前端
- xxx
---
```
至此，成功给文章添加分类，点击首页的"分类"可以看到该分类下的所有文章。

#### 添加"标签"

+ `cd` 到<span id="inline-purple">blog</span>下，执行命令`hexo new page tags`
+ 成功后会提示`INFO Created: d:/blog/source/categories/index.md`
+ 找到<span id="inline-purple">index.md</span>, 添加`type: "categories"`

打开需要添加标签的文章，为其添加tags属性。下方的`tags: blog` `-hexo` 就是这篇文章的标签了

``` 
---
title: 利用Hexo搭建个人博客
date: 
categories:
- tools
tags:
- blog 
- hexo 
---
```
至此，成功给文章添加标签，点击首页的"标签"可以看到该标签下的所有文章。

#### 添加"about"并添加想说的话

+ `cd` 到<span id="inline-purple">blog</span>下，执行命令`hexo new page about`
+ 成功后会提示`INFO Created: d:/blog/source/categories/index.md`
+ 找到<span id="inline-purple">index.md</span>,写上你想说的话

至此，成功给文章添加标签，点击首页的"标签"可以看到该标签下的所有文章。

### 添加搜索功能：LocalSearch搜索

安装`hexo-generator-searchdb`. `cd`到<span id="inline-purple">blog</span>下，执行以下命令`npm install hexo-generator-searchdb --save`

编辑<span id="inline-purple">站点配置文件</span>，新增以下内容到任意位置

```
search:
  path: search.xml
  field: post
  format: html 
  limit: 10000
```
编辑<span id="inline-purple">主题配置文件</span>，启用本地搜索功能

```
# local
local_search:
  enable: ture
```

### 首页设置

#### 不显示全文

Hexo的Next主题默认首页显示每篇文章的全文内容，下面将其修改为只显示部分内容。

**方法1: 修改<span id="inline-purple">主题配置文件</span>**

<span id="inline-purple">主题配置文件</span>，找到以下代码：

```
# Automatically Excerpft. Not recommend.
# Please use <!-- more --> in the post to control excerpt accurately.
auto_excerpt:
  enable: false
  length: 150

```
把`enable`的`false`改成`true`即可。`length`设定文章预览的文本长度。 修改后重启hexo即可。

**方法2: 在文章内容后加上`<!--more-->`**

在<span id="inline-purple">.md</span>文章内容后加上`<!--more-->`,首页和列表页显示的文章内容就是`<!--more-->`之前的文字，之后的不会显示

{%note info%}
第一种会格式化文章的样式，直接把文章挤在一起显示，最后会有`...`。第二种不会有
{%endnote%}

### 文章设置

#### 置顶

安装node插件

```bash 
npm uninstall hexo-generator-index --save 
npm install hexo-generator-index-pin-top --save
```
在需要置顶的文章的`Front-matter`中加上`top:true`即可。 也可以指定`top: 数字`。 数字越大排序越靠前。

```
title: 
date:
tags:
categories:
description:
top: true
```
#### 显示版权信息

<span id="inline-purple">主题配置文件</span>，修改以下部分：

```
# Declare license on posts
post_copyright:
  enable: false
  license: CC BY-NC-SA 3.0
  license_url: https://creativecommons.org/licenses/by-nc-sa/3.0/

```
将其中的`enable: false` 改为`enable: true`。 同时，在<span id = "inline-purple">站点配置文件中</span>，修改`URL`为自己的站点的域名地址。

#### 访问统计功能

添加博客的访问量。`不蒜子统计`显示文章的访客数，浏览量等信息

<span id="inline-purple">主题配置文件</span>, 找到`busuanzi_count`，将`enable: false`改为`enable: true`

```
# Show PV/UV of the website/page with busuanzi.
# Get more information on http://ibruce.info/2015/04/04/busuanzi/
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: 访客数 <i class="fa fa-user"></i>
  site_uv_footer: 人次
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: 浏览量 <i class="fa fa-eye"></i>
  site_pv_footer: 次
  # custom pv span for one page only
  page_pv: true
  page_pv_header: 阅读量 <i class="fa fa-file-o"></i>
  page_pv_footer: 次
```
+ 当`enable: true`时，代表开启全局开关；
+ 当`site_uv: true`时，代表页面底部显示站点UV
+ 当`site_pv: true`时，代表页面底部显示站点PV
+ 当`page_uv: true`时，代表文章页面标题下显示该页面的PV

#### 显示文章更新时间

<span id="inline-purple">主题配置文件</span>，`post_meta`部分:

```
# Post meta display settings
post_meta:
  item_text: true
  created_at: true
  updated_at: false
  categories: true

```
将`updated_at: false`改为`updated_at: true`即可。

### 网站底部

#### 去掉底部hexo强力驱动

<span id="inline-purple">主题配置文件</span>，修改

```
  # If not defined, will be used `author` from Hexo main config.
  copyright:
  # -------------------------------------------------------------
  # Hexo link (Powered by Hexo).
  powered: false

```
#### 添加博客运行时间

<span id="inline-purple">themes/next/layout/_partials/footer.swig</span>

```
<span class="footer__copyright">
<div><span id="span_dt_dt"> </span>
<script language="javascript">
function show_date_time(){
window.setTimeout("show_date_time()", 1000);
BirthDay=new Date("8/25/2016 00:00:00");//这个日期是可以修改的
today=new Date();
timeold=(today.getTime()-BirthDay.getTime());//其实仅仅改了这里
sectimeold=timeold/1000
secondsold=Math.floor(sectimeold);
msPerDay=24*60*60*1000
e_daysold=timeold/msPerDay
daysold=Math.floor(e_daysold);
e_hrsold=(e_daysold-daysold)*24;
hrsold=Math.floor(e_hrsold);
e_minsold=(e_hrsold-hrsold)*60;
minsold=Math.floor((e_hrsold-hrsold)*60);
seconds=Math.floor((e_minsold-minsold)*60);
span_dt_dt.innerHTML="博客已运行"+daysold+"天"+hrsold+"小时"+minsold+"分"+seconds+"秒 🐼 ";
}
show_date_time();
</script></div>
</span>

```

#### 底部的心跳动

<span id="inline-purple">主题配置文件</span>
```
footer:
  icon: heart
```

<span id="inline-purple">~/blog/themes/next/layout/_partials/footer.swig</span>,编辑
```
<span class="with-love" id="heart">
```

<span id="inline-purple">~/blog/themes/next/source/css/_custom/custom.styl</span>, 添加
```
// 自定义页脚跳动的心样式
@keyframes heartAnimate {
    0%,100%{transform:scale(1);}
    10%,30%{transform:scale(0.9);}
    20%,40%,60%,80%{transform:scale(1.1);}
    50%,70%{transform:scale(1.1);}
}
#heart {
    animation: heartAnimate 1.33s ease-in-out infinite;
}
.with-love {
    color: rgb(255, 113, 168);
}
```
### 代码块

#### 代码块样式

```
```[language][title][url][link-text]
code
```
<div class="note info">
  <p>说明
+ [language] 是代码语言的名称，用来设置代码块颜色高亮，非必须；
+ [title] 是顶部左边的说明，非必须；
+ [url] 是顶部右边的超链接地址，非必须；
+ [link text] 如它的字面意思，超链接的名称，非必须。
</div>

```python Python https://docs.python.org/3/library/stdtypes.html#string-methods Python
print("Hello,world!")
```

#### 设置代码高亮主题

<span id="inline-purple">主题配置文件</span>，修改`highlight_theme`

```
# Code Highlight theme
# Available value: normal | night | night eighties | night blue | night bright
# https://github.com/chriskempson/tomorrow-theme
highlight_theme: night
```
## Next各种样式

### 文本块内容样式

{%note default%}
#### note default
default 
{%endnote%}

{%note info%}
#### note info
info
{%endnote%}

{%note success%}
#### note success
success
{%endnote%}

{%note warning%}
#### note warning
warnig
{%endnote%}

{%note danger%}
#### note danger
danger
{%endnote%}

<div class="note primary">
  <h4>note primary</h4>
  <p>使用html标签写法primary</p>
</div>

```
{%note default%}
### note default
default 
{%endnote%}

<div class="note primary">
  <h4>note primary</h4>
  <p>使用html标签写法primary</p>
</div>
```

如果想用包含图标的，到<span id="inline-purple">主题配置文件</span>，修改为`icons: true`

```
# Note tag (bs-callout).
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: simple
  icons: true
  border_radius: 3
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 0
```

### 文字内容样式

{%label @复道%}{%label primary@行空%}, {%label default@不霁%}{%label success@何虹%}。 
{%label info@长桥%}{%label danger@卧波%},{%label warning@未云%}<mark>何龙</mark>。

```
{%label @复道%}{%label primary@行空%}, {%label default@不霁%}{%label success@何虹%}。
```

### 文字增加背景色块

打开<span id="inline-purple">themes/next/source/css/_custom</span>下<span id="inline-purple">custom.styl</span>文件,添加属性样式

```
// 颜色块-红
span#inline-red {
display:inline;
padding:.2em .6em .3em;
font-size:80%;
font-weight:bold;
line-height:1;
color:#fff;
text-align:center;
white-space:nowrap;
vertical-align:baseline;
border-radius:0;
background-color: #E34018;
}
// 颜色块-黄
span#inline-yellow {
display:inline;
padding:.2em .6em .3em;
font-size:80%;
font-weight:bold;
line-height:1;
color:#fff;
text-align:center;
white-space:nowrap;
vertical-align:baseline;
border-radius:0;
background-color: #f0ad4e;
}
// 颜色块-绿
span#inline-green {
display:inline;
padding:.2em .6em .3em;
font-size:80%;
font-weight:bold;
line-height:1;
color:#fff;
text-align:center;
white-space:nowrap;
vertical-align:baseline;
border-radius:0;
background-color: #5cb85c;
}
// 颜色块-蓝
span#inline-blue {
display:inline;
padding:.2em .6em .3em;
font-size:80%;
font-weight:bold;
line-height:1;
color:#fff;
text-align:center;
white-space:nowrap;
vertical-align:baseline;
border-radius:0;
background-color: #2780e3;
}
// 颜色块-紫
span#inline-purple {
display:inline;
padding:.2em .6em .3em;
font-size:80%;
font-weight:bold;
line-height:1;
color:#fff;
text-align:center;
white-space:nowrap;
vertical-align:baseline;
border-radius:0;
background-color: #9954bb;
}

```

在你需要编辑的文章地方。放置如下代码：
```
<span id="inline-blue"> 站点配置文件 </span>
<span id="inline-purple"> 主题配置文件 </span>
<span id="inline-yellow"> 站点配置文件 </span>
<span id="inline-green"> 主题配置文件 </span>

```

### 改变文字颜色

使用html语法直接写即可。

<font color="#FF0000"> 我可以设置这一句的颜色哈哈 </font> 

`<font color="#FF0000"> 我可以设置这一句的颜色哈哈 </font> `

<font size=6> 我还可以设置这一句的大小嘻嘻 </font> 

`<font size=6> 我还可以设置这一句的大小嘻嘻 </font> `

<font size=5 color="#FF0000"> 我甚至可以设置这一句的颜色和大小呵呵</font> 

`<font size=5 color="#FF0000"> 我甚至可以设置这一句的颜色和大小呵呵</font>`

### 文字居中

`<center>这一行需要居中</center>`

### tabs标签

{% tabs tab, 1 %}
<!-- tab ID3 -->
**这是选项卡 1**
<!-- endtab -->
<!-- tab C4.5-->
**这是选项卡 2**
<!-- endtab -->
<!-- tab C5.0-->
**这是选项卡 3**
<!-- endtab -->
{% endtabs %}

```
{% tabs tab, 1 %} 
<!-- tab ID3 -->
**这是选项卡 1**
<!-- endtab -->
<!-- tab C4.5-->
**这是选项卡 2**
<!-- endtab -->
<!-- tab C5.0-->
**这是选项卡 3**
<!-- endtab -->
{% endtabs %}
```
### 按钮

**Botton**
{% btn https://blog.csdn.net/u011236348/article/details/88146947, NexT进度条加载,,title %}

```
{% btn url,test_tile,,title %}
```

**Botton with Icon**
{% btn http://theme-next.iissnan.com/theme-settings.html, NexT主题设置,hand-o-right %}

```
{%btn url,showlabel,hand-o-right%}
```

**Botton with Fix-width** 
{% btn https://www.jianshu.com/p/3a05351a37dc, NexT个性化设置, hand-o-right fa-fw %}

```
{%btn url, Next样式, hand-o-right fa-fw %}
```

**Center** 
<div class="text-center"><span>{% btn https://www.google.com,,google %}{% btn url,,edge %}{% btn url,, chrome %}</span>
<span>{% btn url,, terminal %}{% btn url,,diamond fa-rotate-270 %}</span></div>

``` 
<div class="text-center"><span>{% btn url,,google%}{%btn url,,edge %}{% btn url,,chrome %}</span>
<span>{% btn url,,terminal %}{% btn url,,diamond fa-rotate-270 %}</span></div>
```

## 酷绚效果

### 点击发射桃心效果

+ <span id="inline-purple">/themes/next/source/js/src</span>下新建文件<span id="inline-purple">clicklove.js</span>。 把下面代码贴到该文件中。

```
! function (e, t, a) {
  function n() {
    c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"), o(), r()
  }

  function r() {
    for (var e = 0; e < d.length; e++) d[e].alpha <= 0 ? (t.body.removeChild(d[e].el), d.splice(e, 1)) : (d[e].y--, d[e].scale += .004, d[e].alpha -= .013, d[e].el.style.cssText = "left:" + d[e].x + "px;top:" + d[e].y + "px;opacity:" + d[e].alpha + ";transform:scale(" + d[e].scale + "," + d[e].scale + ") rotate(45deg);background:" + d[e].color + ";z-index:99999");
    requestAnimationFrame(r)
  }

  function o() {
    var t = "function" == typeof e.onclick && e.onclick;
    e.onclick = function (e) {
      t && t(), i(e)
    }
  }

  function i(e) {
    var a = t.createElement("div");
    a.className = "heart", d.push({
      el: a,
      x: e.clientX - 5,
      y: e.clientY - 5,
      scale: 1,
      alpha: 1,
      color: s()
    }), t.body.appendChild(a)
  }

  function c(e) {
    var a = t.createElement("style");
    a.type = "text/css";
    try {
      a.appendChild(t.createTextNode(e))
    } catch (t) {
      a.styleSheet.cssText = e
    }
    t.getElementsByTagName("head")[0].appendChild(a)
  }

  function s() {
    return "rgb(" + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + "," + ~~(255 * Math.random()) + ")"
  }
  var d = [];
  e.requestAnimationFrame = function () {
    return e.requestAnimationFrame || e.webkitRequestAnimationFrame || e.mozRequestAnimationFrame || e.oRequestAnimationFrame || e.msRequestAnimationFrame || function (e) {
      setTimeout(e, 1e3 / 60)
    }
  }(), n()
}(window, document);
```

+ <span id="inline-purple">\themes\next\layout\_layout.swig</span>, `</body>` 上方，添加

```
<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/clicklove.js"></script>
```

## 插件

### 字数与时间统计

```
npm install hexo-symbols-count-time --save
```

### 绘制图mermaid

<span id="inline-purple">安装</span>
```
npm i hexo-filter-mermaid-diagrams
```

<span id="inline-purple">主题配置文件</span>, 增加
```
# mermaid chart
mermaid: ## mermaid url https://github.com/knsv/mermaid
  enable: true  # default true
  version: "7.1.2" # default v7.1.2
  options:  # find more api options from https://github.com/knsv/mermaid/blob/master/src/mermaidAPI.js
    #startOnload: true  // default true```
```

{% note danger %}
注意set `external_link: false`
{% endnote %}

<span id="inline-purple">themes/next/layout/_partials/footer.swig</span>, 添加

```
{% if theme.mermaid.enable %}
  <script src='https://unpkg.com/mermaid@{{ theme.mermaid.version }}/dist/mermaid.min.js'></script>
  <script>
    if (window.mermaid) {
      mermaid.initialize({theme: 'forest'});
    }
  </script>
{% endif %}
```
{% btn, https://stazhenggy.github.io/2019/04/20/mermaid/ , 更多mermaid内容, % }

### 无响应问题

在国内可能会出现`npm`无响应的情况，这时可以换用`cnpm`

```bash 
npm install cnpm -g --registry=https://registry.npm.taobao.org
```
之后使用`cnpm install [name]` 

### `CERT_NOT_VALID_YET`
 
先运行

```bash
npm config set strict-ssl false
```
即可。

## .Rmd直接导入hexo

有大量的建模使用R实现; 日后查看整个建模流程或查阅一些常用命令。
具体查看需求的内容包含两点：

+ 代码以及代码的执行结果，包含图片
+ 以上需同步到博客

针对以上两个需求的实现
+ 用rmarkdown直接实现
+ 借助hexo <- 将<span id="inline-purple">.rmd</span>转成<span id="inline-purple">.md</span>, 放到<span id="inline-purple">_post</span>文件夹下即可。

可能有bug的点，是图片以及公式能否显示成功。(已解决)

### 已有方案

Xie yihui(谢益辉),谢大大已经有新的`package: blogdown`可以实现在<span id="inline-green">RStudio</span>中生成博客, 支持Hugo主题。 但自己，已经有基于Hexo搭建的博客，且现阶段基于`sublime text` + `markdown` + `git bash` 写博客的流程已经比较顺手且暂时不想再转换。所以，准备鼓捣利用`rmarkdown`，生成<span id="inline-purple">.md</span>文档。还保持之前写博客的方法。

从网上查了一些资料写了以下方案，亲测代码，代码结果输出，图片，公式，网页链接引用均没有问题。 流程不算复杂，基本满足我个人需求。

### 解决方案

#### `.rmd` -> `.md` -> `hexo`

在<span id="inline-purple">.rmd</span>文件`yaml head`里加入以下代码：

```
--- 
output:
    md_document 
        variant: markdown_github
---

```
直接`knit`即可生成<span id="inline-purple">.md</span>，然后将这个<span id="inline-purple">.md</span>移到<span id="inline-purple">_post</span>文件夹下即可。 

需要注意的一点是，如果<span id="inline-purple">.rmd</span>中包含的了图片，在`knit`的时候，会创建名为<span id="inline-purple">rmdname_files</span>的文件夹，存放该<span id="inline-purple">.md</span>中对应的图。 <span id="inline-purple">.md</span>引用该图使用的是`markdown`语法的相对路径，即`![](rmdname_files/figure-markdown_github/chunkname-1.png)`。为了保证能正确显示图片，建议使用以下流程：

+ 在<span id="inline-purple">站点配置文件</span>中, 将`post_asset_folder: false` 改为 `true`。 修改后，每次执行`hexo n(new) post_name` 将不只在<span id="inline-purple">_post</span>下生成<span id="inline-purple">post_name.md</span>, 同时新建一个与post_name`同名的文件夹。

+ 在<span id="inline-green">Rstudio</span>中, `setwd()`到<span id="inline-purple">post_name</span>文件夹下。新建<span id="inline-purple">.rmd</span>并保存到该文件夹下，注意<span id="inline-purple">.rmd</span>命名为<span id="inline-purple">post_name.rmd</span>

+ 开始写<span id="inline-purple">.rmd</span>文档。写好后，点击`knit`, 将会在<span id="inline-purple">post_name</span>文件夹中生成<span id="inline-purple">post_name.md</span>以及新文件夹:<span id="inline-purple">post_name_files</span>

+ 将<span id="inline-purple">post_name</span>文件夹中的<span id="inline-purple">post_name.md</span>替换<span id="inline-purple">_post</span>文件夹下的同名<span id="inline-purple">.md</span>即可。

#### 其他方案

参见BaoDuGe_飽蠹閣的博文：[如何将我的R项目更好地展示在Hexo博客上](http://blog.baoduge.com/rproject_hexo/)


## 参考

+ [Next各种样式](https://blleng.top/190123/#more)
+ [Next更多自定义样式](https://reishin.me/hexo-next-optimization/)
+ [Next深度优化](https://reuixiy.github.io/technology/computer/computer-aided-art/2017/06/09/hexo-next-optimization.html)
+ [Hexo+NexT优化设置](http://www.dragonstyle.win/3358042383.html#more)
+ [Hexo各种自定义](https://juejin.im/post/5c6d20b151882562934c9962)
+ [怎么在hexo博客系统中用Rmarkdown写文章](https://shixiangwang.github.io/2018/02/06/how-to-write-rmd-documents-in-hexo-system/)
+ [资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html)
+ [Hexo图片插入](http://www.xinxiaoyang.com/programming/2016-11-25-hexo-image-bug/)
+ [Hexo用Latex渲染数学公式](https://www.jianshu.com/p/68e6f82d88b7)
+ [Hexo中渲染MathJax数学公式](http://www.mamicode.com/info-detail-2145077.html)
+ [MathJax](http://docs.mathjax.org/en/latest/start.html)
+ [MathJax Reference](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference)
+ [绘图插件](https://www.liuyude.com/How_to_make_your_HEXO_blog_support_handwriting_flowchart.html)
+ [mermaid实用教程](https://blog.csdn.net/fenghuizhidao/article/details/79440583)
+ [mermaid绘图基础命令](https://blog.csdn.net/Subson/article/details/78054689)


















