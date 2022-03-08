#### bind ( ) 方法

​	主要就是将函数绑定到某个对象，bind ( ) 会创建一个函数，函数体内的this对象的值会被绑定到传入bind ( ) 第一个参数的值，例如，f.bind(obj)，实际上可以理解为obj.f()，这时，f函数体内的this自然指向的是obj



#### call() 和 apply() 方法

当使用 person2 作为参数调用 person1.fullName 时，this 将引用 person2，即使它是 person1 的方法

```js
var person1 = {
  fullName: function() {
    return this.firstName + " " + this.lastName;
  }
}
var person2 = {
  firstName:"Bill",
  lastName: "Gates",
}
person1.fullName.call(person2);  // 会返回 "Bill Gates"
```

