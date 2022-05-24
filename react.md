react 父子组件传递数据


react 父子组件传递数据
react 组件之间的传值有两种模式：
一、第一种使用props 
﻿
import Home from './Home'
﻿
const Index = ()=>{
﻿
  const data = {
﻿
    value:'90',
﻿
    name:'qqqq'
﻿
  }
﻿
  return (
﻿
    // 向子组件传递一个对象
﻿
    <Home value = {data}>
﻿
    //或者将传递的对象解构传递过去
﻿
    //<Home {...data}>
﻿
  )
﻿
}
﻿
export default Index
﻿
const Home = (props)=>{
﻿
//props 就是父组件传递过来的value的值
﻿
// 接收父组件传递过来的参数,并且解构
﻿
  const {value,name}= props
﻿
  return (
﻿
    <div>
﻿
      {value}=={name}
﻿
      // 90==qqqq
﻿
    </div>
﻿
  )
﻿
}
﻿
export default Home
﻿
//接收传递过来解构好的参数
﻿
const Home = ({value,name})=>{
﻿
return (
﻿
  <div>
﻿
    {value}==={name}
﻿
  </div>
﻿
)
﻿
}
﻿
​
二、使用React.createContext 与 useContext 发布订阅者模式
﻿
import Home from './Home
﻿
export const Tentext = React.createContext('obj') // 这里obj 属于默认值，在没有匹配到最近的provide的时候 默认的值会生效 
﻿
const Index = ()=>{
﻿
  const value = {
﻿
  obj:'90',
﻿
  name:'2233'
﻿
  }
﻿
  return (
﻿
  // provider 作为发布者，将value这个属性发布出去，所有在Tentext 组件内部的组件都会接收到
﻿
  // value这个属性
﻿
  <Tentext.Provider value = {value}>
﻿
  <Home />  
﻿
  </Tentext.Provider>
﻿
  )
﻿
  
﻿
}
﻿
export default Index      
﻿
      
﻿
      
﻿
      
﻿
import React form 'react'
﻿
import {Tentext} from './Index'
﻿
// 接收创建的上下文发布者
﻿
const Home = ()=>{
﻿
  // 将创建的上下文发布者，使用useContext 接收到传递的参数，也就是value的值，
﻿
  const params = React.useContext(Tentext)
﻿
  //解构接收到的 参数的值
﻿
  //const {obj,name} = React.useContext(Tentext)
﻿
  return (
﻿
     <div>
﻿
      {params.obj}==={params.name}
﻿
      //90==2233
﻿
    </div>
﻿
  )
﻿
}
﻿
export default Home
﻿
import {Tentext} from './Index'
﻿
const Home =()=>{
﻿
  return (
﻿
  //使用订阅者模式，去接受发布者发布的数据
﻿
  <Tentext.Consumer>
﻿
      {
﻿
        ({obj,name})=>{
﻿
          return (
﻿
            <div>
﻿
              {obj}=={name}
﻿
            //90==2233
﻿
            </div>
﻿
          )
﻿
         }
﻿
      }
﻿
      
﻿
  </Tentext.Consumer>
﻿
  )
﻿
}
﻿
export default Home

