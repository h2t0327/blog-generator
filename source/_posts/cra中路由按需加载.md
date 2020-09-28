---
title: create-react-app 路由按需加载
date: 2019-04-15 23:00:00
categories:
  - 'react'
  - 'CRA'
tags:
  - 'react'
  - 'CRA'
copyright: true
---

# create-react-app 路由按需加载
由`create-react-app`创建的react应用是将webpack的配置项隐藏的，可以让开发者在不需要做任何配置的情况下开发react，但有时候开发者也会需要有些特殊的需求
1. `npm run eject`将webpack抛出再自己添加配置以解决需求
2. 通过`react-app-rewired`以及`customize-cra`来解决特殊需求
3. 正常的antd 按需加载 以及`less` `sass` `alias`等配置在网上都有大佬写出教程。  
4. 作为一个react 小白， 我就是很作。  
我就是想在不抛出webpack配置的情况下来做到路由组件的按需加载，经过在网络的漫长搜索， 发现都是通过抛出webpack 的方式来做按需加载。

通过一番努力， 发现抛出方式都是在`.babelrc`的`plugins`上添加一个`syntax-dynamic-import`插件。 于是借此解决了在不抛出配置的情况下按需加载问题。解决如下：
```react
const {override, addBabelPlugins, useBabelRc} = require('customize-cra');

module.exports = override(
    addBabelPlugins(
        ["syntax-dynamic-import",{"legacy": true}],
    ),useBabelRc());
```

在组件中
```react
import Loadable from 'react-loadable';

const MyLoadingComponent = ({isLoading, error}) => {
  // Handle the loading state
  if (isLoading) {
    return <div>没有</div>;
  }
  // Handle the error state
  else if (error) {
    return <div>Sorry, there was a problem loading the page.</div>;
  }
  else {
    return null;
  }
};

const LoadableComponent = Loadable({
                  loader: () => import('/pages/index'),
                  loading: MyLoadingComponent
                });
```

至此按需加载算是完成了

- 后来发现react更新后添加了两个新特性`Suspense, lazy`可以直接通过引入这两个特性做到按需加载， 根本不需要上面那么麻烦的配置


```react
import React, {Component, Suspense, lazy} from 'react';
const DynamicComponent = lazy (() => import('/pages/index'));
 <Suspense fallback={<div>loading...</div>}>
 	<DynamicComponent />
 </Suspense>
```