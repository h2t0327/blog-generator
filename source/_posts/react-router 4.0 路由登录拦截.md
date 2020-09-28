---
title: react-router4.0 路由登录拦截
date: 2019-04-15 23:00:00
categories:
  - 'react'
  - 'react-router'
tags:
  - 'react'
  - 'react-router'
copyright: true
---

# react-router4.0 路由登录拦截

## 创建路由表
```react
const routers = [
  {path: "/", name: "Index", component: './pages/Index'},
  {path: "/login", name: "Login", component: './pages/Login'},
  {path: "/register", name: "Register", component: './pages/Register'},
  {path: "/my", name: "My", component: './pages/My', auth: true},
  {path: "/create", name: "Create", component: './pages/Create', auth: true},
  {path: "/detail/:blogId", name: "Detail", component: './pages/Detail', auth: true},
  {path: "/edit/:blogId", name: "Edit", component: './pages/Edit', auth: true},
  {path: "/user/:userId", name: "User", component: './pages/User', auth: true},
]
```

## 遍历路由表
```react
import React, {Component, Suspense, lazy} from 'react';
import {BrowserRouter as Router, Route, Switch, Redirect} from 'react-router-dom'
import routers from './router'
import {NotFound} from 'pages'
import {Page} from 'components'

class App extends Component {
  async componentWillMount() {
    await this.props.dispatch(authActions.getAuthInfo());
  }

  render() {
      return (
        <Router>
          <Switch>
            {
              routers.map((item, index) => {
                const DynamicComponent = lazy (() => import(`${item.component}/index`)); 
                return <Route key={index} path={item.path} exact render={props => (
                    <Page {...props}>
                      <Suspense fallback={<div>loading...</div>}>
                      {
                        !item.auth
                            ? (<DynamicComponent {...props} />)
                            : (token
                                ? (<DynamicComponent {...props} />)
                                : (<Redirect to={{ pathname: "/login", state: {from: props.location}
                                }}/>)
                            )
                      }
                      </Suspense>
                    </Page>
                )}>
                </Route>
              })
            }
            <Route component={NotFound}/>
          </Switch>
        </Router>
    );
  }
}
export default App;
```

- 关于BrowserRouter Switch Route 等可直接查看[官方文档](https://react-router.docschina.org/)
- 该教程用到了Suspense, lazy来做页面的懒加载，这是react 的新特性， 所以不需要再引入外部的插件来做懒加载
- 在遍历路由表的情况下， 会先将layout 组件 `Page` 放在最外层， 也就是只要不是404页面， layout布局都会渲染，然后再判断 `auth` ，这个字段是来判断当匹配到这个路由的时候你是否需要做拦截，然后再判断是否有token
- token的保存存储以及获取则是另外的解决方案