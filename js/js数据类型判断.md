# js数据类型判断

1.对于基本类型以及函数：typeof
用法： typeof(val)

```js
var a = 'Nich'; //string
var b = true;  //boolean
var c = 12;  //number
var d;  //undefined
var e = null;  //object
var f = {};  //object
var g = function(){}  //function
```

2.对于引用类型：instanceof
用法：obj instanceof Type(eg: obj instanceof Array) 

```js
var person = {};
alert(person instance of Object);//true;
var color = []; //
alert(color instance of Array);//true;
var pattern = /\w/;
alert(pattern instance of RegExp);//true;
```

3.万能型(跨框架)：Object.prototype.toString.call()
用法：Object.prototype.toString.call(val)

```js
Object.prototype.toString.call('');//object String
Object.prototype.toString.call(123);//object Number
Object.prototype.toString.call(true);//object Boolean
Object.prototype.toString.call(a);//object Undefined
Object.prototype.toString.call(undefined);//object Undefined
Object.prototype.toString.call(null);//object Null
Object.prototype.toString.call([]);//object Array
//Array.isArray([])也可以跨框架
Object.prototype.toString.call({});//object Object
Object.prototype.toString.call(function(){});//object Function
Object.prototype.toString.call(/\d/);//object RegExp
```

补充：

* Array： ES6新增Array.isArray()方法。
