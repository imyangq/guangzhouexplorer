# Guangzhou Explorer 网页开发教程

## 一、准备工作

### 1.1 必备工具

- VS Code：一个支持扩展的文本编辑器，用来写代码的。
- Git：一种版本控制工具，用来跟踪文件变化、协作开发代码、记录项目历史。
- GitHub：一个免费的远程代码仓库，用于托管代码以及生成 GitHub Pages 网页。

说明：GitHub Pages 是 GitHub 提供的一项免费静态网站托管服务，可以直接从 GitHub 仓库中的文件生成网页。

### 1.2 开发前准备

1. 安装VS Code和Git两个软件工具，下载地址为：
   - Git：https://git-scm.com/
   - VS Code：https://code.visualstudio.com/

2. 注册Github账户，我会将你的账户添加到源码仓库开发者中。

3. 在本地初始化git的个人信息配置，并拉取远程仓库的代码。
```
git config user.name "your name"
git config user.email "your email"
```
拉取远程仓库代码
```
git clone git@github.com:imyangq/guangzhouexplorer.git
```
执行完以上指令后，所有源码文件将会被下载到本地仓库。

4. 为了能够准确地将本地代码推送到你的 GitHub 仓库，还需要进行一次密钥匹配。

在本地执行
```
ssh-keygen -t ed25519 -C "your@email.com"
```

然后将生成的公钥（`~/.ssh/id_ed25519.pub`）添加到 GitHub 的 Settings → SSH and GPG keys 页面。
```
ssh -T git@github.com
```

如果出现
```
The authenticity of host 'github.com (140.82.xxx.xxx)' can't be established.
ED25519 key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```
则表示连接成功。

### 1.3 仓库文件说明

在克隆仓库到本地后，将得到以下的文件结构：
```
/
├── img
├── style.css
├── index.html
├── how-to-book.html
├── about-us.html
├── adventure-gulong-gorge.html
├── shenzhen-high-tech.html
├── tour-city-highlights.html
├── wholesale-market-shopping-tour.html
├── CNAME
└── README.md
```

说明：
- `img`：用于存放网页所用到的图片文件夹
- `style.css`：定义了网页中的样式
- `index.html`：`主页`页面的内容
- `how-to-book.html`：`预定`页面的内容
- `about-us.html`: `关于我们`页面的内容
- `adventure-gulong-gorge.html`：`古龙峡`产品页面的内容，其他产品介绍页面类似

### 1.4 基础 HTML 和 CSS 知识

HTML 和 CSS 是前端开发最基础和最核心的两个技术，用盖房子来举例，可以理解为
- HTML 是房子的结构
- CSS 是房子的外观装修

#### HTML 介绍

HTML（HyperText Markup Language，超文本标记语言）是用来描述网页结构和内容的语言。

简单来说，HTML 就像网页的“骨架”和“内容”，告诉浏览器：
- 页面上有哪些元素（标题、段落、图片、链接等）
- 它们的层级和语义是什么

示例：
```html
<!DOCTYPE html>
<html>
  <head>
    <title>我的网页</title>
  </head>
  <body>
    <h1>欢迎来到我的网站</h1>
    <p>这是一个用 HTML 编写的简单网页。</p>
    <img src="photo.jpg" alt="一张图片">
  </body>
</html>
```

解释：
- `<html>`：网页的根元素
- `<head>`：存放网页的元信息（标题、编码、样式等）
- `<body>`：真正显示给用户的内容
- `<h1>`：标题标签
- `<p>`：段落标签
- `<img>`：图片标签

#### CSS 介绍

CSS（Cascading Style Sheets，层叠样式表）用于控制网页的外观、样式和布局。
- HTML 决定“网页上放什么”
- CSS 决定“这些东西长什么样”

示例：
```css
body {
  background-color: #f9f9f9;
  font-family: "Microsoft YaHei", sans-serif;
}

h1 {
  color: darkblue;
  text-align: center;
}

p {
  color: #333;
  font-size: 16px;
}
```

解释：

- `body`、`h1`、`p` 是选择器，表示要修饰哪些 HTML 元素。

- `{}`里的内容是样式声明，由属性（如 color、font-size）和值（如 red、16px）组成。

#### HTML 和 CSS 之间的关系

| 对比项  | HTML         | CSS        |
| ---- | ------------ | ---------- |
| 功能   | 定义网页结构       | 定义网页样式     |
| 类型   | 标记语言         | 样式表语言      |
| 作用   | 放内容          | 美化内容       |
| 谁依赖谁 | CSS 依附于 HTML | HTML 可独立存在 |
| 比喻   | 建筑的框架        | 建筑的装饰与颜色   |

它们通常一起使用：
``` html
<!DOCTYPE html>
<html>
  <head>
    <title>HTML + CSS 示例</title>
    <style>
      body {
        background-color: #e6f7ff;
        font-family: Arial;
      }
      h1 {
        color: #0077b6;
        text-align: center;
      }
    </style>
  </head>
  <body>
    <h1>我的第一个网页</h1>
    <p>使用 HTML 搭建结构，用 CSS 美化样式。</p>
  </body>
</html>
```

## 二、开发流程

以在 Guangzhou City 1-Day Tours 模块中新增一个产品为例，开发步骤如下：

1. 打开`index.html`文件，找到
```html
<section class="tour-section">
    <div class="section-head">
        <h2>Guangzhou City 1-Day Tours</h2>
    </div>

    <div class="tour-grid">
        ...
    </div>
</section>
```
将新增的内容添加到`<div class="tour-grid">...</div>`的段尾中
```html
<section class="tour-section">
    <div class="section-head">
        <h2>Guangzhou City 1-Day Tours</h2>
    </div>

    <div class="tour-grid">
        ...
        // -以下是新增内容-
        <a class="tour-link" href="tour-city-highlights.html">
        <div class="tour-card">
            <img src="img/explore_local_food_life.png" alt="Explore Local Food & Life ">
            <div class="tour-info">
                <h3>Explore Local Food & Life </h3>
                <p>From dim sum to street food, and from Cantonese culture to a local park</p>
                <span class="price">Starting from ¥900($126) pp</span>
                <div class="icons">
                <i class="fa-regular fa-clock"></i> 8h
                </div>
            </div>
        </div>
        </a>
        // -新增内容结束-
    </div>
</section>
```

说明：

- `<a class="tour-link" href="tour-city-highlights.html">`字段中的`href`定义了这个卡片指向的新页面，新建页面在下一节介绍。
- `<img src="img/explore_local_food_life.png" alt="Explore Local Food & Life ">`中定义了卡片的展示图片， `src`是图片文件的相对位置，放在`img`文件夹中，`alt`定义了当图片文件缺失的情况下展现的文字描述。
- `<div class="tour-info">...</div>`中定义了标题（`<h3>...</h3>`），以及内容描述(`<p>...</p>`)，价格描述`<span class="price">...</span>`。
- 其他不需要修改。

2. 新建页面

由于新增内容页面的排版和已有页面是一致的，所以我们只需要直接复制任意已有页面，文件重命名为新增页面的名字，再修改页面中的具体内容即可。

首先，复制一个已有的产品内容介绍页面文件，并且重命名为`tour-city-highlights.html`。

用 VS Code 打开该文件，并找到`<main class="container main">...</main>`段落，需要修改的内容都在这个段落里面，具体如下：

封面：
```html
<section class="card">
  <div class="tour-cover-wrap">
    <img class="tour-cover" src="img/guangzhou-city-highlights/1.png"
      alt="Guangzhou City Highlights tour cover image">
  </div>
</section>
```

概要和价格：
```html
<section class="segment">
  <h2 class="tour-head">Guangzhou City Highlights</h2>
  <p class="hero__subtitle">Discover the city's must-see landmarks and historic sites in 1 day.</p>
  <div class="kv">
    <div class="kv__item"><span class="kv__key"><i class="fa-regular fa-clock"></i> Duration</span><span
        class="kv__val">8h</span></div>
    <div class="kv__item"><span class="kv__key"><i class="fa-solid fa-tag"></i> Price</span><span
        class="kv__val">From 900 RMB (130 USD) per group</span></div>
  </div>
</section>
```

为什么选择我们：
```html
  <section class="card">
    <h2 class="tour-head">Why Join This Tour?</h2>
    <ul class="list list-check">
      ...
    </ul>
  </section>
```

价格表：
```html
<section class="card">
  <h2 class="tour-head">Private Tour Price</h2>
  <div class="table-wrap">
    <table class="price-table">
      ...
    </table>
  </div>
</section>
```

费用包含：
```html
<section class="card">
  <h2 class="tour-head">Includes</h2>
  <ul class="list list-check">
    ...
  </ul>
</section>
```

费用不含：
```html
<section class="card">
  <h2 class="tour-head">Excludes</h2>
  <ul class="list list-cross">
    ...
  </ul>
</section>
```

用车价格：
```html
<section class="card">
  <h2 class="tour-head">Private car service (optional)</h2>
  <div class="table-wrap">
    <table class="price-table">
      ...
    </table>
    <p> Price includes 8-hour, 100 km service and parking fees.</p>
  </div>
</section>
```

行程安排：
```html
<section class="card gx-itn" aria-label="Itinerary">
...
</section>
```

3. 预览和推送代码

当编辑完所有内容后，可以直接用浏览器打开`index.html`文件进行预览，检查内容都没有问题后，就可以将代码推送到远程仓库进行发布，过程如下：

将修改部分添加到本地git的暂存区
```
git add .
```

提交本次的修改
```
git commit -am "本次提交你想写的备注"
```

将代码推送到远程仓库中
```
git push
```

代码推送成功后，等待几分钟后刷新网站即可看到更新后的内容。

## 三、其他

其他常用的 git 命令有：

- 拉取远程仓库的代码：`git pull`
- 放弃本次所有修改回退到上次提交版本：`git reset --hard`