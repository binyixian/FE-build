#npm介绍

>说明：npm（node package manager）nodejs的包管理器，用于node插件管理（包括安装、卸载、管理依赖等）；

使用npm安装插件：命令提示符执行 

```
npm install <name> [-g] [--save-dev]
```

- name:node插件名称。例：npm install gulp-less --save-dev
- -g:全局安装。将会安装在C:\Users\Administrator\AppData\Roaming\npm，并且写入系统环境变量；  非全局安装：将会安装在当前定位目录；  全局安装可以通过命令行在任何地方调用它，本地安装将安装在定位目录的node_modules文件夹下，通过require()调用；
- --save:将保存配置信息至package.json（package.json是nodejs项目配置文件）；
- -dev:保存至package.json的devDependencies节点，不指定-dev将保存至dependencies节点；


### 为什么要保存至package.json？
因为node插件包相对来说非常庞大，所以不加入版本管理，将配置信息写入package.json并将其加入版本管理，其他开发者对应下载即可（命令提示符执行npm install，则会根据package.json下载所有需要的包）。

- 使用npm卸载插件：npm uninstall <name> [-g] [--save-dev]  PS：不要直接删除本地插件包
- 使用npm更新插件：npm update <name> [-g] [--save-dev]
- 查看npm帮助：npm help
- 当前目录已安装插件：npm list

PS：npm安装插件过程：从http://registry.npmjs.org下载对应的插件包（该网站服务器位于国外，所以经常下载缓慢或出现异常），解决办法往下看↓↓↓↓↓↓。

### 选装cnpm
> 说明：因为npm安装插件是从国外服务器下载，受网络影响大，可能出现异常，如果npm的服务器在中国就好了，所以我们乐于分享的淘宝团队干了这事。

- 来自官网：“这是一个完整 npmjs.org 镜像，你可以用此代替官方版本(只读)，同步频率目前为 10分钟 一次以保证尽量与官方服务同步。”
- 官方网址：http://npm.taobao.org
- 安装：命令提示符执行npm install cnpm -g --registry=https://registry.npm.taobao.org；  注意：安装完后最好查看其版本号cnpm -v或关闭命令提示符重写打开，安装完直接使用有可能会出现错误

注：cnpm跟npm用法完全一致，只是在执行命令时将npm改为cnpm即可。

