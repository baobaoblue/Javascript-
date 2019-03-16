### javascript原型规则

- 所有的引用类型（数组、对象、函数），都具有对象特性，即 可自由扩展属性（null 除外）

```
var obj = {}; obj.a = 100;
var arr = []; arr.a = 100;
function fn(){} fn.a = 100
```

- 所有的引用类型（数组、对象、函数），都有一个__proto__属性（这里暂时称之为 隐式类型 ），属性值是一个普通对象

```
console.log(obj.__proto__);
console.log(arr.__proto__);
console.log(fn.__proto__);
```

- 所有函数都有一个prototype属性（这里暂时称之为 显式类型），属性值也是一个普通对象

```
console.log(fn.prototype)
```

- 所有的引用类型数组、对象、函数），__proto__属性值只想它的构造函数的prototype属性值

```
console.log(obj.__proto__ === Object.prototype)   //true
console.log(arr.__proto__ === Array.prototype)   //true
```

- 当试图得到一个对象的某个属性时，如果这个对象本身没有这个属性，那么会去它的__proto__（即 它的构造函数的prototype）中寻找

```
function Foo(name){
    this.name = name
}
Foo.prototype.alertName = function(){
    alert(this.name)
}
var f = new Foo("zhangsan");
f.printName = function(){
    console.log(this.name);
}
f.printName();
f.alertName();
f.toString(); // 要去f.__proto__.__proto__中查找toString
