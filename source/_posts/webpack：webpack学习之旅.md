---
title: webpack：webpack学习之旅
date: 2019-09-03 16:28:28
tags: webpack
category: 技术
type: 'tags'
---


<meta name="referrer" content="no-referrer"/>

<img src="" />

<!--more-->

[webpack官方文档](https://webpack.js.org/)

### 一、为什么需要构建工具

（1）转换 ES6 语法

（2）转换 JSX

（3）CSS 前传补全

（4）压缩混淆

（5）图片压缩

### 二、为什么选择 webpack

（1）社区生态丰富

（2）配置灵活和插件化扩展

（3）官方更新迭代速度快

### 三、初识 webpack

webpack是模块打包工具（Module Bundler）

* 它能识别任何模块引入方式使用的语法；
* 它能打包任何形式的文件，不仅限于js文件；

webpack 默认配置文件：webpack.config.js

可以通过 webpack --config 指定配置文件

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190918091733.png?raw=true)

### 四、安装 webpack

#### 1、安装 Node.js 和 NPM

#### 2、创建一个空目录

`mkdir my_project`

#### 3、进入该目录

`cd my_project`

#### 4、生成初始的 package 文件

`npm init -y`

#### 5、安装 webpack 和 webpack-cli

1. 全局安装

`npm install webpack webpack-cli -g`

查看版本号 `webpack -v`

卸载 `npm uninstall webapck webpack-cli -g`

2. 项目内部安装

进入项目内部，执行 `npm install webpack webpack-cli --save-dev`或`npm install webpack webpack-cli -D`

#### 6、在项目中新建一个 webpack.config.js 文件

```
'use strict';
const path = require('path');
module.exports = {
  entry: './src/index.js',
  output: {
    path: path.join(_dirname, 'dist'),
    filename: 'bundle.js'
  },
  mode: 'production'
};

```

#### 7、创建一个 src 目录

在 src 中新建一个 helloworld.js 文件

```
export function helloworld() {
  return 'Hello webpack';
}
```

在 src 中新建一个 index.js 文件

```
import { helloworld } from './helloworld';
document.write(helloworld());
```

#### 8、运行打包

在 package.json 文件中的“scripts”中添加"build": "webpack"

```
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack"
  },
```

然后`npm run build`

### 五、webpack 基本用法

本质上，webpack 是一个现代 JavaScript 应用程序的静态模块打包器（module bundler）。当 webpack 处理应用程序时，他会递归的构建一个依赖关系图（dependency graph），其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。

在这开始之前需要先理解四个核心概念：

- 入口（entry）
- 输出（output）
- loader
- 插件（plugins）

#### 1、核心概念之入口（entry）

**入口起点 **（ entry point）指示 webpack 应该使用哪个模块来作为构建其内部依赖图的开始。进入入口起点后，webpack 会找出哪些模块和库是入口起点（直接或间接）依赖的。

每个依赖项随即被处理，最后输出到称之为 bundles 的文件中。

可以通过在 webpack 配置中配置 entry 属性，来指定一个入口起点（或多个入口起点）。默认值为./src。

**单入口** ：entry 是一个字符串

```
module.exports = {
  entry:'./path/to/my/entry/files.js'
}
```

**多入口** ：entry 是一个对象

```
module.exports = {
  entry:{
    app:'./src/app.js',
    adminApp:'./src/adminApp.js'
  }
}
```

#### 2、核心概念之出口（output）

**Output** 用来告诉 webpack 如何将编译后的文件输出到磁盘

**多入口配置**

**用法：**

```
const path = require('path');
module.exports = {
  entry: {
    index: './src/index.js',
    search: './src/search.js'
  },
  output: {
    path: path.join(__dirname, 'dist'),
    filename: '[name].js'
  },
  mode: 'production'
};
```

#### 3、核心概念之 Loaders

webpack 开箱即用只支持 JS 和 JSON 两种文件类型，通过 loaders 去支持其他文件类型并且把他们转化成有效的模块，并且可以添加到依赖图中。

loaders就是一个打包方案

本身是一个函数，接受源文件作为参数，返回转换的结果。

loaders需要安装 `npm install loader名称 -D`

常见的 loaders:

|     名称      |              描述              |
| :-----------: | :----------------------------: |
| bable-loader  | 转换 ES6、ES7 等 JS 新特性语法 |
|  css-loader   |   支持.css 文件的加载和解析    |
|  less-loader  |     将 less 文件转换成 css     |
|   ts-loader   |        将 TS 转换成 js         |
|  file-loader  |     进行图片、文字等的打包     |
|  raw-loader   |   将文件以字符串定位形式导入   |
| thread-loader |      多进程打包 JS 和 CSS      |

loader是有执行顺序的，`从下到上，从右到左`

**用法：**

（1） 打包静态资源 —— 图片

a) [file-loader](https://webpack.js.org/loaders/file-loader/)

```
const path = require('path');
module.exports = {
  output: {
    filename: 'bundle.js'
  },
 modules:{
   rules:[
      {
        test:/\.(jpg|png|gif)$/,        //test指定匹配规则
        use: 'file-loader',     //use指定使用的loader名称
        options: {
          name: '[name].[ext]',  // palceholders 占位符
          outputPath: 'images/'  // 打包位置
        }
      }
   ]
 }
};
```

b) [url-loader](https://webpack.js.org/loaders/url-loader/)

（2） 打包静态资源 —— 样式

a）[style-loader](https://webpack.js.org/loaders/style-loader/)

b) [css-loader](https://webpack.js.org/loaders/css-loader/)

c）[scss-loader](https://webpack.js.org/loaders/sass-loader/)

d）[postcss-loader](https://webpack.js.org/loaders/postcss-loader/)

* loader做了什么？

  1. 当它发现他在代码中引入了一个图片时，它会将这个图片移动到打包文件中，并自定义一个图片名称
  2. 将打包文件中的图片名称返回给引入图片的文件

#### 4、核心概念之 Plugins

插件用于 bundle 文件的优化，资源管理和环境变量注入

作用于整个构建过程

**常见的 Plugin:**

|           名称           |                       描述                       |
| :----------------------: | :----------------------------------------------: |
|    CommonsChunkPlugin    |      将 chunks 相同的模块代码提取成公共 js       |
|    CleanWebpackPlugin    |                   清理构建目录                   |
| ExtractTextWebpackPlugin | 将 css 从 bundle 文件中提取成一个独立的 css 文件 |
|    CopyWebpackPlugin     |       将文件或者文件夹拷贝到构建的输出目录       |
|    HtmlWebpackPlugin     |        创建 html 文件去承载输出的 bundle         |
|   UglifyjsWepackPlugin   |                     压缩 JS                      |
|     ZipWebpackPlugin     |          将打包出的资源生成一个 zip 包           |

**用法：**

```
const path = require('path');
module.exports = {
  output: {
    filename: 'bundle.js'
  },
 plugins: [
   new HtmlWebpackPlugin({          //放在plugins数组中
     template: './src/index.js'
   })
 ]
};
```

#### 5、核心概念之 mode

mode 用来制定当前的构建环境是：production、development 还是 none

设置 mode 可以使用 webpack 内置的函数，默认值为 production

**mode 的内置函数功能**

|    选项     |                                                                                                         描述                                                                                                         |
| :---------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
| development |                                                             设置 process、env、NODE_ENV 的值为 development，开启 NamedChunksPlugin 和 NamedModulesPlugin                                                             |
| production  | 设置 process.env.NODE_ENV 的值为 production。开启 FlagDependencyUsagePlugin, FlagIncludedChunksPlugin, ModuleConcatenationPlugin, NoEmitOnErrorsPlugin, OccurrenceOrderPlugin, SideEffectsFlagPlugin 和 TerserPlugin |
|    none     |                                                                                                    不开启任何优化                                                                                                    |

### 六、资源解析

#### 1、解析 CSS

css-loader 用于加载。css 文件，并且转换成 .js 对象

style-loader 将样式通过< style > 标签插入到 head 中

`npm i style-loader css-loader -D`

```
const path = require('path');
module.exports = {
  entry:'./src/index.js'
  output: {
    filename: 'bundle.js',
    path:path.resolve(__dirname, 'dist')
  },
 modules:{
   rules:[
     {
       test:/\.css$/,
       use: [
         'style-loader',
         'css-loader'
       ]
     }
   ]
 }
};
```

#### 2、解析 Less 和 SaSS

less-loader 用于将 less 转换成 css

`npm i less less-loader -D`

```
const path = require('path');
module.exports = {
  entry:'./src/index.js'
  output: {
    filename: 'bundle.js',
    path:path.resolve(__dirname, 'dist')
  },
 modules:{
   rules:[
     {
       test:/\.less$/,
       use: [
         'style-loader',
         'css-loader',
         'less-loader'
       ]
     }
   ]
 }
};
```

#### 3、解析文件、字体

file-loader 用于处理文件、字体

`npm i file-loader -D`

```
const path = require('path');
module.exports = {
  entry:'./src/index.js'
  output: {
    filename: 'bundle.js',
    path:path.resolve(__dirname, 'dist')
  },
 modules:{
   rules:[
     {
       test:/\.(png|svg|gif|word|woff2|otf)$/,
       use: [
         'file-loader'
       ]
     }
   ]
 }
};
```

url-loader 也可以处理图片和字体，可以设置较小资源自动 base64

```
const path = require('path');
module.exports = {
  entry:'./src/index.js'
  output: {
    filename: 'bundle.js',
    path:path.resolve(__dirname, 'dist')
  },
 modules:{
   rules:[
     {
       test:/\.(png|svg|gif|word|woff2|otf)$/,
       use: [
         'url-loader',
         options:{
           limit:10240
         }
       ]
     }
   ]
 }
};
```

#### 4、解析 ES6

使用 babel-loader

babel 的配置文件是：\_babelrc

```
const path = require('path');
module.exports = {
  entry:'./src/index.js'
  output: {
    filename: 'bundle.js',
    path:path.resolve(__dirname, 'dist')
  },
 modules:{
   rules:[
     {
       test:/\.js$/,
       use: 'babel-loader'
     }
   ]
 }
};
```

增加 ES6 的 babel preset 配置

```
{
  "presets":[
    "@babel/preset-env"        ————————增加ES6的babel preset配置
    "@babel/preset-react"      ————————增加React的babel preset配置
  ],
  "plugins":[
    "@babel/proposal-class-properties"
  ]
```

### 七、webpack 中的文件监听

文件监听是在发现源码发生变化时。自动重新构建出新的输出文件

webpack 开启监听模式，有两种方式：

·启动 webpack 命令时，带上--watch 参数

·在配置 webpack.config.js 中设置成 watch:true

唯一缺陷：每次需要手动刷新浏览器

**文件监听的原理分析：**

轮训判断文件的最后编辑时间是否变化

某个文件发生了变化，并不会立刻告诉监听者，而是先缓存起来，等 aggregateTimeout

```
module.export = {
  //默认false，也就是不开启
  watch:true,
  //只有开启监听模式时，watchOptios才有意义
  watchOptions:{
    //默认为空，不监听的文件或者文件夹，支持正则匹配
    ignored:/node_modules/,
    //监听到变化发生后会等300ms再去执行，默认300ms
    aggregateTimeout:300ms,
    //判断文件是否发生变化时通过不停的询问系统指定文件有没有变化实现的，默认美妙问1000次
    poll:1000
  }
}
```

### 八、热更新

#### (1) webpack-dev-server(WDS)

WDS 不刷新浏览器

WDS 不输出文件，而是放在内存中

使用 HotModuleReplacementPlugin 插件

```
{
  "name":"hello-webpack",
  "version":"1.0.0",
  "description":"Hello webpack",
  "main":"index.js",
  "scripts":{
    "build":"webpack",
    "dev":"webpack-dev-server --open",
  },
  "keywords":[],
  "author":"",
  "license":"ISC"
}
```

#### (2) webpack-dev-middleware

WDM 将 webpack 输出的文件传送给服务器

适用于灵活的定制场景

#### (3) 热更新的原理分析

Webpack Compile：将 JS 编译成 Bundle

HMR Server：将热更新的文件输出给 HMR Runtime

Bundle server：提供文件在浏览器的访问

HMR Rumtime：会注入到浏览器，更新文件的变化

bundle.js：构建输出的文件

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190919192920.png?raw=true)

### 九、文件指纹

打包后输出的文件名的后缀

#### （1） 文件指纹如何生成

Hash：和整个项目的构建有关，只要项目文件有修改，整个项目构建的 hash 值就会更改

Chunkhash：和 webpack 打包的 chunk 有关，不同的 entry 会生成不停的 chunkhash

Contenthash：根据文件内容来定义 hash，文件内容不变，则 contenthash 不变

#### （2）JS 的文件指纹设置

设置 output 的 filename，使用[chunkhash]

```
module.exports = {
  entry: {
    index: './src/index.js',
    search: './src/search.js'
  },
  output: {
    path: __dirname+'/dist',
    filename: '[name][chunkhash:8].js'
  },
};
```

#### （3）CSS 的文件指纹设置

设置 MiniCssExtractPlugin 的 filename，使用[contenthash]

```
module.exports = {
  entry: {
    index: './src/index.js',
    search: './src/search.js'
  },
  output: {
    path: __dirname+'/dist',
    filename: '[name][chunkhash:8].js'
  },
  plugins:[
    new MiniCssExtractPlugin({
      filename:'[name][contenthash:8].css'
    })
  ]
};
```

#### （4）图片的文件指纹设置

设置 file-loader 的 name，使用[hash]

|  占位符名称   |               含义               |
| :-----------: | :------------------------------: |
|     [ext]     |            资源后缀名            |
|    [name]     |             文件名称             |
|    [path]     |          文件的组对路径          |
|   [folder]    |         文件所在的文件夹         |
| [contenthash] | 文件的内容 hash，默认是 MD5 生成 |
|    [hash]     | 文件内容的 Hash，默认是 MD5 生成 |
|    [emoji]    |  一个随机的指代文件内容的 emoji  |

```
const path = require('path');
module.exports = {
  entry: {
    index: './src/index.js',
    search: './src/search.js'
  },
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  module:{
    rules:[
      {
        test:/\.(png|svg|jpg|gif)$/,
        use:[{
          loader:'file-loader',
          options:{
            name:'img/[name][hash:8].[ext]'
          }
        }]
      }
    ]
  }
};
```

### 十、代码压缩

#### （1）JS 文件的压缩

内置了 uglifyjs-webpack-plugin

#### （3）CSS 文件的压缩

使用 optimize-css-assets-webpack-plugin

同时使用 cssnano

```
module.exports = {
  entry: {
    index: './src/index.js',
    search: './src/search.js'
  },
  output: {
    path: __dirname+'/dist',
    filename: '[name][chunkhash:8].js'
  },
  plugins:[
    new OptimizeCSSAssetsPlugin({
      assetNameRegExp:/\.css$/,
      cssProcessor:require('cssnano)
    })
  ]
};
```

#### （3）html 文件的压缩

修改 html-webpack-plugin，设置压缩参数

```
module.exports = {
  entry: {
    index: './src/index.js',
    search: './src/search.js'
  },
  output: {
    path: __dirname+'/dist',
    filename: '[name][chunkhash:8].js'
  },
  plugins:[
    new HtmlWebpackPlugin({
      tempalte:path.join(__dirname,'src/search.html'),
      filename:'search.html',
      chunks:['search'],
      inject:true,
      minify:{
        html5:true,
        collapseWhitespace:true,
        preserveLineBreaks:false,
        minifyCSS:true,
        minifyJS:true,
        removeComments:false
      }
    })
  ]
};
```
