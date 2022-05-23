# plop 使用：

## plop 可以在需要重复得去写一些重复得文件或者内容重复得时候去使用：

## 1、安装 plop 到项目中

```js
 npm install plop -D
yarn add plop -D
```

## 2、创建plopfile.js

创建plopfile.js 文件 作为plop得入口文件

## 3、配置项

```js
module.exports = (plop) => {
    // setGenterator 第一项是 命令行 具体得命令
    plop.setGenerator('component', {
        description:'vue components', //描述信息
        prompts: [ //在命令行显示得信息，需要手动输入确定
            {
                type：'input', //以input方式输入得信息
                name:'name', 
                message:'please write components name', //需要确认得信息是什么，得到的就是输入得信息,
                default:'vue',//默认不输入得情况下的components 名字
            }
        ]，
        // 根据输入的信息去创建文件，data 是输入数据得对象集合
        actions：(data) => {
        const actions = [
            {
                type:'add', //新建文件
                path:`src/components/${data.name}/${data.name}.vue`, //写入到那个文件中去
                templateFile:'plop_template/components.hbs'//根据那个模板来写文件
            },
            //创建多个文件，就添加多个对象即可
            {
                type:'add', //新建文件
                path:`src/components/${data.name}/${data.name}.scss`, //写入到那个文件中去
                templateFile:'plop_template/style.hbs'//根据那个模板来写文件
            }
        ]
        return actions
    }
    })
}
```

## 4、模板文件（plop_template/components.hbs）

```js
<template>
  <div class="{{name}}">{{name}}</div>
</template>

<script>
export default {
  name: '{{name}}',
}
</script>

<style lang = 'scss' scoped>
  @import 'src/style/{{name}}/{{name}}.scss'
</style>

```

## 5、使用 创建好得命令

```js
yarn plop component
```

输入命令行提示得问题后，就会得到创建好得文件

