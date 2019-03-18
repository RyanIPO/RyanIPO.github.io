---
title: npm install -g -S -D的区别
key: 20180105
tags: npm
---


`package.json` 中 `dependencies` 下是生产环境需要的依赖，`devDependencies` 下是开发时需要的依赖。

两者都会被下载安装，区别在于前者用于生产环境，后者用于开发环境

npm install
{:.info}

什么都不加也会安装，但是不会加至 `package.json` 中

#### `-g` 表示全局安装，通常用于安装脚手架等工具

全局安装；例：vue-cli , webpack-cli...

#### `--save`(-S) 表示本地安装，会被加至 dependencies 部分

项目（运行时、发布到生产环境时）依赖；例：antd , element,react...

#### `--save-dev`(-D) 表示本地安装，会被加至 devDependencies 部分

工程构建（开发时、“打包”时）依赖 ；例：xxx-cli , less-loader , babel-loader...


