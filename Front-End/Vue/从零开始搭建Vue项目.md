[TOC]

# 从零开始搭建Vue项目

## 初始化项目

创建项目的根目录，命名为`CustomVueProject`。之后进入到目录中，执行`npm init -y`。

```bash
mkdir WithoutVueCli
cd WithoutVueCli
npm init -y
```

## 安装依赖

### webpack系列

项目使用`webpack`工具进行打包，需要安装`webpack`、`webpack-cli`、`webpack-dev-server`这三个依赖。

同时，因为开发配置与生成配置是两个独立的文件，需要`webpack-merge`合并最基础的配置。

```bash
npm i -D webpack webpack-cli webpack-dev-server webpack-merge
```

### Babel系列

我们需要安装babel的依赖，来处理ES5版本以上的JS代码。

```bash
npm i -D bable-loader @babel/core @babel/preset-env @babel/plugin-transform-runtime 
npm i -S @babel/runtime
```

### Vue系列

既然是Vue的项目，自然需要安装Vue的相关包依赖，执行下面的命令安装：

```bash
npm i -S vue
npm i -D vue-loader vue-template-compiler vue-router
```

### CSS系列

项目采用的是`SCSS`预处理器，如果要安装其他的预处理器，可自行Google。

```bash
npm i -D sass-loader node-sass style-loader css-loader
```

### 图片和字体

需要安装两个依赖：`url-loader`、`file-loader`。

```bash
npm i -D url-loader file-loader
```

### html-webpack-plugin

安装`html-webpack-plugin`插件，这个插件会自动生成html文件，当然，也可以指定模版生成。

```bash
npm i -D html-webpack-plugin
```

## 编写Webpack与相关配置

在项目的根目录下，我们创建一个`webpack.config.js`文件，并在对其编写如下：

```javascript
//webpack.config.js
const VueLoaderPlugin = require('vue-loader/lib/plugin')
const path = require('path')
const HtmlWebpackPlugin = require('html-webpack-plugin')


module.exports = {
  entry: './src/main.js',
  output: {
    path: path.resolve(__dirname, './build/'),
    filename: 'scripts/bundle.js',
    publicPath: '/'
  },
  resolve: {
    extensions: ['.vue', '.js']
  },
  module: {
    rules: [
      {
        test: /\.js$/,
        exclude: /node_modules/,
        use: 'babel-loader'
      },
      {
        test: /\.vue$/,
        use: 'vue-loader'
      }
    ]
  },
  devServer: {
    host: 'localhost',
    port: 5000,
    histortyApiFallback: true
  },
  plugins: [
    new VueLoaderPlugin(),
    new HtmlWebpackPlugin({
      filename: 'index.html',
      template: path.resolve(__dirname, './src/main.js')
    })
  ]
}
```

这是基本的webpack配置。我们使用到`babel-loader`来转译JS，按照其官方要求，我们还需要对babel编写配置，编写配置有几种，这里采用其中一种，感兴趣的同学可以去官网查看。

在根目录下，我们创建`babel.config.js`文件，并对其编写配置：

```javascript
//babel.config.js
module.exports = {
  presets: [
    [
      '@babel/preset-env',
      {
        useBuiltIns: 'usage'
      }
    ]
  ],
  plugins: ['@babel/plugin-transform-runtime']
}
```

## 创建src目录

在根目录下创建`src`目录，然后依次在该目录下创建`main.js`、`App.vue`、`index.html`。创建完成后，就可以编写代码了。

**main.js**

```javascript
//main.js
import Vue from 'vue'

import App from './App'

new Vue({
  render: h => h(App)
}).$mount('#root')
```

**App.vue**

```vue
//App.vue
<template>
  <div>
    <h1>{{msg}}</h1>
  </div>
</template>

<script>
  export default {
    name: 'App',
    data() {
      return {
        msg: '不使用Vue-CLI来搭建Vue项目'
      }
    }
  }
</script>

<style scoped>
</style>
```

**index.html**

```html
<!doctype html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Without Vue-CLI to build project</title>
</head>
<body>
  <div id="root"></div>
</body>
</html>
```

## 编写命令

打开`package.json`文件，我们编写执行打包的命令。

```json
{
  "script": {
    "start": "webpack-dev-server --config ./webpack.config.js",
    "build": "webpack --config ./webpack.config.js"
  }
}
```

执行`npm start`，编译成功之后，打开浏览器输入`localhost:5000`，页面中会展示`App.vue`中的内容。

![Hello World](.\images\without_cli_to_build_project.png)

之后我们执行`npm run build`，看是否能构建成功。如果构建成功，会在根目录下生成一个`build`目录，里面就是我们打包的文件。

打包的项目是需要在服务器环境下运行，检测项目是否可以运行，我们可以安装一个工具来运行这个项目。

```bash
npm i -g http-server
cd build
http-server
```

全局安装 `http-server`依赖，然后进入到`build`目录，执行`http-server`。

之后会出现一段信息如下：

```bash
Starting up http-server, serving ./
Available on:
  http://192.168.1.5:8080
  http://127.0.0.1:8080
Hit CTRL-C to stop the server
```

我们按照提示打开`127.0.0.1:8080/index.html`，一样显示我们填写的内容的话，就说明谋稳台（粤语乱入）啊。