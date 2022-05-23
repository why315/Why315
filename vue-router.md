# vue-router

routes 是路由规则的匹配,根据path去加载component，

```js
{
path:'/',
name:'index',
component:import('./index.vue')
}
```

实现原理：

实现一个class类

```js
export default class router {}
```

constructor 构造函数，需要接收options 对象，options对象为传递进来的数据

```js
constructor(options){
    this.options = options
    this.routerMap = {}
    this.data = vue.observe
}
```





这个类中有一个静态install的方法去判断当前的是否安装过router，并且将router挂载在实例上

具体实现方法：要设置一个属性去判断router是否已经安装了，如果已经安装了，就不再去重复安装，如果没有安装，就安装并挂载在vue实例上,声名一个全局变量去挂载vue实例

```js
let _vue = null
export default class router {
    static install(vue){
        if(router.install.installed){
            return 
        }
        router.install.installed = true
        _vue = vue
    }
}
```

