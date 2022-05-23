# vue3

#### compontionApi

###### (1)ref

使用：

```ts

/*
ref 包裹的值会转化成Proxy对象（响应式）
*/
//简单数据类型
const num = ref(1)
//复杂数据类型
const Array = ref({
    a:1,
    b:2,
})
//ref 对象取值
console.log(num.value)
console.log(Array.a.value)
```

(2)reactive

使用：

```ts
/*
reactive包裹的值也是响应式proxy 对象,并且是深拷贝的数据
*/
const number = reactive({
    a:'12121',
    b:{
        c:'121212'
    }
    
})
/*
reactive 更适合包裹复杂数据类型
reactive 取值
*/
console.log(number.values) //proxy{a:'12121'....}
console.log(number.b.values)
```

(3) setup

```js
/**
setup 函数 可以定义数据，方法，并且包含beforeCreated、created生命周期,在页面上使用的数据函数通过renturn 返回出去
**/
setup(){
    //定义数据
    const num = ref(0)
    //定义方法
    const getDate = (index:number) => {
        console.log(idnex)
    }
    return {
        num,
        getDate
    }
}
```

```ts
/*
setup函数可以接收两个参数，props，context（上下文）,props不需要再通过ref或者是reactive包装一次
*/
export default defineComponent({
    props：{
    data:{
    type:string,
    default:''
    }
  },
    setup(props,context){
    const data = props.data
    //const data = ref(props.data)
    return {
        data
    }
  }
})
```

```ts
/**
setup函数接收context参数，context可以解构出emit，slots，attrs, emit触发函数，向上传递参数与方法
*/
export default defineComponent({
  emits:['change']
    setup(context){
    const changeDate = () => {
        //data 是change方法携带的参数数据
        context.emit('change',data)
    }
       return {
           changeDate
       }
   } 
})
//emit使用需要载页面上明确有props属性，否则会报错,并且需要在函数中定义emits，将触发的函数写入其中
```

```ts
/*
生命周期函数需要onxxxx，这种方式在setup中使用，并且在 
import {onMounted, defineComponent, onUpdate} from 'vue'引入
**/
export default defineComponent({
    setup(){
        const op = () => {
            console.log('op')
        }
        onMounted(() =>{
            op()
        })
        onUpdate(() => {
            op()
        })
        return {
            op
        }
    }
})
```



```ts
/*
setup函数中的provide与inject使用。祖孙组件传值
**/
//父组件 
import {provide} from 'vue'
export default defineComponent({
    setup(){
        const listDate = reactive({
            detail:[],
            total:90
        })
        provide('listDate',listDate)
        return {
            listDate
        }
    }
})
//孙组件 inject接收传递的数据名称与provide中的名称对应
import {inject} from 'vue'
export default defineComponent({
    setup(){
    	const data = inject('listdata')
        return {
            data
        }
    }
})
```

```js
/*
setup函数中获取到当前的实例对象方法getCurrentInstance（）
**/
import {getCurrentInstance} from 'vue'
export default defineComponent({
    setup() {
        const obj = getCurrentInstance()
        console.log(obj)
     return {
    
     }
    }
})
```

```js
/**
setup函数中使用toRefs,可以将reactive或者是ref包裹的对象，解构，在页面中直接使用
*/
<template>
 <div>
    //在页面中直接使用Array中的数据
   {{a}}
 </div>
</template>
import {toRefs} from 'vue'
export default defineComponent({
    setup() {
        const Array = reactive({
            a:'1',
            b:'3'
        })
     return {
    	...toRefs(Array)
      }
    }
})

```

```js
//全局属性（方法）挂载 方法 globalProperties属性
app.config.globalProperties.$http = () => void
```

```js
/**
setup函数中使用watch，观察数据变化,watch 只有在数据变化的时候才会监听数据
***/
import {watch ，defineComponent} from 'vue'
export default defineComponent({
    setup() {
        const wacher = ref(1)
        //watch监听数据（'监听的数据'，calback（））ref数据可以直接写变量名称
        //reactive 数据需要返回函数 （（）=> '监听数据', callback()）
        //需要深拷贝数据的时候，添加数据{deep：true}
        watch( watcher,(newValue,oldValue)=>{
            console.log(newValue,oldValue)
        })
     return {
    	wacher
      }
    }
})
```

```js
//teleport标签 to表示要挂载的地址可以使用ID或者是类名或者是属性名称
<teleport to="#id">
 <div></div>    
</teleport>
```

```js
//watchEffect 函数 会立即执行一此，并且在监听的数据发生变化时，再次执行
import {watchEffect ，defineComponent} from 'vue'
export default defineComponent({
    setup() {
	const watcher = ref(0)
    watchEffect(()=>{
        console.log(watcher.value)
    })
     return {
    	wacher
      }
    }
})
```



