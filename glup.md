# gulp使用配置

1、创建文件，yarn init--yes，初始化packjson 文件

2、yarn add gulp --dev  安娤gulp文件

3、使用gulp

```js
exports.foo = () => {
    console.log('foo')
}
命令行：yarn gulp foo
报错：
 The following tasks did not complete: foo
Did you forget to signal async completion?
 需要在函数中接收一个参数done
expors.foo= (done) => {
    conosle.log('foo')
    done()
}
```

 

4、组合使用gulp

```js
const { series, parallel } = require('gulp')
const foo = (done) => {
  console.log('startFoo')
  done()
}
const op = (done) => {
console.log(op)
done()
}
//串行任务
exports.bar = series(foo,  op)
// 并行任务
exports.fos = parallel(foo, op)
```

5、gulp异步的三种方式

```js
exports.callback = (done) => {
  console.log("callback");
  done();
};
exports.callback_error = (done) => {
  console.log(callback_error);
  done();
};
//promise 模式
exports.promises = () => {
  console.log("promise");
  return Promise.resolve();
};
exports.promise_error = () => {
  console.log("promsie_error");
  return Promise.reject(new Error("promsie_error"));
};
//async await 模式
const timeOut = (time) => {
 return  new Promise(resolve => {
    setTimeout(resolve, time);
  });
};

exports.bar = async() => {
  await timeOut(100)
  console.log('async')
}
```

6、读写文件

```js
//读写文件，将package.json文件内容写到tem.txt文件中
exports.writeFile = () => {
  const readFile = fs.createReadStream('package.json')
  const writeFile = fs.createWriteStream('tem.txt')
  readFile.pipe(writeFile)
  return readFile
}
```

7、gulp核心工作原理就是读取文件，经过转换，写入到新的文件中

```js
const fs = require("fs");
const { Transform } = require("stream");
exports.default = () => {
  const read = fs.createReadStream("min.css");
  const write = fs.createWriteStream("mins.css");
  const transFrom = new Transform({
    transform: (chunk, encoding, callback) => {
      const input = chunk.toString();
      const output = input.replace(/\s+/g, "").replace(/\/\*.+?\*\//g, "");
      callback(null, output)
    },
  });
  read
  .pipe(transFrom)
  .pipe(write)
  return read
};

```

8、gulp-imagemin报错

```js
gulp-imagemin 报错
require() of ES modules is not supported
const image = require('gulp-iamgemin')改成
const image = import ('gulp-imagemin')
或者降低版本打稳定版本
npm install gulp-imagemin@7.1.0 -D
```

