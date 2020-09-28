---
title: react-router4.0 路由传参跳转及获取参数
date: 2019-04-15 23:00:00
categories:
  - 'react'
  - 'react-router'
tags:
  - 'react'
  - 'react-router'
copyright: true
---

## Router相关的属性有哪些？

- `history `
- `location`
- `match`

`react-router-dom` 提供一个`withRouter`高阶组件，可以将这三个属性当成`props`传入组件中使用

##Router 如何跳转？

1. `react-router-dom`中提供一个`Link`组件可以当成`a`链接使用，但是这个是用来单页应用的路由跳转的
2. `js`的路由跳转是通过`history`这个对象来跳转的，其中提供了很多种跳转方法

## Router 跳转传参有哪些方式？

- ### params

  ```react
  <Route path='/path/:name' component={Component}/>
  <Link to="/path/hht">xxx</Link>
  this.props.history.push({pathname:"/path/" + name});
  ```

  读取参数：this.props.match.params.name

  优势：刷新地址栏，参数依然存在
  缺点：只能传字符串，并且，如果传的值太多的话，url会变得长而丑陋。

- ### query

  ```react
  <Route path='/path' component={Query}/>
  <Link to={{ path : '/path' , query : { name : 'sunny' }}}>
  this.props.history.push({pathname:"/path",query: { name : 'sunny' }});
  ```

  读取参数：this.props.location.query.name

  优势：传参优雅，传递参数可传对象；
  缺点：刷新地址栏，参数丢失

- ### state

  ```react
  <Route path='/path' component={Sort}/>
  <Link to={{ path : ' /path' , state : { name : 'sunny' }}}> 
  this.props.history.push({pathname:"/path",state : { name : 'sunny' }});
  ```

  读取参数：this.props.location.query.state

  优势：传参优雅，传递参数可传对象；
  缺点：刷新地址栏，参数丢失

- ### search

  ```react
  <Route path='/web/departManange' component={DepartManange}/>
  <link to="web/departManange?tenantId=12121212">xxx</Link>
  this.props.history.push({pathname:"/web/departManange?tenantId" + row.tenantId});
  ```

  读取参数用: this.props.location.search

  优势：刷新地址栏，参数依然存在
  缺点：只能传字符串，并且，如果传的值太多的话，url会变得长而丑陋。

## Hooks中如何使用Router

```react
import { useHistory,useLocation,useParams,useMatch } from 'react-router-dom';
let history = useHistory();
history.push('/')
```