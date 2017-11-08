# React + React-router + Redux 的前端代码框架


**`./app/actions`**

Redux 中使用的 actions

**`./app/components`**

组件（木偶组件）目录。一个组件一般用一个文件夹表示，里面一般有`index.jsx`、`style.less`、`img/`目录

**`./app/constants`**

Redux 的 actions 和 reducers 都会用到的常量，统一放在这里，

**`./app/containers`**

页面（智能组件）目录。注意，一个页面一般用一个文件夹表示，里面有`index.jsx`，如果页面复杂，可能需要`subpage/`目录来拆分页面。

**`./app/reducers`**

Redux 用到的 reducers

**`./app/router`**

React-router 配置文件

## `./app/static`

系统全局使用的静态资源

## `./app/store`

Redux 创建 store

## `./app/util`

系统工具函数，处理时间格式，处理字符串格式等

