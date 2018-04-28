---
title: react-router 传参注意事项
date: 2018-04-28 13:19:31
tags: [前端, react-router]
---
主要是介绍一下react-router注册路由的这两种写法，在传递参数时的区别。
```
<Route path="/changzhu" component={() => <Changzhu />} />
<Route path="/changzhu" component={Changzhu} />
```

遇到这个问题的起因，是在抽离地块部分二级菜单组件的时候，考虑到组件的通用性，设想今后可能会有**点击Link时，将数据通过Link传入路由渲染的组件**这一需求，决定将留出路由传递参数的接口。
<!--more-->

## react-router传参方式
react-router传参的方法简单来说有2种：
1. 在路由注册中指定参数
```
<Route path='/user/:name' component={UserPage}></Route>
```
这种在组件内可以通过`this.props.params.name`来获取。

2. 通过query或者state来传参
```
<Route path='/user' component={UserPage}></Route>
```
正常注册路由，通过Link传递参数
```
<Link to={{
	pathname: '/user',
	query: data
}}>用户</Link>

<Link to={{
	pathname: '/user',
	state: data
}}>用户</Link>
```
然后再组件中通过`this.props.location.query`或者`this.props.location.state`来获取数据。

## 需要注意事项
通过方式2能很简单的用props方法获取参数，但是在项目中却遇到了问题。
```
<Route path="/changzhu" component={() => <Changzhu />} />

<Link to={{ 
	pathname: item.link, 
	state: { data: item.link } 
}}>{item.name}</Link>
```
在`<Changzhu />`组件里面怎么也找不到`this.props.location`属性，最后在chrome的React DevTool发现了问题。

原来是因为在注册路由时通过`component={() => <Changzhu />} `这种写法，导致`<Changzhu />`组件外面其实包裹了一层无状态组件component，传递的参数到这里丢失了=。=
![Alt text](https://i.loli.net/2018/04/28/5ae406fa18c39.png)
将注册路由修改为`<Route path="/changzhu" component={Changzhu} />`之后，问题解决！
![Alt text](https://i.loli.net/2018/04/28/5ae4071c21837.png)

哈哈哈哈，以前这两种写法都很随意，今后如何选择需要注意咯！