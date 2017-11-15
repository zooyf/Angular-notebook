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

### 学习路径
![](angular学习路径.png)

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

本人习惯使用sublime编辑器，先用sublime新建一个greeter.ts的文件，敲代码，发现没有颜色，好不习惯，下载插件[TypeScript-Sublime-Plugin](https://github.com/Microsoft/TypeScript-Sublime-Plugin)。发现这里有好多快捷键，先不管了，留下以后看，继续5 minutes.

```
cd ~/"Library/Application Support/Sublime Text 2/Packages"
git clone --depth 1 https://github.com/Microsoft/TypeScript-Sublime-Plugin.git TypeScript
```

#### 小结

跟着教程完成了五分钟上手TypeScript，加上写笔记总共花掉了将近一个小时，要加快速度了。

编辑器根据个人喜好，我喜欢用sublime记东西，敲代码还是喜欢集成开发环境，想尝试下vscode，毕竟ts也是微软自家的东西，应该会更好用吧。找到一篇博客:[vscode+typescript环境搭建](http://blog.wolksoftware.com/setting-up-your-typescript-vs-code-development-environment)，抽空再看。

## 11.15

今天杂七杂八忙活完22点了，看一下[angular-快速上手](https://angular.cn/guide/quickstart)。

昨天把npm下载了，今天过程很顺利，照着教程超快速撸完。