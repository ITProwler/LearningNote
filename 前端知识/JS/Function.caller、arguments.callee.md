- ### Function.caller

	指向调用当前函数的函数，如果是在全局范围内被调用的话，caller的值为null（但使用node执行js文件时，发现输出结果并不是null，在浏览器中是null）

```javascript
function outer() {
    inner();
}
function inner() {
    if(inner.caller==null) { //值为null，在全局作用域下调用
        console.log("我是在全局环境下调用的");
    } else {
        console.log(inner.caller+"调用了我");
    }    
}
inner();
outer();
```

- ### arguments.callee

	指向拥有该arguments的函数对象，但是在严格模式下使用arguments.callee会报错。

	在函数名发生变动时，使用arguments.callee可以减少修改代码的地方，降低出错率。

```javascript
function outer() {
    inner();
}
function inner() { //只需改这个函数名，而不需要改内部代码
    if(arguments.callee.caller==null) {
        console.log("我是在全局环境下调用的");
    } else {
        console.log(arguments.callee.caller+"调用了我");
    }    
}
inner();
outer();
```

- ### arguments.caller（已废弃）
