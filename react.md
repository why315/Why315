# react

## 

一、react是如何决定更新的以及如何保证状态更新的

react决定更新是去判断内存是否一致，不是根据内容是否一致去判断，当存储在浏览器中的内存发生变化时，react才会去更新ui以及内容，

```javascript
const obj = {name:'90',age:'889'}
const obj2 = obj
obj===obj2 
// true 这里两个数据的内容是一致的，指针指向的内存地址也是一致的，
//属于浅拷贝，所以完全相等
const obj3 = Object.assgin({},obj)
obj === obj3 
// false obj3是由 obj 与空对象 组合在一起的，属于一个新的内存当中的内容，
//虽然obj与obj3内容完全一致，但是指针指向的不是一个内存地址
```

```javascript
import './App.css';
import { Component } from 'react';

class App extends Component {
  constructor() {
    super()
    this.state = {
      name: 'wangh',
      age: '90'
    }
  }
  render() {
    return (
      <div>
        {this.state.name}
        <button onClick={() => {
          this.setState({
            name:'why'
          })
          console.log(this.state)
        }}>changeName</button>
      </div>
    )
  }
}
```

输入的内容为 {name: 'wangh', age: '90'}

这里是因为this.setState并不是同步更新，是异步更新，没有办法保证log的时候，内容一定会拿到更更新后的值，如果想拿到更新后的值，建议使用函数与回调函数

在this.setState中有两个函数，第一个函数设置需要更改的值，第二个函数，可以拿到更改后的值，并且对更改的值做一些数据处理。

```javascript
return(
    <div>
        {this.state.name}
        <button onClick={() => {
          this.setState(() => {
            return { name: 'why' }
          }, () => {
            console.log(this.state)
          })
        }}>changeName</button>
      </div>
)
```

二、react 是如何决定渲染顺序的

类组件当中，react 会首先去渲染 constructor 构造函数，然后去render dom节点，在渲染dom节点的时候，去渲染recat的挂载生命周期中执行的函数，如果在生命周期函数中有setState函数设置，会重新去渲染 render 函数，更新dom节点

三、react 组件之间的传值

第一种：使用发布订阅者模式，Provider 组件内的所有组件都可以接收到  父组件传递的参数

```javascript
import React from 'react'
import Content from './content'
export const Provide = React.createContext('light)
const App = ()=>{
const values = {
    name:'wwww',
    age:"90"
}
    return 
    <>
        <Provide.Provider value = {values}>
            <Content />
        </Provide.Provider>
    </>
}
export default  App 
```

使用 useContext 接收订阅者发布的消息，useContext (发布者)

```javascript
import React from 'react'
import {Provide}  from './App'
const Content = ()=>{
const {name, age} = React.useConetxt(Provide)
    return 
    <>
        {name}---{age}
    </>
}
```

使用 Consumer 接收发布者发布的消息

```javascript
import React from 'react'
import {Provide} from './App'
const Content = ()=>{
    return (
    <>
    <Provide.Consumer>
    {
    ({name,age})=>{
        return (
            <>{name} ==== {age}</>
            )
        }
    }
    <Provide.Consumer/>
    </>
)
}
```

第二种：使用props 方式传递值,父组件上传递属性，组件使用Props 接收传递过去的属性，也可以在子组件中直接解构props

```javascript
import React from 'react'
import Content from './Content'
const App = ()=>{
const values = {
    name:'www',
    age:'90'
}
    return(
    <>
      <Content value = {values}/>
    </>
) 
}
export default App
```

```javascript
import React from 'react'

const Content = (props || {name, age})=>{
  const {name,age} = props
// 在组件上直接解构，租价内部可以不使用解构方法
    return (
    <>
      {name}=={age}  
    </>
    )
}
export default Content
```

四、react hooks 使用

一、useCallback （）对函数进行保存，只有依赖项发生变化的时候才会触发函数

```javascript
const hand = useCallback(()=>{},[]) // 数组为依赖项
```

二、useMemo() 对函数进行缓存 ，只有依赖项发生变化的时候才会触发函数，用于函数内部的计算属性缓存

```javascript
const arr= UseMemo(()=>{},[])  //数组为依赖项
```

useCallback() 与useMemo () 当中的依赖项都不会传入到内部，都只是作为更新的条件！

三、useRef（） 用于生成ref 属性，通过  .current  获取当前ref实例

```javascript
const actionRef = useRef()
```
