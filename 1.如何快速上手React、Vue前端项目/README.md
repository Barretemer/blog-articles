## 前言
想必有不少前端的小伙伴在拿到一个前端开源项目或者新的项目的时候会有点手足无措，六神无主。这篇文章主要是为那些准备上手常见的前端项目提供思路。

## 问题
1. 当自己拿到一个新的项目的时候如何去快速上手？
2. 如何快速了解项目中的技术栈？
3. 如何深入了解项目中的脚手架实现？

## 核心
- 确定把握项目中所用到的技术栈
- 了解使用对应的npm依赖包

## 开始了解项目
这里全程以[ant-design-pro项目](https://github.com/ant-design/ant-design-pro)为例子

### 1. 查看项目中的README.md文档
README.md文档就是该项目的说明文档，一般放置在项目的根目录下。在该文档中往往蕴含着项目构建者对该项目的描述（Introduction，Features，Usage， License...），通过该文档可以快速了解项目的技术栈，如何构建等信息。

### 2. 查看项目的package.json，确定项目的技术栈
package.json文件，定义了这个项目所需要的各种npm依赖，以及项目的配置信息。运行*npm install* 命令会根据这个文件下载对应的npm依赖包。
常见的package.json字段（可对照后面的package.json代码查看）
1. **name**字段  项目名称
2. **version**字段 项目版本号
3. **description**字段 项目描述
4. **author**字段 项目作者
5. **scripts**字段 指定运行脚本命令的npm。 例如npm run start会执行scripts下的start字段里面的命令。
6. **dependencies**字段 指定了项目运行所依赖的模块以及对应的版本号
7. **devDependencies**字段 指定项目开发所需要的模块以及对应的版本号
8. **engines**字段 规定该模块运行的平台
9. **browserslist**字段 规定项目兼容的浏览器平台

注：还会有更多其他的字段，如果需要了解，则直接在google搜索对应额字段则知道该字段的作用。

#### 重点解析：
- scripts字段： 该字段主要作用是指定运行的脚本命令。常用的脚本命令类型有：1、项目在本地运行命令；2、项目构建编译生产需要的文件命令；3、测试脚本运行命令；4、代码规范校验命令。
- dependencies字段、devDependencies字段：该字段能够确定项目中所用的技术栈，以确定自己是否熟悉该技术栈（项目中所有所用的npm包都应该知道其作用）。常见的技术栈主要有以下几部分组成：（框架）+ （JS编写语言）+（样式表预处理器语言）+（UI框架）+（项目构建工具）+ （数据流工具）

#### 常见的技术栈（根据dependencies字段，devDependencies字段确定项目的技术栈）
- 框架： React、Vue、Angular
- JS编写语言：TypeScript、ES6、CoffeeScript
- 样式表预处理器语言：Stylue、LESS、SASS
- UI框架：Antd、Element、Bootstrap...(比较多)
- 
- 项目构建工具：Webpack、Grunt、Gulp
eg:
```
{
  "name": "ant-design-pro",
  "version": "2.2.1",
  "description": "An out-of-box UI solution for enterprise applications",
  "private": true,
  "scripts": {
    "start": "cross-env APP_TYPE=site umi dev",
    "build": "umi build",
    "lint-staged": "lint-staged",
    "test": "umi test",
    "prettier": "node ./scripts/prettier.js"
  },
  "dependencies": {
    "@antv/data-set": "^0.10.1"
  },
  "devDependencies": {
    "@types/react": "^16.8.1"
  },
  "engines": {
    "node": ">=8.0.0"
  },
  "browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 10"
  ]
}
```

### 3. 搞清楚项目的目录结构
如果脚手架为开源脚手架的话，在github上会找到对应的说明。要判断该脚手架是否为开源脚手架，请按照第一二步骤来确定。
#### 常见的目录结构
- **config** 项目的配置文件，常见的配置文件有：构建工具配置文件、环境变量配置文件、路由配置文件、还有其他的npm包的配置文件
- **mock** mockJs的文件放置目录。模拟用户接口请求的返回数据
- **tests** 自动化测试脚本文件放置目录
- **src** 代码的源文件目录
- **src > components** Vue、React组件封装目录
- **src > utils** 公共文件放置目录
- **src > services** ajax接口收口
- **src > assets** 静态资源文件目录

### 4. 找准项目的入口文件
项目的入口文件的文件名一般为：main.js、app.js、index.js等。入口文件都放置于src文件夹目录下（具体应该查看对应的项目构建工具配置）。这个文件一般会引用全局用到的npm依赖包，路由文件，重置样式文件，全局样式文件...

注：有些项目里面找不到这些入口文件怎么办？那就要看看项目中使用的脚手架了，有些脚手架（例如：Nuxt.js）会直接帮你自动生成该文件（这里就不讨论优劣了）

### 5. 找到项目的路由文件
路由文件可以准确的找到哪个页面对应着哪个组件，这个文件在我们以后写业务的时候经常会修改到。我们可以根据URL上的路由来根据路由文件查找对应的组件文件。路由文件可以多种多样，总体来说应该是一个路由对应着一个组件，根据路由可以找到对应的组件文件进行代码修改。同样，自己需要添加页面时，也需要首先在这个页面进行路由声明，才能访问对应的路由显示出对应的页面组件。

注：有些项目里面找不到这些路由文件怎么办？那就要看看项目中使用的脚手架了，有些脚手架（例如：Nuxt.js）会直接帮你自动生成该文件

eg: 
```
export default [
  // user
  {
    path: '/user',
    component: '../layouts/UserLayout',
    routes: [
      { path: '/user', redirect: '/user/login' },
      { path: '/user/login', component: './User/Login' },
      { path: '/user/register', component: './User/Register' },
      { path: '/user/register-result', component: './User/RegisterResult' },
    ],
  }
]
```
### 6. 模仿组件做一个TODO list
入门一个语言最经典的是Hello World.而上手一个项目的最好的应该是做一个todo list了吧。如果可以写出对应的todo list的增删改查，基本上能够在该项目进行基本的业务编写。

基本步骤：
1. 在页面文件夹中新建对应的组件；
2. 在路由文件中添加对应的路由（有些脚手架会自动帮你生成，不用自己手动添加）；

## 总结

![总结](https://user-gold-cdn.xitu.io/2019/2/17/168fb26fb80903ef?w=2654&h=1038&f=png&s=285683)

## 进阶
作为一条咸鱼，仅仅是会用该项目中的脚手架来写项目是远远不够的。应该要了解脚手架的使用，并且要跟着设计者的思路，自己能够打造一个类似的脚手架。接下来会介绍如何打造一个属于自己的脚手架的基本思路。
