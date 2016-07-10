## Webpack自学文档 ##
**1.1	新建一个webpack项目**

如果文件夹中没有package.json文件，则可以通过：

	$ npm init

来新建一个package.json文件，系统会引导输入名称，版本，描述等内容。

**1.2	打包js文件**

在项目中我们可能会引用到其他js文件（index.js），通过以下语句时便可以把其他js文件打包到我们引用的文件中（bundle.js）中：

	$ webpack index.js js/bundle.js

此处特地没放在同水目平录，路径使用相对路径即可。

**1.3	关于module.exports**

模块化思想中，每个文件都是独立的模块，那么问题来了，每个模块想要暴露的变量是不是该有统一的方式呈现，暴露方式如下：

	....
	module.exports = {
		name:"module.js",
		description:"I am a module"
	}

在引入端用如下方法接受即可：

	var mod = require('./module/module.js');
	console.log( mod.description );


----------

**2.1	关于Loader** 

本来webpack只能加载JS文件，通过Loader我们可以把LESS，图片等统统转换为模块，通过require来引入访问。Loader可以通过npm来管理，也可以自己在项目中写Loader模块。

**2.2	Loader的使用** 

安装css-Loader，以及对应css文件的引入方法:
		
	$ npm install css-loader style-loader

	require('!style!css!./css/style.css')

----------


**3.1	配置文件** 

如果每一项配置都需要我们手动输入，显然这种模块加载方式就会变得很麻烦，所以我们开始的package.json文件就起作用了。

	---package.json
	{
	  "name": "webpack-example",
	  "version": "1.0.0",
	  "description": "A simple webpack example.",
	  "main": "bundle.js",
	  "scripts": {
	    "test": "echo \"Error: no test specified\" && exit 1"
	  },
	  "keywords": [
	    "webpack"
	  ],
	  "author": "zhaoda",
	  "license": "MIT",
	  "devDependencies": {
	    "css-loader": "^0.21.0",
	    "style-loader": "^0.13.0",
	    "webpack": "^1.12.2"
	  }
	}
置完后执行以下：

	$ npm install

同时配置一个webpack.config.js文件：

	---webpack.config.js
	var webpack = require('webpack')
	
	module.exports = {
	  entry: './entry.js',
	  output: {
	    path: __dirname,
	    filename: 'bundle.js'
	  },
	  module: {
	    loaders: [
	      {test: /\.css$/, loader: 'style!css'}
	    ]
	  }
	}