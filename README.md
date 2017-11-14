# Angular-notebook

## 简介

本人16年计算机科学与技术专业 本科毕业，iOS开发两年+，随着移动互联网的没落，准备转型前端。大学学过web开发选修课，没敲过太多代码，对前端已经没什么印象了，可以说是从零开始吧。2017.11.14开始学习使用Angular框架，在git上记录下学习笔记。

#### 操作环境

* mac OS

## 11.14

### 1. Angular学习清单

#### 两个语言

* 《JavaScript权威指南》

* [TypeScript](https://tslang.cn/): 官网+书籍

#### 一个框架

* [Angular](https://angular.cn/)：官网+书籍

### 2. [五分钟上手TypeScript](https://tslang.cn/docs/handbook/typescript-in-5-minutes.html)

#### 安装

TypeScript需要通过npm来安装，在terminal中输入npm提示`-bash: npm: command not found`，google了下`npm install`发现npm的[最佳安装方法](http://blog.npmjs.org/post/85484771375/how-to-install-npm)是安装node.js。遂安装node.js:

```
$ brew update
$ brew uninstall node
$ brew install node
$ brew postinstall 
```

安装完成，输入以下命令，确保npm是最新版本

```
sudo npm install npm -g
```

最后安装TypeScript:

```
$ npm install -g typescript
```

#### 第一个TypeScript文件

本人使用sublime编辑器

