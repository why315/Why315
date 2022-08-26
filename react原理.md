vitrulDom 虚拟Dom

react  虚拟Dom 进行算法匹配，将更改后的节点更新到真实Dom上

vitrulDom 转换成真实的Dom

第一步需要渲染render函数,render函数需要使用diff算法

```javascript
import diff from './diff'
export default function render (vitrulDom,contain,oldDom) {
// vitrulDom 虚拟dom 数据 contain 挂载的数据节点 oldDom 原来的节点
diff(vitrulDom,contain, oldDom)    
}
```

第二部 diff算法，判断是否存在原来的节点

```javascript
import mountElement from './mountElement'
export default function diff (vitrulDom,contain, oldDom) {
//调用算法判断当前是否存原来就有的节点
if(!oldDom) {
    mountElement(vitrulDom,contain)
}   
}
```

第三步 mountElement 判断 oldDom 是否存在，mountIsElement,进行渲染

```javascript
export default function mountElement (vitrulDom,contain) {
//渲染元素节点
    mountIsElement(vitrulDom ,contain)            
}
```

第四步  mountIsElement  判断是元素，可以进行虚拟Dom转换成真实Dom ,进行页面挂载

```javascript
import createElement from './createElement'
export default function mountIsElement(vitrulDom,contain) {
  const newsElement = createElement(vitrulDom)
  contain.appendChild(newsElement )
}
```

```javascript
export default function createElement (vitrulDom) {
    let newElement = null
    if(vitrulDom.type === "text) {
    newElement = document.createTextNode(vitrulDom.props.textContent)
    }else {
    newElement = document.createElement(vitrulDom.type)
    }
    vitrulDom.props.children.forEach(child =>{
    mountElement(child,newElement )
   })
    return  newElement 
}
```

第五步 为元素添加属性   

```javascript
export default function mountIsElement(vitrulDom,contain) {
    let newElement = null
    if(vitrulDom.type === "text) {
    newElement = document.createTextNode(vitrulDom.props.textContent)
    }else {
    newElement = document.createElement(vitrulDom.type)
    createNodeAttribute(newElement,contain)
    }
    vitrulDom.props.children.forEach(child =>{
    mountElement(child,newElement )
   })
  contain.appendChild(newElement)
}
```

```javascript
// vitrulDom 虚拟Dom contain 元素节点
export default function createNodeAttribute (vitrulDom,contain) {
//获取dom  props 数据，判断数据得
const newProps = vitrulDom.props
//item是获取到元素的属性
Object.keys(newProps).forEach(item =>{
    const newKey = newProps[item]
//判断属性是否是事件
    if(item.slice(0,2) === "on") {
        const newEvent = item.toLowerCase.slice(2)
        contain.addEventListener(newEvent,newKey)
    }else if(item === "value" || item === "checked"){
        newProps[item] = newKey
    }else if (item!== ""children) {
        if(item === "className) {
            contain.setAttribute("class",newKey )
        } else  {
            contain.setAttribute(item,newKey)
        }
     }
  })
}
```

第六步  渲染组件

```javascript
//判断是否是组件。组件type类型是函数
export default function isFunction(vitrulDom) {
    return vitrulDom && typeof vitrulDom.type === "function"
}
```

```javascript
export default function mountElement (vitrulDom,contain) {
//判断是否是组件
//渲染元素节点
if(isFunction(vitrulDom)){
//渲染组件
  mountComponent(vitrulDom,contain)  
 }else {
//渲染元素
  mountIsElement(vitrulDom ,contain)  
 }        
}
```

```javascript
//判断是函数组件还是类组件
export default function isFunctionComponent(vitrulDom){
const type = vitrulDom.type
  return  type&&isFunction(vitrulDom)&&
          !(type.prototype&&type.prototype.render)
}
```

```javascript
export default function mountComponent (vitrulDom,contain) {
if(isFunctionComponent(vitrulDom)){
    //渲染函数组件   
   mountFunctionComponent(vitrulDom,contain)
 }else {
    //渲染类组件
    mountClassComponent(vitrulDom,contain)
 }
}
```

```javascript
//渲染函数组件,传递props内容
import createElement form './createElement'
export default function mountFunctionComponent(vitrulDom,contain){
    //渲染函数组件得函数体内容，return返回得结构
    const element =  vitrulDom.type(vitrulDom.props)
    const newElement  = createElement(element)
    contain.appliendChild(newElement)
}
```

```javascript
//渲染类组件,获取class类，调用render 方法,获取结构数据
import createElement form './createElement'
export default function mountClassComponent(vitrulDom,contain){
    const newComponent = new vitrulDom.type()
    const news =newComponent.render()
    const newElement = createElement(news )
    contain.applendChild(newElement)    
}
```

```javascript
// 导出 react Component 类,传递 props参数
export default class Component{
    construal(props) {
    this.props = props
    }    
}
```

 
