# Gulp 快速入门

 [Gulp.js](http://www.gulpjs.com.cn) 是一个自动化构建工具,开发者可以使用它在项目开发过程中自动执行常见任务。

### 1.全局安装

```
npm install --global gulp
```

### 2.作为项目的开发依赖（devDependencies）安装：

```
npm install --save-dev gulp
```

### 3.在项目根目录下创建一个名为 gulpfile.js 的文件：

```
var gulp = require('gulp');

gulp.task('default', function() {
  // 将你的默认的任务代码放在这
});

```

### 4.运行gulp

```
gulp

```



















