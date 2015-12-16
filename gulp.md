# Gulp 快速入门

 [Gulp.js](http://www.gulpjs.com.cn) 是一个自动化构建工具,开发者可以使用它在项目开发过程中自动执行常见任务。
他不仅能对网站资源进行优化，而且在开发过程中很多重复的任务能够使用正确的工具自动完成，提高我们的工作效率。


gulp是基于Nodejs的自动任务运行器， 她能自动化地完成 javascript/coffee/sass/less/html/image/css 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。在实现上，她借鉴了Unix操作系统的管道（pipe）思想，前一级的输出，直接变成后一级的输入，使得在操作上非常简单。通过本文，我们将学习如何使用Gulp来改变开发流程，从而使开发更加快速高效。

###gulp常用地址：

- [gulp 官方网址](http://gulpjs.com)
- [gulp 插件地址](http://gulpjs.com/plugins)
- [gulp 官方API](https://github.com/gulpjs/gulp/blob/master/docs/API.md)
- [gulp 中文API](http://www.ydcss.com/archives/424)


在学习前，先谈谈大致使用gulp的步骤，给读者以初步的认识。首先当然是安装nodejs，通过nodejs的npm全局安装和项目安装gulp，其次在项目里安装所需要的gulp插件，然后新建gulp的配置文件gulpfile.js并写好配置信息（定义gulp任务），最后通过命令提示符运行gulp任务即可。

**安装nodejs -> 全局安装gulp -> 项目安装gulp以及gulp插件 -> 配置gulpfile.js -> 运行任务**



### 1.全局安装gulp

全局安装gulp目的是为了通过他来执行gulp任务

```
npm install --global gulp
```

查看是否正确安装：命令提示符执行 `gulp -v`，出现版本号即为正确安装

### 2.作为项目的开发依赖（devDependencies）安装：

```
npm install --save-dev gulp
```

本示例以 gulp-less 为例（编译less文件），命令提示符执行

```
npm install gulp-less --save-dev
```
将会安装在node_modules的gulp-less目录下，该目录下有一个gulp-less的使用帮助文档README.md

为了能正常使用，我们还得本地安装gulp：

```
npm install gulp --save-dev
```
PS:细心的你可能会发现，我们全局安装了gulp，项目也安装了gulp，全局安装gulp是为了执行gulp任务，本地安装gulp则是为了调用gulp插件的功能。

### 3.新建 gulpfile.js：

说明：gulpfile.js是gulp项目的配置文件，是位于项目根目录的普通js文件

它大概是这样一个js文件（更多插件配置[请查看这里](http://www.ydcss.com/archives/tag/gulp)）：

```
//导入工具包 require('node_modules里对应模块')
var gulp = require('gulp'), //本地安装gulp所用到的地方
    less = require('gulp-less');
 
//定义一个testLess任务（自定义任务名称）
gulp.task('testLess', function () {
    gulp.src('src/less/index.less') //该任务针对的文件
        .pipe(less()) //该任务调用的模块
        .pipe(gulp.dest('src/css')); //将会在src/css下生成index.css
});
 
gulp.task('default',['testLess', 'elseTask']); //定义默认任务
 
//gulp.task(name[, deps], fn) 定义任务  name：任务名称 deps：依赖任务名称 fn：回调函数
//gulp.src(globs[, options]) 执行任务处理的文件  globs：处理的文件路径(字符串或者字符串数组) 
//gulp.dest(path[, options]) 处理完后文件生成路径

```

```
var gulp = require('gulp');

gulp.task('default', function() {
  // 将你的默认的任务代码放在这
});

```

该示例文件请[下载查看](http://www.ydcss.com/wp-content/uploads/2015/03/gulp.rar)



### 4.运行gulp

```
gulp

```

- 说明：命令提示符执行gulp 任务名称；
- 编译less：命令提示符执行gulp testLess；
- 当执行gulp default或gulp将会调用default任务里的所有任务[‘testLess’,’elseTask’]。



# glup 任务实例

我们将要使用Gulp插件来完成我们以下任务：

- sass的编译（gulp-sass）
- 自动添加css前缀（gulp-autoprefixer）
- 压缩css（gulp-minify-css）
- js代码校验（gulp-jshint）
- 合并js文件（gulp-concat）
- 压缩js代码（gulp-uglify）
- 压缩图片（gulp-imagemin）
- 自动刷新页面（gulp-livereload）
- 图片缓存，只有图片替换了才压缩（gulp-cache）
- 更改提醒（gulp-notify）

安装这些插件需要运行如下命令：

```
npm install gulp-sass gulp-autoprefixer gulp-minify-css gulp-jshint gulp-concat gulp-uglify gulp-imagemin gulp-notify gulp-rename gulp-livereload gulp-cache --save-dev

```
更多插件可以看这里 [gulpjs.com/plugins/](http://gulpjs.com/plugins/)


接着我们要创建一个gulpfile.js在根目录下，gulp只有四个API： task，watch，src，和 dest

- task这个API用来创建任务，在命令行下可以输入 gulp test 来执行test的任务。
- watch这个API用来监听任务。
- src这个API设置需要处理的文件的路径，可以是多个文件以数组的形式[main.scss, vender.scss]，也可以是正则表达式/**/*.scss。
- dest这个API设置生成文件的路径，一个任务可以有多个生成路径，一个可以输出未压缩的版本，另一个可以输出压缩后的版本。


###加载插件 

```
// Load plugins
var gulp = require('gulp'),
    sass = require('gulp-sass'),
    autoprefixer = require('gulp-autoprefixer'),
    minifycss = require('gulp-minify-css'),
    jshint = require('gulp-jshint'),
    uglify = require('gulp-uglify'),
    imagemin = require('gulp-imagemin'),
    rename = require('gulp-rename'),
    concat = require('gulp-concat'),
    notify = require('gulp-notify'),
    cache = require('gulp-cache'),
    livereload = require('gulp-livereload');
```

### 建立任务：

编译sass、自动添加css前缀和压缩

首先我们编译sass，添加前缀，保存到我们指定的目录下面，还没结束，我们还要压缩，给文件添加 .min 后缀再输出压缩文件到指定目录，最后提醒任务完成了：

```
// Styles任务
gulp.task('styles', function() {
    //编译sass
    return gulp.src('stylesheets/main.scss')
    .pipe(sass())
    //添加前缀
    .pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))
    //保存未压缩文件到我们指定的目录下面
    .pipe(gulp.dest('stylesheets'))
    //给文件添加.min后缀
    .pipe(rename({ suffix: '.min' }))
    //压缩样式文件
    .pipe(minifycss())
    //输出压缩文件到指定目录
    .pipe(gulp.dest('assets'))
    //提醒任务完成
    .pipe(notify({ message: 'Styles task complete' }));
});
```

###  js代码校验、合并和压缩

```
// Scripts任务
gulp.task('scripts', function() {
    //js代码校验
    return gulp.src('javascripts/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter('default'))
    //js代码合并
    .pipe(concat('all.js'))
    //给文件添加.min后缀
    .pipe(rename({ suffix: '.min' }))
    //压缩脚本文件
    .pipe(uglify())
    //输出压缩文件到指定目录
    .pipe(gulp.dest('assets'))
    //提醒任务完成
    .pipe(notify({ message: 'Scripts task complete' }));
});
```

### 图片压缩

```
// Images
gulp.task('images', function() {
  return gulp.src('images/*')
    .pipe(cache(imagemin({ optimizationLevel: 3, progressive: true, interlaced: true })))
    .pipe(gulp.dest('images'))
    .pipe(notify({ message: 'Images task complete' }));
});
```

### 事件监听

```
// Watch
gulp.task('watch', function() {
  // Watch .scss files
  gulp.watch('stylesheets/*.scss', ['styles']);
  // Watch .js files
  gulp.watch('javascripts/*.js', ['scripts']);
  // Watch image files
  gulp.watch('images/*', ['images']);
  // Create LiveReload server
  livereload.listen();
  // Watch any files in assets/, reload on change
  gulp.watch(['assets/*']).on('change', livereload.changed);
});
```


### 完整代码

```
/*!
 * gulp
 * $ npm install gulp-sass gulp-autoprefixer gulp-minify-css gulp-jshint gulp-concat gulp-uglify gulp-imagemin gulp-notify gulp-rename gulp-livereload gulp-cache --save-dev
 */
// Load plugins
var gulp = require('gulp'),
    sass = require('gulp-sass'),
    autoprefixer = require('gulp-autoprefixer'),
    minifycss = require('gulp-minify-css'),
    jshint = require('gulp-jshint'),
    uglify = require('gulp-uglify'),
    imagemin = require('gulp-imagemin'),
    rename = require('gulp-rename'),
    concat = require('gulp-concat'),
    notify = require('gulp-notify'),
    cache = require('gulp-cache'),
    livereload = require('gulp-livereload');
// Styles
gulp.task('styles', function() {
    return gulp.src('stylesheets/main.scss')
    .pipe(sass())
    .pipe(autoprefixer('last 2 version', 'safari 5', 'ie 8', 'ie 9', 'opera 12.1', 'ios 6', 'android 4'))
    .pipe(gulp.dest('stylesheets'))
    .pipe(rename({ suffix: '.min' }))
    .pipe(minifycss())
    .pipe(gulp.dest('assets'))
    .pipe(notify({ message: 'Styles task complete' }));
});
// Scripts
gulp.task('scripts', function() {
  return gulp.src('javascripts/*.js')
    .pipe(jshint())
    .pipe(jshint.reporter('default'))
    .pipe(concat('all.js'))
    .pipe(rename({ suffix: '.min' }))
    .pipe(uglify())
    .pipe(gulp.dest('assets'))
    .pipe(notify({ message: 'Scripts task complete' }));
});
// Images
gulp.task('images', function() {
  return gulp.src('images/*')
    .pipe(cache(imagemin({ optimizationLevel: 3, progressive: true, interlaced: true })))
    .pipe(gulp.dest('images'))
    .pipe(notify({ message: 'Images task complete' }));
});
// Default task
gulp.task('default', function() {
    gulp.start('styles', 'scripts', 'images');
});
// Watch
gulp.task('watch', function() {
  // Watch .scss files
  gulp.watch('stylesheets/*.scss', ['styles']);
  // Watch .js files
  gulp.watch('javascripts/*.js', ['scripts']);
  // Watch image files
  gulp.watch('images/*', ['images']);
  // Create LiveReload server
  livereload.listen();
  // Watch any files in assets/, reload on change
  gulp.watch(['assets/*']).on('change', livereload.changed);
});
```

### 运行

可以运行单独的任务，例如

```
gulp default
gulp watch
```

也可以运行整个任务

```
gulp
```


### 最后是我自己设置的项目文件路径

```
|--/dist/ ---------- 压缩后样式和脚本存放的目录
|--/images/ -------- 图片存放目录
|--/js/ ------------ 脚本存放目录
|--/style/ --------- 样式存放目录
|--/plugin/ -------- 插件存放目录
|--gulpfile.js

```

更多参考内容 [查看这里](https://markgoodyear.com/2014/01/getting-started-with-gulp/)















