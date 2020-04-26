# 从零开始搭建React、Vue项目

## 简要

本文默认读者熟悉ES6，熟悉npm的操作，以及熟悉React或者Vue的使用，并且使用过两者之一的脚手架搭建过项目，但对如何摒弃CLI搭建项目不清楚、不熟悉的开发者。如果你是老鸟可以关闭这个标签页了（手动狗头），当然，欢迎任何人提出针对改进的意见。

## 创建项目目录

使用命令行创建或者手动创建目录。在目录中执行npm初始化操作。

```
mkdir react-template && cd react-template
npm init -y
```

## 安装webpack

我们给项目本地添加webpack的依赖，在命令行中输入：

```
npm i -D webpack webpack-cli webpack-dev-server
```

- `webpack`：webpack的核心依赖包。
- `webpack-cli`：在webpack 4中，webpack的命令行功能已被单独分离到这里。
- `webpack-dev-server`：在项目开发时所需的本地server依赖包。

## 安装babel

项目需要使用babel工具来对JS代码进行转换，因此我们需要安装babel的相关依赖：

```
npm i -D @babel/core @babel/preset-env @babel/preset-react @babel/plugin-transform-runtime

npm i @babel/runtime-corejs3
```

- `@babel/core`：如其名，这是babel的核心代码包。
- `@babel/preset-env`：`env`依赖包支持把ES6+也就是已经形成标准的而不是提案的JS特性转换成ES5。
- `@babel/preset-react`：这是用于转换JSX语法的，适用于react项目。这个项目包含了`@babel/plugin-syntax-jsx`、`@babel/plugin-transform-react-jsx`、`@babel/plugin-transform-react-display-name`这三个依赖包。

安装完依赖之后，我们在项目根目录创建一个`babel.config.js`的文件，这是babel转译代码所需的配置文件，我们填写如下配置：
