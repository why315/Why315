# vue2

### 1、组件之间得通信：

```js
(1)props
props:['value']
props:{
        type:Array,
        default:[]
}
(2) $emit\$on
(3)vuex
(4)project\inject 依赖注入
(5)bus 中间件
```

### 2、event 事件

```js
标签绑定事件是Dom原生事件
组件绑定事件是自定义事件需要使用.native自定义事件绑定为Dom原生事件
```

### 3、sync修饰符

```js
同步父子组件得数据 :money.sync = 'money'
```

### 4、$attrs与$listener

```js
//$attrs 可以获取到组件上得传递得数据
// 父组件
<todo title='我的组件'/>
//子组件
 this.$attrs 可以获取到父组件得title 属性,
 使用v-bind绑定$attrs
// $listener 可以获取父组件传递得函数
 <toso @click = handle/>
 handle(){
     console.log('0000')
 }
//子组件
this.$listener 获取click函数
使用 v-on 绑定函数 $listener
```

5、vue-router

```js
vue-router 使用hash 和history 模式原理：
hash 使用锚点链接，配合window.onhashChnage 
history 是使用
history.pushState() ie10以上版本支持
history.replaceState()
```

5.1 hash与history 模式存在得问题

history 模式需要服务器配合进行设置解决 刷新页面丢失问题

history 在node中需要设置中间件

```js
app.use(history())
```

history 在 nginx 中需要在location 中进行设置

```js
try_files: $url $url/ /index.html
进行文件访问地址映射设置
```

6、vue-router 传参

params 与 query  
name与params搭配使用
path与query 搭配使用
动态传递参数时候参数可传可不传,在动态参数得后面添加？

```js

{
    path：'/login/:id?',
    name:'login',
    component:() => import( '../login')
}

```

如果参数为空得话：需要在传递参数时设置undefined

```js
this.$router.push({
    name:'login',
    params:{
        keyword:this.keyword || undefined
    }
})
```

使用props传递参数：
(1)

```js
{
    path：'/login/:id',
    name:'login',
    component:() => import( '../login'),
    props:true
}
```

组件内部使用得时候：
props：['id']
页面上直接使用：
{{id}}
(2)

```js
 {
    path：'/login/:id',
    name:'login',
    component:() => import( '../login'),
    props:{a:1,b:2}
 }
```

组件内部接收
props：['a','b']
页面上使用：
{{a}}{{b}}
(3) 使用函数得时候只能接收params 参数

```js
{
    path：'/login/:id',
    name:'login',
    component:() => import( '../login'),
    props:($route) => {
        return {
            id:$route.params.id
        }
    }
}
```

组件内部使用得时候：
props：['id']
页面上直接使用：
{{id}}

