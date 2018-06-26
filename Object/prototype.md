### __proto__

`o1`和`o2`效果是一样的
```javascript
let o1={ __proto__: {x:1,y:2} }

let o2=Object.create( {x:1,y:2} )
```

如果当前对象没有该属性, 则从继承对象中找该属性
```javascript
let o1={ __proto__: {x:1,y:2} }

o1.x      // 1 并非返回undefined, 因为语言特性, 从继承关系获取x
o1.x=11   // 设置了o1.x  并非是o1.__proto__.x
o1.x      // 11
o1.__proto__.x                // 1
Object.getPrototypeOf(o1).x   // 1
```

寻找属性, 直到继承链不再存在
```javascript
let o={ __proto__: { __proto__:{x:1}, y:2} }

console.log(o.x)		// 1  继承对象的继承对象中找到了x
```

函数是可以被new出实例的<br>

```javascript
function O() {}

O.prototype.x=1

let o=new O

console.log(o)					  // O {}
console.log(o.x)				  // 1
console.log(o.__proto__)	// {x:1,y:2}
```
