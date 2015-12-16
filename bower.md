
#  bower 

Bower是一个客户端技术的软件包管理器，它可用于搜索、安装和卸载如JavaScript、HTML、CSS之类的网络资源。
其他一些建立在Bower基础之上的开发工具，如YeoMan和Grunt。

#  安装 bower

### 准备工作

安装bower 首先需要安装如下文件

- node
- NPM
- Git

### 安装bower

```
npm install -g bower

```

### 开始使用bower

安装完bower之后就可以使用所有的bower命令了，可以键入 `help` 来查看。


### 包的安装

Bower是一个软件包管理器，所以你可以在应用程序中用它来安装新的软件包。举例来看一下来如何使用Bower安装JQuery，在你想要安装该包的地方创建一个新的文件夹，键入如下命令：

```
 bower install jquery
 
```

上述命令完成以后，你会在你刚才创建的目录下看到一个 `bower_components` 的文件夹，其中目录如下:

```
$ tree bower_components/
bower_components/
└── jquery
    ├── README.md
    ├── bower.json
    ├── component.json
    ├── composer.json
    ├── jquery-migrate.js
    ├── jquery-migrate.min.js
    ├── jquery.js
    ├── jquery.min.js
    ├── jquery.min.map
    └── package.json

1 directory, 10 files

```


# bower.json文件的使用

bower.json文件的使用可以让包的安装更容易，你可以在应用程序的根目录下创建一个名为“bower.json”的文件，并定义它的依赖关系。使用 `bower init` 命令来创建 bower.json 文件：

```
$ bower init
[?] name: wee
[?] version: 1.0.0
[?] description:简单快速的响应式HTML/CSS前端框架
[?] main file:
[?] keywords: css scss framework lightweight responsive
[?] authors: King Zhi <zyj10222@126.com>
[?] license: MIT
[?] homepage:
[?] set currently installed components as dependencies? Yes
[?] add commonly ignored files to ignore list? Yes
[?] would you like to mark this package as private which prevents it from being accidentally published to the registry? No

{
  "name": "wee",
  "version": "1.0.0",
  "homepage": "https://github.com/zyj1022/wee",
  "authors": [
    "King Zhi <zyj10222@126.com>"
  ],
  "description": "简单快速的响应式HTML/CSS前端框架",
  "keywords": [
    "css",
    "scss",
    "framework",,
    "lightweight",
    "responsive"
  ],
  "license": "MIT",
  "ignore": [
    "**/.*",
    "node_modules",
    "bower_components",
    "test",
    "tests"
  ],
  "main": "",
  "moduleType": [],
  "private": true,
  "dependencies": {
    "jquery": "~2.1.4"
  }
  
[?] Looks good? Yes

```
可以查看该文件，会加入jQuery的依赖关系。

如果想要用 modernizr，可以用下面的命令安装 modernizr 并更新 bower.json 文件：

```
bower install modernizr --save

```

它会自动安装最新版本的 modernizr 并更新bower.json文件：

```
{
  "name": "wee",
  "version": "1.0.0",
  "homepage": "https://github.com/zyj1022/wee",
  "authors": [
    "King Zhi <zyj10222@126.com>"
  ],
  "description": "简单快速的响应式HTML/CSS前端框架",
  "keywords": [
    "css",
    "scss",
    "framework",,
    "lightweight",
    "responsive"
  ],
  "license": "MIT",
  "ignore": [
    "**/.*",
    "node_modules",
    "bower_components",
    "test",
    "tests"
  ],
  "main": "",
  "moduleType": [],
  "private": true,
  "dependencies": {
    "modernizr": "~3.2.0",
    "jquery": "~2.1.4"
  }

```



