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

### 1.设置开发环境

先安装node.js(已安装)，然后全局安装 [Angular CLI](https://github.com/angular/angular-cli) 。

```
npm install -g @angular/cli
```

### 2.创建新项目

```
ng new my-app
```

### 3.启动开发服务器
进入项目目录，并启动服务器。
```
cd my-app
ng serve --open
```

`ng serve`命令会启动开发服务器，监听文件变化，并在修改这些文件时重新构建此应用。

使用--open（或-o）参数可以自动打开浏览器并访问http://localhost:4200/。

## 11.18

开始撸[英雄编辑器](https://angular.cn/tutorial/toh-pt1)

### 1.搭建本地开发环境

利用 [github 上的《快速上手》种子](https://github.com/angular/quickstart)在你的电脑上搭建一个新项目是很快很容易的。

#### 克隆并启动

```
git clone https://github.com/angular/quickstart.git quickstart
cd quickstart
npm install
npm start
```

`npm start`这个命令会在“监听”模式下运行TypeScript编译器，当代码变化时，它会自动重新编译。 同时，该命令还会在浏览器中启动该应用，并且当代码变化时刷新浏览器。

#### 删除非必需文件（可选）

```
xargs rm -rf < non-essential-files.osx.txt
rm src/app/*.spec*.ts
rm non-essential-files.osx.txt
```

### 2.显示

#### 插值表达式显示组件属性

要显示组件的属性，最简单的方式就是通过插值表达式 (interpolation) 来绑定属性名。 要使用插值表达式，就把属性名包裹在双花括号里放进视图模板，如`{{myHero}}`。

    模板是包在 ECMAScript 2015 反引号 (`) 中的一个多行字符串。 反引号 (`) — 注意，不是单引号 (') — 允许把一个字符串写在多行上， 使 HTML 模板更容易阅读。
    
注意，我们没有调用 new 来创建AppComponent类的实例，是 Angular 替我们创建了它。那么它是如何创建的呢？

注意@Component装饰器中指定的 CSS 选择器selector，它指定了一个叫my-app的元素。 该元素是index.html的body里的占位符。

***src/index.html (body)***

```
 content_copy
<body>
  <app-root></app-root>
</body>
```

当我们通过main.ts中的AppComponent类启动时，Angular 在index.html中查找一个<my-app>元素， 然后实例化一个AppComponent，并将其渲染到<my-app>标签中。

### 3.编辑名字(双向绑定)

把模板中的英雄名字重构成这样：

***src/app/app.component.ts***

```
<div>
  <label>name: </label>
  <input [(ngModel)]="hero.name" placeholder="name">
</div>
```

[(ngModel)]是一个Angular语法，用与把hero.name绑定到输入框中。 它的数据流是双向的：从属性到输入框，并且从输入框回到属性。

不幸的是，做了这项改动之后，我们的程序崩溃了。 打开浏览器的控制台，我们会看到Angular抱怨说：“ngModel ... isn't a known property of input.”（ngModel不是input元素的已知属性）

虽然NgModel是一个有效的Angular指令，但它默认情况下却是不可用的。 它属于一个可选模块FormsModule。 我们必须选择使用那个模块。

#### 导入 FormsModule

打开app.module.ts文件，并且从@angular/forms库中导入符号FormsModule。 然后把FormsModule添加到@NgModule元数据的imports数组中，它是当前应用正在使用的外部模块列表。

修改后的AppModule是这样的：

***app.module.ts (FormsModule import)***

```
import { NgModule }      from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule }   from '@angular/forms'; // <-- NgModel lives here
 
import { AppComponent }  from './app.component';
 
@NgModule({
  imports: [
    BrowserModule,
    FormsModule // <-- import the FormsModule before binding with [(ngModel)]
  ],
  declarations: [
    AppComponent
  ],
  bootstrap: [ AppComponent ]
})
export class AppModule { }
```