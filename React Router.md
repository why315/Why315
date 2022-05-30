# React Router

一、使用的路由模式

游览器路由，hash 路由，history 路由，内存路由，静态路由

```javascript
import { BrowserRouter } from "react-router-dom";
import { HashRouter } from "react-router-dom";
import { unstable_HistoryRouter as HistoryRouter } 
from "react-router-dom";
import { MemoryRouter} from "react-router-dom";
import { StaticRouter } from "react-router-dom/server";
```

尝试用的路由主要是hashRouter与historyRouter，BrowserRouter!

二、路由的组件

路由组件有<mark> Link</mark>，<mark>NavLink</mark>,  <mark>Navigate</mark>,  <mark>Outlet</mark>,  <mark>Route</mark>,   <mark>Routes</mark>

<mark>Link </mark>  路由跳转，to属性可以跳转到指定的路由路径

```javascript
import {Link} from  'react-router-dom'
const app = ()=>{
    return (
    <>
        <Link  to ="/login"/>
    </>
)
}
```

<mark>NavLink</mark>



<mark>Navigate</mark>   配合useNavigate () 获取到路径跳转的navigate ，进行路径跳转 

```javascript
import { useNavigate } from "react-router-dom";
const App = ()=>{
const naviaget = useNavigate()    
return (
    <>
        <button  onClick = {()=>{
          navigate('/login')
       }/>
    </>
  )
}
```

<mark>Outlet</mark>  路由占位符 ,路由匹配时，进行占位的，可以匹配到路由上的地址去进行渲染，类似于 vue的router-view

```javascript
import {Outlet} from  'react-router-dom'
const App = ()=>{
    return (
    <div>
         <button>按钮</button> 
            <Outlet/>  
    </div>
)
}
```

<mark>Route</mark> 路由需要和<mark>Routes</mark> 配合使用 path是路由跳转的路径，element 是路由匹配加载的模块名称

```javascript
import {Route,Routes} from 'react-router-dom'
import Login from './Login'
const App = () = > {
    return (
    <>
    <Routes >
        <Route path="/login"  element = <Login />
    </Routes>
    </>
)
}
```

react-router Hooks

```js
import {useRoutes} from 'react-router-dom'
import Login from './login'
import App from './App'

const router = useRoutes([
    {
    path:'/login',
    element:<Login/>
    },
    {
        path:'/add/:id',
        //动态路由传递参数
        element:<App/>
    }
])
```

一、 useParams()获取动态传递的参数

```javascript
import {useParams} from  'react-router-dom'
const App = ()=>{
const params = useParams()    
return(
    <>
    {
    params.id
    }
    </>
)
}
```


