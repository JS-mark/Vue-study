# Webpack
- 1.安装webpack
- 2.配置webpack.config.js
	- 配置webconfig：
~~~
官方教程：https://doc.webpack-china.org/configuration/#-
var path = require('path');

module.exports = {
	entry: './foo.js',
		output: {
		path: path.resolve(__dirname, 'dist'),
		filename: 'foo.bundle.js'
	}
	module: 
		rules: [ 
			{
				test: /\.(js|jsx)$/,
				use: 'babel-loader'
			}
		]
		plugins: [
		new (webpack.optimize.UglifyJsPlugin)
		new HtmlWebpackPlugin(template: './src/index.html')
	  ]
};
~~~
- 3.模块打包（默认只能打包JS模块，规则CommonJS等模块规范）；让webpack支持其他文件类型打包，要选择合适的loader
	- nodejs 书写模块规范 模块化规范CommonJs,AMD,ES6 modules,
- Webpack （使用npm全局安装）
	- build-tool 构建工具
	- loader webpack默认只能打包JS，loader可以帮助我们打包其他的文件类型
	- sass-loader 下载时，必须安装ruby或者python环境才能使用；
	- 安装webpack-dev-server热启动插件，必须在项目在安装webpack，要不然会报错！
	- webpack 使用方法：
		在命令行 输入webpack 入口文件(app.js) 输出文件（build.js）
	- 配置webpack ； 使用webpack.config.js；让webpack支持其他文件类型打包，要选择合适的loader
	- url-loader 和 file-loader 类似，url-loader加载不了的使用file-loader加载；
	- HtmlWebpackPlugin 插件(自动在output目录中生成文件)以及，配置安装
  	- npm install --save-dev html-webpack-plugin
  	- 在webpack.config.js中配置：
~~~
  const path = require('path');
  const HtmlWebpackPlugin = require('html-webpack-plugin');

  module.exports = {
    entry: {
      app: './src/index.js',
      print: './src/print.js'
    },
    plugins: [
     new cleanWebpackPlugin(['dist']),//数组内可以放置多个要删除的目录，放置在HtmlWebpackPlugin插件前
     new HtmlWebpackPlugin({
        title: '页面标题',  //生成页面标题
        filename: 'index.html',//要生成的文件名
        template: 'index.html'//要生成页面的时候的模板
     })
   ],
    output: {
      filename: '[name].bundle.js',
      path: path.resolve(__dirname, 'dist')
    }
  };
~~~
- JSon文件中不能以有注释
  - 使用package.json中的scripts键名是要启动的命令的简写，值是要启动的命令（这个个命令可以随意写，反正就是要在命令行中执行的命令，就可以写在这里）；
  - 例： 
  "scripts": {
    "dev": "webpack-dev-server --inline --hot --open --port 3000"
  },
  启动命令为 npm run dev
  例： 
  "scripts": {
    "start": "webpack-dev-server --inline --hot --open --port 3000"
  },
  启动命令为 npm start
如果键名是start，可以省略写run

- 配置HMR 模块热替换，热替换这个插件，必须配置在项目目录，因为配置全局的话，不会有热替换的效果，浏览器不会自动刷新；插件webpack-dev-sever在package.json
- "scripts": {
    "start": "webpack-dev-server --inline --hot --open --port 3000"
  }
- 配置ES6语法降级，-bable-loader
~~~
{
  test: /\.js$/,
  exclude: /(node_modules|bower_components)/,
  use: {
    loader: 'babel-loader',
    options: {
      presets: ['@babel/preset-env']
    }
  }
}
~~~
- 解析vue模板，vue-loader，这个模板安装后，可能会发生错误，就是需要在安装另外一个模块，安装上就好了！
- 解析文件的话，要去下载各种文件类型的loader
- webpack 可以打包各种模块，js就是模块或者说是包，我们可以直接使用CommenJS或者ES6等规范的语法，导入各种各样我们需要的模块，并把它并把导入的模块用对象包裹起来，我们就可以调用里边的方法了