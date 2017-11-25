
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

