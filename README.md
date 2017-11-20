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

## 11.18-1 英雄编辑器

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

## 11.18-2.主从结构

1.创建英雄列表

```
const HEROES: Hero[] = [
  { id: 11, name: 'Mr. Nice' },
  { id: 12, name: 'Narco' },
  { id: 13, name: 'Bombasto' },
  { id: 14, name: 'Celeritas' },
  { id: 15, name: 'Magneta' },
  { id: 16, name: 'RubberMan' },
  { id: 17, name: 'Dynama' },
  { id: 18, name: 'Dr IQ' },
  { id: 19, name: 'Magma' },
  { id: 20, name: 'Tornado' }
];
```

2.暴露英雄以供绑定`heroes = HEROES;`

3.在模板中显示英雄

```
<h2>My Heroes</h2>
<ul class="heroes">
  <li>
    <!-- each hero goes here -->
  </li>
</ul>
```

4.通过 ngFor 来显示英雄列表

```
<li *ngFor="let hero of heroes">
```

> ngFor的*前缀表示<li>及其子元素组成了一个主控模板。

> ngFor指令在AppComponent.heroes属性返回的heroes数组上迭代，并输出此模板的实例。

> 引号中赋值给ngFor的那段文本表示“从heroes数组中取出每个英雄，存入一个局部的hero变量，并让它在相应的模板实例中可用”。

> 要学习更多关于ngFor和模板输入变量的知识，参见[显示数据](https://angular.cn/guide/displaying-data)一章的[用*ngFor显示数组属性](https://angular.cn/guide/displaying-data#ngFor)和 [模板语法](https://angular.cn/guide/template-syntax)章的[ngFor](https://angular.cn/guide/template-syntax#ngFor)。

5.选择英雄

处理点击事件

```
<li *ngFor="let hero of heroes" (click)="onSelect(hero)">
  ...
</li>
```

添加一个onSelect方法，用于将用户点击的英雄赋给selectedHero属性。

```
onSelect(hero: Hero): void {
  this.selectedHero = hero;
}
```

替换hero为selectedHero，修改模板绑定到新的selectedHero属性

```
<h2>{{selectedHero.name}} details!</h2>
<div><label>id: </label>{{selectedHero.id}}</div>
<div>
    <label>name: </label>
    <input [(ngModel)]="selectedHero.name" placeholder="name"/>
</div>
```

使用 ngIf 隐藏空的详情

```
<div *ngIf="selectedHero">
  <h2>{{selectedHero.name}} details!</h2>
  <div><label>id: </label>{{selectedHero.id}}</div>
  <div>
    <label>name: </label>
    <input [(ngModel)]="selectedHero.name" placeholder="name"/>
  </div>
</div>
```

给所选英雄添加样式

```
<li *ngFor="let hero of heroes"
  [class.selected]="hero === selectedHero"
  (click)="onSelect(hero)">
  <span class="badge">{{hero.id}}</span> {{hero.name}}
</li>
```

## 11.19 1.多个组件

### 1.制作英雄详情组件

往app/文件夹下添加一个名叫hero-detail.component.ts的文件。这个文件中会存放这个新的HeroDetailComponent。

文件名和组件名遵循[风格指南](https://angular.cn/guide/styleguide#naming)中的标准方式。

* 组件的类名应该是大驼峰形式，并且以Component结尾。 因此英雄详情组件的类名是HeroDetailComponent。
* 组件的文件名应该是小写中线形式，每个单词之间用中线分隔，并且以.component.ts结尾。 因此HeroDetailComponent类应该放在hero-detail.component.ts文件中。

HeroDetailComponent的代码如下：

***app/hero-detail.component.ts (initial version)***

```
import { Component } from '@angular/core';

@Component({
  selector: 'hero-detail',
})
export class HeroDetailComponent {
}
```

### 2.英雄详情的模板

把英雄详情的视图移入HeroDetailComponent，把对应的selectedHero改为hero

### 3.添加Hero属性

在***hero-detail.component.ts***文件中添加`hero: Hero;`属性。

创建hero.ts，把Hero类移出。

在`app.component.ts`和`hero-detail.component.ts`中导入Hero

```
import { Hero } from './hero';
```

### 4.hero属性是一个***输入***属性

在***src/app/app.component.html***的绑定如下:

```
<hero-detail [hero]="selectedHero"></hero-detail>
```

在等号的左边，是方括号围绕的hero属性，这表示它是属性绑定表达式的目标。 我们要绑定到的目标属性必须是一个输入属性，否则Angular会拒绝绑定，并抛出一个错误。

首先，修改@angular/core导入语句，使其包含符号Input。

***src/app/hero-detail.component.ts (excerpt)***

```
import { Component, Input } from '@angular/core';
```

然后，通过在hero属性前面加上@Input装饰器，来表明它是一个输入属性。

***src/app/hero-detail.component.ts (excerpt)***

```
@Input() hero: Hero;
```

### 5.在AppModule中声明HeroDetailComponent

每个组件都必须在一个（且只有一个）Angular模块中声明。

打开app.module.ts并且导入HeroDetailComponent，以便我们可以引用它。

***src/app/app.module.ts***

```
import { HeroDetailComponent } from './hero-detail.component';
```

把HeroDetailComponent添加到该模块的declarations数组中。

***src/app/app.module.ts***

```
declarations: [
  AppComponent,
  HeroDetailComponent
],
```

### 6.把HeroDetailComponent添加到AppComponent中

把<hero-detail>元素添加到AppComponent模板的底部，那里就是英雄详情视图所在的位置。

***app.component.ts (excerpt)***

```
<hero-detail [hero]="selectedHero"></hero-detail>
```

## 11.20.1.坑了我一小时的bug

```
Jason-Yu-MJLU2:angular-tour-of-heroes yufan$ npm start

> angular-quickstart@1.0.0 prestart /Users/yufan/STUDY/remote proj/Angular-notebook/angular/2.tutorial/angular-tour-of-heroes
> npm run build


> angular-quickstart@1.0.0 build /Users/yufan/STUDY/remote proj/Angular-notebook/angular/2.tutorial/angular-tour-of-heroes
> tsc -p src/

src/app/app.component.ts(95,25): error TS2304: Cannot find name 'Void'.
npm ERR! code ELIFECYCLE
npm ERR! errno 2
npm ERR! angular-quickstart@1.0.0 build: `tsc -p src/`
npm ERR! Exit status 2
npm ERR! 
npm ERR! Failed at the angular-quickstart@1.0.0 build script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/yufan/.npm/_logs/2017-11-20T13_38_17_141Z-debug.log
npm ERR! code ELIFECYCLE
npm ERR! errno 2
npm ERR! angular-quickstart@1.0.0 prestart: `npm run build`
npm ERR! Exit status 2
npm ERR! 
npm ERR! Failed at the angular-quickstart@1.0.0 prestart script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /Users/yufan/.npm/_logs/2017-11-20T13_38_17_162Z-debug.log
```

接触angular一周就遇到了npm start失败，google了好多方法都不管用，仔细看了log三遍，在第三遍注意到了这一行`src/app/app.component.ts(95,25): error TS2304: Cannot find name 'Void'.
`，在文件中找到了Void的位置，改为void，解决/(ㄒoㄒ)/~~

> mark：
> 
> 用的mac本，周末两天没关电脑，这个bug在`npm start`服务运行中没有导致崩溃或者其他问题，今早关了服务，晚上再开启才发现这个问题。

## 11.20.2.服务

### 1.创建服务

***src/app/hero.service.ts
```
import {Injectable} from '@angular/core';

@Injectable()
export class HeroService {}
```

### 2.获取数据

将HEROES常量从`app.component.ts`中剪切粘贴到`mock-heroes.ts`

***src/app/mock-heroes.ts***

```
import { Hero } from './hero';
 
export const HEROES: Hero[] = [
  { id: 11, name: 'Mr. Nice' },
  { id: 12, name: 'Narco' },
  { id: 13, name: 'Bombasto' },
  { id: 14, name: 'Celeritas' },
  { id: 15, name: 'Magneta' },
  { id: 16, name: 'RubberMan' },
  { id: 17, name: 'Dynama' },
  { id: 18, name: 'Dr IQ' },
  { id: 19, name: 'Magma' },
  { id: 20, name: 'Tornado' }
];
```

并修改`app.component.ts`中的heroes

```
  heroes: Hero[];
```

### 3.在hero.service.ts中返回英雄数据

```
import { Injectable } from '@angular/core';

import { Hero } from './hero';
import { HEROES } from './mock-heroes';

@Injectable()
export class HeroService {
  getHeroes(): Hero[] {
    return HEROES;
  }
}
```

### 4.注入HeroService

```
import { HeroService } from './hero.service';

@Component({
  ...
  providers: [HeroService]
})

export class AppComponent {
  ...
  constructor(private heroService: HeroService) { }
  
  getHeroes(): void {
    this.heroes = this.heroService.getHeroes();
  }
  ...
```

### 5.ngOnInit生命周期钩子

只要我们实现了 Angular 的 ngOnInit 生命周期钩子，Angular 就会主动调用这个钩子。 Angular提供了一些接口，用来介入组件生命周期的几个关键时间点：刚创建时、每次变化时，以及最终被销毁时。

添加`OnInit`接口的实现

```
export class AppComponent implements OnInit {
  ngOnInit(): void {
    this.getHeroes();
  }
}
```

### 6.异步服务与承诺

> 这里只是粗略说说，要了解更多 ES2015 Promise 的信息，见[ES6概览](http://http//exploringjs.com/es6.html)中的[承诺与异步编程](http://exploringjs.com/es6/ch_promises.html)。

把HeroService的getHeroes方法改写为返回承诺的形式：

***src/app/hero.service.ts (excerpt)***

```
getHeroes(): Promise<Hero[]> {
  return Promise.resolve(HEROES);
}
```

修改HeroService之后，this.heroes会被赋值为一个Promise而不再是英雄数组。

我们得修改这个实现，把它变成基于承诺的，并在承诺的事情被解决时再行动。 一旦承诺的事情被成功解决（Resolve），我们就会显示英雄数据。

我们把回调函数作为参数传给承诺对象的then方法：

***src/app/app.component.ts (getHeroes - revised)***

```
getHeroes(): void {
  this.heroService.getHeroes().then(heroes => this.heroes = heroes);
}
```

> 回调中所用的 ES2015 箭头函数 比等价的函数表达式更加简洁，能优雅的处理 this 指针。

在回调函数中，我们把服务返回的英雄数组赋值给组件的heroes属性。

模拟慢速链接:

```
getHeroesSlowly(): Promise<Hero[]> {
  return new Promise(resolve => {
    setTimeout(() => resolve(this.getHeroes()), 2000);
  }
}
```

> 问题:
> 
> 不知道为什么，跟着教程走，像这种报错我从来不会遇到，明明和教程是完全一样的步骤。先记下来，以后研究。
> 
> ```
> EXCEPTION: No provider for HeroService! (AppComponent - HeroService)
> ```


