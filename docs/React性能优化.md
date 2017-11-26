
# React 性能优化


## 性能检测

安装 react 性能检测工具 `npm i react-addons-perf --save`，然后在`./app/index.jsx`中

```js
// 性能测试
import Perf from 'react-addons-perf'
if (__DEV__) {
    window.Perf = Perf
}
```

运行程序。在操作之前先运行`Perf.start()`开始检测，然后进行若干操作，运行`Perf.stop`停止检测，然后再运行`Perf.printWasted()`即可打印出浪费性能的组件列表。在项目开发过程中，要经常使用检测工具来看看性能是否正常。

如果性能的影响不是很大，例如每次操作多浪费几毫秒、十几毫秒，没必要深究，但是如果浪费过多影响了用户体验，就必须去搞定它。





## PureRenderMixin 优化

React 最基本的优化方式是使用[PureRenderMixin](http://reactjs.cn/react/docs/pure-render-mixin.html)，安装工具 `npm i react-addons-pure-render-mixin --save`，然后在组件中引用并使用

```jsx
import React from 'react'
import PureRenderMixin from 'react-addons-pure-render-mixin'

class List extends React.Component {
    constructor(props, context) {
        super(props, context);
        this.shouldComponentUpdate = PureRenderMixin.shouldComponentUpdate.bind(this);
    }
    //...省略其他内容...
}
```

React 有一个生命周期 hook 叫做`shouldComponentUpdate`，组件每次更新之前，都要过一遍这个函数，如果这个函数返回`true`则更新，如果返回`false`则不更新。而默认情况下，这个函数会一直返回`true`，就是说，如果有一些无效的改动触发了这个函数，也会导致无效的更新(组件中的`props`和`state`一旦变化会导致组件重新更新并渲染，但是如果`props`和`state`没有变化也莫名其妙的触发更新了)

这里使用`this.shouldComponentUpdate = PureRenderMixin.shouldComponentUpdate.bind(this);`的意思是重写组件的`shouldComponentUpdate`函数，在每次更新之前判断`props`和`state`，如果有变化则返回`true`，无变化则返回`false`。

因此，在每个 React 组件中都尽量使用`PureRenderMixin`



