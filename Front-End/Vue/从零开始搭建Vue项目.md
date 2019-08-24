[TOC]

# 从零开始搭建Vue项目

## 初始化项目

创建项目的根目录，命名为`CustomVueProject`。之后进入到目录中，执行`npm init -y`。

```bash
mkdir CustomVueProject
cd CustomVueProject
npm init -y
```

## 安装依赖

### webpack系列

项目使用`webpack`工具进行打包，需要安装`webpack`、`webpack-cli`、`webpack-dev-server`这三个依赖。

```bash
npm i -D webpack webpack-cli webpack-dev-server
```

### Babel系列

我们需要安装babel的依赖，来处理ES5版本以上的JS代码。

```bash
npm i -D bable-laoder @babel/core @babel/preset-env
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

### 图片和字体系列

需要安装两个依赖：`url-loader`、`file-loader`。

```bash
npm i -D url-loader file-loader
```



