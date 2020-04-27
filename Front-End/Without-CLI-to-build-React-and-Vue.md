# 从零开始搭建React、Vue项目

## 简要

本文默认读者熟悉ES6，熟悉npm的操作，以及熟悉React或者Vue的使用，并且使用过两者之一的脚手架搭建过项目，但对如何摒弃CLI搭建项目不清楚、不熟悉的开发者。如果你是老鸟可以关闭这个标签页了（手动狗头），当然，欢迎任何人提出针对改进的意见。

## 创建项目目录

使用命令行创建或者手动创建目录。在目录中执行npm初始化操作。

```bash
mkdir react-template && cd react-template
npm init -y
```

## 安装webpack

我们给项目本地添加webpack的依赖，在命令行中输入：

```bash
npm i -D webpack webpack-cli webpack-dev-server
```

- `webpack`：webpack的核心依赖包。
- `webpack-cli`：在webpack 4中，webpack的命令行功能已被单独分离到这里。
- `webpack-dev-server`：在项目开发时所需的本地server依赖包。

安装完`webpack`依赖之后，我们创建`webpack`的配置文件`webpack.config.js`，然后写些简单的配置：

```javascript
const path = require('path')

module.exports = {
  output: {
    path: path.resolve(__dirname, './dist'), // path 文件输出的路径，必须是绝对路径
    filename: 'bundle.js' // filename 对应entry而生成的文件名
  },
  module: {
    rules: [
      {
        test: /\.js$/,  // 凡是以js后缀结尾的文件
        use: 'babel-loader'  // 给它用babel-loader转译
      }
    ]
  }
}
```

## 安装babel

项目需要使用babel工具来对JS代码进行转换，因此我们需要安装babel的相关依赖：

```bash
npm i -D @babel/core @babel/preset-env @babel/preset-react @babel/plugin-transform-runtime babel-loader

npm i @babel/runtime-corejs3
```

- `@babel/core`：如其名，这是babel的核心代码包。
- `@babel/preset-env`：`env`依赖包支持把ES6+也就是已经形成标准的而不是提案的JS特性转换成ES5。
- `@babel/preset-react`：这是用于转换JSX语法的，适用于react项目。这个项目包含了`@babel/plugin-syntax-jsx`、`@babel/plugin-transform-react-jsx`、`@babel/plugin-transform-react-display-name`这三个依赖包。

安装完依赖之后，我们在项目根目录创建一个`babel.config.json`的文件，这是babel转译代码所需的配置文件，我们填写如下配置：

```json
{
  "plugins": [
    ["@babel/plugin-transform-runtime", {
      "corejs": 3
    }]
  ],
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

> `presets`预设，执行顺序是**从右至左**；`plugins`插件，在预设之前运行，自身执行顺序是**从左至右**。

现在，来测试一下我们目前为止所做的是否正确，创建`src`目录，并在该目录下创建`index.js`，在里面写一些代码来测试一下：

```javascript
const greeting = 'just hi.'

class Person {
  constructor() {
    this.name = 'Coolman'
  }

  sayHi () {
    console.log(`${greeting}`)
  }

  sayName: () => {
    console.log(`My name is ${this.name}`)
  }
}
```

在根目录下找到`package.json`，打开并找到`scripts`中的`test`命令，将其改写为如下代码：

```json
"scripts": {
  "start": "webpack"
}
```

在命令行中执行：
```bash
npm start
```

然后就会执行`package.json`中的`start`命令，而`start`命令又执行`webpack`让其按照`webpack.config.json`中的配置工作。一切执行完之后，根目录下多了一个`dist`的文件夹，里面有一个`bundle.js`的文件，而这，就是我们在`webpack.config.js`中做的配置输出。

> 大家都知道`webpack`有个很关键的`entry`入口配置，为什么没有写呢？原因是`entry`有默认值的，即`src/index.js`，后面多入口页会写到。


