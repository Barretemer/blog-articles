## 前言
本人原为React开发者，现在转战Vue。在这些天接触Vue的日子里，说说自己的感觉：同样的登山活动，React就像父亲，给你必要的登山工具就让你出发了；Vue就像母亲，在你登山之前为你准备好了所有东西，唠唠叨叨了一波，规划了路线，给了你厚厚的导航指南，才让你出发。

## 本文目的
- 方便React开发者更快的上手Vue
- 进行更加详尽的React以及Vue的开发体验比较

## 目标人群
有一定的React开发经验，正在并行使用Vue的开发者

## 问题
1. Vue的模板跟React中使用的jsx有什么区别？
2. 如何在React中实现Vue模板上带有的功能？

## vue模板与JSX比较

###  1. 表达式（expressions）
JSX表达式用{}包裹，vue模板表达式用{{}}包裹，其余一致.

vue模板表达式：
![表达式](https://user-gold-cdn.xitu.io/2019/2/19/16905093775388db?w=1126&h=376&f=jpeg&s=46841)

代码比较：

```

<!--vue-->
<template>
    <div>
      <p>I have a {{ product }}</p>
      <p>{{ product + 's' }}</p>
      <p>{{ isWorking ? 'YES' : 'NO' }}</p>
      <p>{{ product.getSalePrice() }}</p>
    </div>
</template>

<!--react-->
<div>
    <p>I have a { product }</p>
    <p>{ product + 's' }</p>
    <p>{ isWorking ? 'YES' : 'NO' }</p>
    <p>{ product.getSalePrice() }</p>
</div>
```

### 2.指令（directives）
Vue模板：小伙子，用你的头发记好了，有如下指令：

Vue模板指令：
![Vue模板指令](https://user-gold-cdn.xitu.io/2019/2/19/169050ebbea178f9?w=1066&h=542&f=jpeg&s=58442)
JSX：啥啥啥，你自己实现不就好了吗。。。
- v-if, v-else-if, v-else JSX直接用万能的三元表达式
- v-show JSX在dom上添加如下代码，实现一样的功能
```
style={{ display: ifShow ? 'block' : 'none' }}
```
- v-model JSX在对应的dom上绑定事件,事件里面自己爱怎么处理怎么处理

代码比较：
```
<!--vue指令-->
  <template>
    <div>
      <p v-if="container1">你现在看到container1了</p>
      <p v-else-if="container2">你现在看到container2了</p>
      <p v-else>你现在看到default了</p>
      <p v-show="ifShow">影响显示的p</p>
      <input type="text" v-model="inputText"/>
    </div>
  </template>
  
  <!--react指令-->
  <div>
    {
      container1 ?
        <p>你现在看到container1了</p> :
        container2 ?
          <p>你现在看到container2了</p> :
        <p>你现在看到default了</p>
    }
    <p style={{display: ifShow ? 'block' : 'none'}}></p>
    <input type="text" onChange={val => () => {this.setState{inputText:val}}} 
           value={this.state.inputText}/>
  </div>
```

### 3. 列表渲染（list rendering）
Vue模板列表渲染：v-for
JSX: 直接在dom中插入map函数，里面直接用js来处理参数

```
<!--vue-->
  <template>
    <ul>
      <li v-for="(item, i) in list" :key="item.id">{{item.text}}</li>
    </ul>
  </template>
  
  <!--react-->
  <div>
    <ul>
      {
        list.map((item, i) => <li key={item.id}>{item.text}</li>)
      }
    </ul>
  </div>
  ```
### 4. 事件处理（actions/events）
Vue模板：记住了，有以下事件处理

![Vue模板事件处理](https://user-gold-cdn.xitu.io/2019/2/19/16905348334c0d8b?w=1240&h=1370&f=png&s=134258)
JSX：跟js事件名称一致，直接放置在对应的节点进行事件绑定就好

```
<!--vue-->
  <template>
    <button v-on:click="handleBtn">我是一个点击按钮</button>
  </template>
  
  <!--react-->
  <div>
    <button onClick={this.handleBtn}>我是一个点击按钮</button>
  </div>
  ```
## 总结
Vue模板与JSX的基本使用比较完了，Vue模板为你考虑了很多优化的东西，你只需要记住其中的规则就好，更大的降低了技术门槛。而JSX将更大的控制权留给了代码编写者。
