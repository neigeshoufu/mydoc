### **1.安装webpack4及基本配置**
#### 1.1 本地安装
```shell
npm init -y
npm install --save-dev webpack 
```
- webpack4.0+还需要安装CLI
```
npm install --save-dev webpack-cli
```
- 一条命令安装两个
```npm install webpack webpack-cli --save-dev  //webpack和cli```
#### 1.2 基本目录结构

```markdown
webpack-demo
  |- package.json
+ |- index.html
+ |- /src
+   |- index.js
```

#### 1.3  webpack.config.js
- 可包含以下配置项。配置语法参考node.js
```javascript
//路径模块
const path = require('path');
//导入内存中生成页面的插件
const HtmlWebpackPlugin = require('html-webpack-plugin');
//这个插件：自动在内存中根据指定的页面生成一个内存页面
//同时会自动把打包好的bundle.js追加到页面中
//const { CleanWebpackPlugin } = require('clean-webpack-plugin');
//这个文件其实就是js文件，通过node中的模块操作，向外暴露了一个配置对象
module.exports = {
    //手动指定入口和出口文件
    entry: path.join(__dirname,'./src/index.js'), //入口，表示要使用webpack打包哪一个文件
    output: {   //输出文件相关配置
        filename: 'bundle.js', //指定输出文件名称
        
        //指定打包好的文件输出到哪个目录
        path: path.resolve(__dirname, 'dist'),  
    },
    plugins: [
         new HtmlWebpackPlugin({  //创建一个在内存中生成html页面的插件
             template:path.join(__dirname, './src/index.html'),  //指定模板页面，根据这个页面在内存中生成
             filename:'index.html'  //指定生成页面的名称
         }),
        // new CleanWebpackPlugin(),
    ],
    devServer: {
        contentBase: './dist',
        port: 8000
    },
    //这个节点用于配置所有的第三方模块加载器
    module: {
        rules: [    //所有第三方模块的匹配规则
            {
                test: /\.css$/,
                use: [  //处理css的规则
                    'style-loader',
                    'css-loader'
                ]
            },
            {
                test: /\.less$/,
                use: [  //处理less的规则
                    'style-loader',
                    'css-loader',
                    'less-loader' 
                ]
            },
            {
                test: /\.scss$/,
                use: [  //处理sass的规则
                    'style-loader',
                    'css-loader',
                    'sass-loader' 
                ]
            },
            {
                test: /\.(jpg|png|svg|gif)$/,
                use: [
                    'file-loader'
                ]
            },
            {
                test: /\.(woff|woff2|eot|ttf|otf)$/,
                use: [
                    'file-loader'
                ]
            },
           {
               test: /\.js$/,
              use: [
                  'babel-loader'
               ],
           },
        ]
    }
}
```
- 指定多个文件入口，如：
```
entry: {
   home:'./home.js',
   about:'./about.js',
   other:'./other.js'
}，
    output: {   //输出文件相关配置
        filename: '[name].bundle.js', //指定输出文件名称
        
        //指定打包好的文件输出到哪个目录
        path: path.resolve(__dirname, 'dist'),  
    }
```
### **2.配置css,less,scss加载器**
#### 2.1 css-loader,less-loader,sass-loader
- CSS
 ```npm i style-loader css-loader -d ```
- less
``` npm i less-loader -d ```。less-loader需要依赖less，所以还需要安装less```npm i less -d```
- scss
``` npm i sass-loader -d ```。sass-loader需要依赖node-sass，所以还需要安装node-sass```npm i node-sass -d```
- 配置webpack.config.js:
```
//这个节点用于配置所有的第三方模块加载器
    module: {
        rules: [    //所有第三方模块的匹配规则
            {
                test: /\.css$/,
                use: [  //处理css的规则
                    'style-loader',
                    'css-loader'
                ]
            },
            {
                test: /\.less$/,
                use: [  //处理less的规则
                    'style-loader',
                    'css-loader',
                    'less-loader' 
                ]
            },
            {
                test: /\.scss$/,
                use: [  //处理sass的规则
                    'style-loader',
                    'css-loader',
                    'sass-loader' 
                ]
            }
        }
```
### **3.安装jQuery**
```npm install jquery --save```   
- 使用```import $ from 'jquery';```

### **4.webpack-dev-server**
- 这个插件提供了一个小型服务器。可以看到页面实时刷新
- 安装```npm install webpack-dev-server -d```
- 配置package.json
```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "webpack-dev-server --open --port 8099 --contentBase src --hot"
  },
```
(```--open```表示自动打开页面,```--port```指定预览端口,```--contentBase```指定默认显示路径,```--hot```表示开启热重载)
- 配置webpack.config.json
```
//新增加
devServer: {
    contentBase: './dist',
    port: 8000
    },
```
- 运行```npm run dev```
### **4.html-webpack-plugin**
- 为html文件中引入的外部资源如script、link动态添加每次compile后的hash，防止引用缓存的外部文件问题
- 可以生成创建html入口文件，比如单页面可以生成一个html文件入口，配置N个html-webpack-plugin可以生成N个页面入口
- 安装```npm i html-webpack-plugin -d ```
- 配置webpack.config.js
导入模块
```
 //导入内存中生成页面的插件
const HtmlWebpackPlugin = require('html-webpack-plugin')；
```
新增一项：plugins
```
 plugins: [
         new HtmlWebpackPlugin({  //创建一个在内存中生成html页面的插件
             template:path.join(__dirname, './src/index.html'),  //指定模板页面，根据这个页面在内存中生成
             filename:'index.html'  //指定生成页面的名称
         }),
        // new CleanWebpackPlugin(),
    ],
```
### **5.运行**
- webpack-dev-server运行```npm run dev```
- 打包```.\webpack --mode development```

### **6.url-loader,file-loader**
- ```npm i url-loader file-loader -d```
- 配置webpack.config.js
modules的rules新增一条
```
//处理图片
   {
    test: /\.(jpg|png|svg|gif)$/,
     use: [
         'url-loader?limit=385680'
        //limit给定的值是图片的大小，单位是byte。如果引用的图片大于或等于给定的limit，则不会转为base64格式，如果图片小于，就会
       //转为base64
    //'url-loader?limit=385680&name=[hash:8]-[name].[ext]' 这个保持图片名字和格式 并给哈希
      ]
    },
    {
    test: /\.(woff|woff2|eot|ttf|otf)$/, //处理字体文件
    use: [
     'url-loader'
     ]
   },
```
### **7.高阶语法转换**
- 1
```npm install --save-dev babel-loader```，```npm install --save-dev @babel/core @babel/cli @babel/preset-env```,
```npm install babel-core -D ```
或者以下：
```
//webpack中不能转换所有高级语法
//bable可以进行转换：
//两套包：
//npm i bable-core bable-loader bable-plugin-transform-runtime -d
//npm i bable-preset-env bable-preset-stage-0 -d
//然后进行配置modules中的rules添加匹配规则
//新建.bablerc的配置文件
//.bablerc中如下配置：
// //{
//     "presets":["env","stage-0"],
//     "plugins":["插件名"]
// }
```