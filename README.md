## Webpack自学文档 ##
### 1.新建一个webpack项目 ###
如果文件夹中没有package.json文件，则可以通过：

	$ npm init

来新建一个package.json文件，系统会引导输入名称，版本，描述等内容。

### 2.打包js文件 ###
在项目中我们可能会引用到其他js文件（index.js），通过以下语句时便可以把其他js文件打包到我们引用的文件中（bundle.js）中：

	$ webpack index.js js/bundle.js

此处特地没放在同水品目录，路径使用相对路径即可。

### 3.关于module.exports ###
模块化思想中，每个文件都是独立的模块，那么问题来了，每个模块想要暴露的变量是不是该有统一的方式呈现，暴露方式如下：

	....
	module.exports = {
		name:"module.js",
		description:"I am a module"
	}

在引入端用如下方法接受即可：

	var mod = require('./module/module.js');
	console.log( mod.description );