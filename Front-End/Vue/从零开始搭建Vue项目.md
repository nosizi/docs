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

### 图片和字体系列

需要安装两个依赖：`url-loader`、`file-loader`。

```bash
npm i -D url-loader file-loader
```

### HTML系列

安装`html-webpack-plugin`插件，这个插件会自动生成html文件，当然，也可以指定模版生成。

```bash
npm i -D html-webpack-plugin
```



