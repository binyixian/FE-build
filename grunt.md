# Grunt 入门

[Grunt](http://www.gruntjs.net) 和 Grunt插件是通过 npm 安装并管理的，npm 是 Node.js 的包管理器。

#  安装CLI

你需要先将Grunt命令行（CLI）安装到全局环境中，安装时可能需要使用 sudo
（针对OSX）权限或者作为管理员（对于Windows环境）来执行以下命令

 
  ```
    npm install -g grunt-cli
  ```
  

上述命令执行完后，grunt 命令就被加入到你的系统路径中了，以后就可以在任何目录下执行此命令了。


# CLI 是如何工作的

每次运行 `grun` 时，他就利用 `node` 提供的 `require()` 系统查找本地安装的 Grunt。
正是由于这一机制，你可以在项目的任意子目录中运行 `grunt` 。

如果找到一份本地安装的 Grunt，CLI就将其加载，并传递Gruntfile中的配置信息，然后执行你所指定的任务。



# Grunt 实战

在项目目录中添加 `package.json` 和 `Gruntfile`


### package.json


打开终端，进入目录中运行 

```
npm install
```

将依据 `package.json` 文件中所列出的每个依赖自动安装

- 运行 `npm init` 命令会创建一个基本的 `package.json` 文件
- `package.json` 案例，并根据需求扩充

```
	{
		"name": "demo",
		"file": "zepto",
		"version": "0.1.0",
		"description": "demo",
		"license": "MIT",
		"devDependencies": {
			"bower": "^1.7.1",
			"grunt": "~0.4.1",
			"grunt-contrib-clean": "~0.5.0",
			"grunt-contrib-concat": "~0.3.0",
			"grunt-contrib-copy": "~0.4.1",
			"grunt-contrib-jshint": "~0.6.3",
			"grunt-contrib-qunit": "~0.7.0",
			"grunt-contrib-requirejs": "~0.4.1",
			"grunt-contrib-uglify": "~0.2.1",
			"grunt-contrib-watch": "~0.6.1",
			"grunt-strip": "~0.2.1",
			"gulp": "^3.9.0"
	     },
		"dependencies": {
			 "express": "3.x"
		 }
	  }		
```

### 安装Grunt 和 grunt插件

向已经存在的 `package.json` 文件中添加 Grunt 和 [grunt插件](http://www.gruntjs.net/plugins) 的最简单方式是通过
`npm install <module> --save-dev` 命令

例如，下面这条命令将安装Grunt最新版本到项目目录中，并将其添加到devDependencies内：

```
npm install grunt --save-dev
```
同样，grunt插件和其它node模块都可以按相同的方式安装。
下面展示的实例就是安装 JSHint 任务模块：

```
npm install grunt-contrib-jshint --save-dev
```


# Gruntfile

Gruntfile.js 文件放入项目根目录

Gruntfile由以下几部分构成：

- "wrapper" 函数
- 项目与任务配置
- 加载grunt插件和任务
- 自定义任务

### Gruntfile文件案例 

将下面代码放入 `Gruntfile.js`，运行 `grunt` 测试。

```
module.exports = function(grunt) {

  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    concat: {
      options: {
        // 定义一个用于插入合并输出文件之间的字符
        separator: ';'
      },
      dist: {
        // 将要被合并的文件
        src: ['src/**/*.js'],
        // 合并后的JS文件的存放位置
        dest: 'dist/<%= pkg.name %>.js'
      }
    },
    
    // 它的作用是压缩（minify)
    uglify: {
      options: {
        // 此处定义的banner注释将插入到输出文件的顶部
        banner: '/*! <%= pkg.name %> <%= grunt.template.today("dd-mm-yyyy") %> */\n'
      },
      dist: {
        files: {
          'dist/<%= pkg.name %>.min.js': ['<%= concat.dist.dest %>']
        }
      }
    },
    
    qunit: {
      files: ['test/**/*.html']
    },
    
    jshint: {
      files: ['Gruntfile.js', 'src/**/*.js', 'test/**/*.js'],
      options: {
        //这里是覆盖JSHint默认配置的选项
        globals: {
          jQuery: true,
          console: true,
          module: true,
          document: true
        }
      }
    },
    
    watch: {
      files: ['<%= jshint.files %>'],
      // 你可以在命令行使用grunt watch来运行这个任务
      tasks: ['jshint', 'qunit']
    }
  });

  grunt.loadNpmTasks('grunt-contrib-uglify');
  grunt.loadNpmTasks('grunt-contrib-jshint');
  grunt.loadNpmTasks('grunt-contrib-qunit');
  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-contrib-concat');
  
  // 在命令行上输入"grunt test"，test task就会被执行。
  grunt.registerTask('test', ['jshint', 'qunit']);
  
  // 只需在命令行上输入"grunt"，就会执行default task
  grunt.registerTask('default', ['jshint', 'qunit', 'concat', 'uglify']);

};

```













