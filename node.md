# node 安装方法

访问 [nodejs](https://nodejs.org/en/) 官网 下载最新版本安装即可

#  NPM介绍

NPM的全称是Node Package Manager，是一个NodeJS包管理和分发工具，
已经成为了非官方的发布Node模块（包）的标准。在安装NODEJS的时候已经默认安装。

# 测试

在系统任意目录下创建JS文件，如 test.js

  ```
    var http = require('http');
    http.createServer(function (req, res) {
        res.writeHead(200, {'Content-Type': 'text/plain'});
        res.end('Hello World\n');
    }).listen(1337, '127.0.0.1');
    console.log('Server running at http://127.0.0.1:1337/');

  ```
在终端进入该目录 输入

  ```
  node test.js

  ```
在浏览器中输入  http://127.0.0.1:1337/ 查看结果 为 “Hello World”
至此 NODEJS 运行环境已经配置好。

# 查看当前版本

在终端输入

```
node -v

```

```
npm -v

```

查看当前安装 node、npm 版本。
