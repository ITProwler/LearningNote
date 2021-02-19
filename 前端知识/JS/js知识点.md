## 大文件分割

使用file.substr(start, end)会报错，但是使用file.slice(start, end)却不会

- ### substring(indexStart, [indexEnd])
  
  **返回一个索引和另一个索引之间的字符串，不改变原字符串**

1. `substring()`从提取的字符indexStart可达但不包括 indexEnd
2. 如果indexStart 等于indexEnd，`substring()`返回一个空字符串。
3. 如果indexEnd省略，`substring()`字符提取到字符串的末尾
4. 如果任一参数小于0或是NaN，它被视为为0
5. 如果任何一个参数都大于stringName.length，则被视为是stringName.length。
6. 如果indexStart大于indexEnd，那么效果substring()就好像这两个论点被交换了一样； 例如，`str.substring(1, 0) == str.substring(0, 1)`

- ### substr(start, [lenght])

**	返回从指定位置开始的字符串中指定字符数的字符，不改变原字符串**

1. `substr()`会从start获取长度为length字符（如果截取到字符串的末尾，则会停止截取）。
2. 如果start是正的并且大于或等于字符串的长度，则substr()返回一个空字符串。
3. 若start为负数,则将该值加上字符串长度后再进行计算（如果加上字符串的长度后还是负数，则从0开始截取）
4. 如果length为0或为负数，substr()返回一个空字符串。如果length省略，``substr()`字符提取到字符串的末尾

- ### slice(start, [end])

	**返回一个索引和另一个索引之间的字符串或数组，不改变原字符串或原数组**

1. 若start为负数,则将该值加上字符串长度后再进行计算（如果加上字符串的长度后还是负数，则从0开始截取）
2.  如果start大于或等于字符串的长度，`slice()`返回一个空字符串。
3. 如果end省略，则将slice()字符提取到字符串的末尾。如果为负，它被视为strLength + endIndex，其中strLength是字符串的长度

- ### splice(start, howmany[, item1, item2])

**	向/从数组中添加/删除项目，然后返回被删除的项目，返回结果是一个数组。会改变原数组**

```javascript
//插入数据
let a = ['1','2','3']
a.splice(1,0,'a')
console.log(a) //['1','a',2','3']
//删除数据
let b = ['1','2','3']
b.splice(1,1)
console.log(b) //['1','3']
//替换数据
let c = ['1','2','3']
c.splice(1,1,'a')
console.log(c) //['1','a','3']
```

<br/>

## 严格模式

	使用*“use strict";*或者*'use strict';*来为**脚本、函数、eval、内联事件处理属性、WindowTimers.setTimeout()**开启严格模式

#### 严格模式的变化

- 不再把未声明的变量默认为全局变量
- 严格模式会使引起静默失败的赋值操作抛出异常。如：***给NaN赋值、给不可写属性赋值、给只读属性赋值、给不可扩展对象的新属性赋值***
- 在严格模式下, 试图删除不可删除的属性时会抛出异常

- 严格模式要求一个对象内的所有属性名在对象内必须唯一。正常模式下重名属性是允许的，最后一个重名的属性决定其属性值
- 严格模式要求函数的参数名唯一，在正常模式下, 最后一个重名参数名会掩盖之前的重名参数. 之前的参数仍然可以通过 arguments[i] 来访问。
- 严格模式禁止八进制数字语法，支持为一个数字加"0o"的前缀来表示八进制数。
- 严格模式禁用 with
- 严格模式下的eval不在为上层范围引入新变量。
  ```javascript
  var x = 17;
  var evalX = eval("'use strict'; var x = 42; x");
  console.assert(x === 17);  //true
  console.assert(evalX === 42);  //true
  
  //-------------------------------------------
  function strict1(str) {
    "use strict";
    return eval(str); // str中的代码在严格模式下运行
  }
  function strict2(f, str) {
    "use strict";
    return f(str); // 没有直接调用eval(...): 当且仅当str中的代码开启了严格模式时
                   // 才会在严格模式下运行
  }
  function nonstrict(str) {
    return eval(str); // 当且仅当str中的代码开启了"use strict"，str中的代码才会在严格模式下运行
  }
  
  strict1("'Strict mode code!'");
  strict1("'use strict'; 'Strict mode code!'");
  strict2(eval, "'Non-strict code.'");
  strict2(eval, "'use strict'; 'Strict mode code!'");
  nonstrict("'Non-strict code.'");
  nonstrict("'use strict'; 'Strict mode code!'");
  ```
- 严格模式禁止删除声明变量。否则会提示语法错误。
- 严格模式下，禁止修改eval和arguments对象
- 严格模式下，参数的值不会随 arguments 对象的值的改变而变化。

```javascript
function f(a) {
  "use strict";
  a = 42;
  return [a, arguments[0]];
}
var pair = f(17);
console.log(pair[0] === 42); //true
console.log(pair[1] === 17); //true
```

- 严格模式下，通过this传递给一个函数的值不会被强制转换为一个对象。正常模式下，this总会是一个对象。
  ```javascript
  "use strict";
  function fun() { return this; }
  console.log(fun() === undefined); //true
  console.log(fun.call(2) === 2); //true
  console.log(fun.apply(null) === null); //true
  console.log(fun.call(undefined) === undefined); //true
  console.log(fun.bind(true)() === true); //true
  ```

- 严格模式下，使用func.caller和func.arguments会报错（func是一个Function）。

## with的使用

- with的使用

```javascript
var obj = {
	a: 1,
	b: 2,
	c: 3
};

// 重复写了3次的“obj”
obj.a = 2;
obj.b = 3;
obj.c = 4;

//使用with
with (obj) {
	a = 3;
	b = 4;
	c = 5;
}
```

- with的弊端
  
  导致数据泄露
  ```javascript
  function foo(obj) {
  	with (obj) {
  		a = 2;
  	}
  }
  
  var o1 = {
  	a: 3
  };
  
  var o2 = {
  	b: 3
  }
  
  foo(o1);
  console.log(o1.a);	//2
  
  foo(o2);
  console.log(o2.a);	//underfined，o2没有a属性，不会创建这个属性
  console.log(a);		//2，a被泄漏到全局作用域上，在非严格模式下，会自动在全局作用域创建一个全局变量，在严格模式下，会抛出ReferenceError 异常。
  ```
  
  性能下降
  
  严格模式下禁用with

## eval的使用

	eval() 函数可计算某个字符串，并执行其中的的 JavaScript 代码，并返回通过计算 string 得到的值。

```javascript
eval("2+3")	// 返回 5
eval("func()") //执行func方法
eval("var a=1") //声明一个变量a并赋值1
eval("{b:2}") //声明一个对象，
eval("({b:2})") //返回这个对象
```

**注：***Function创建出来的函数，并不会直接调用，只有当手动去调用创建出来的函数的时候才会执行，eval把字符串转化为代码后，直接就执行了。*