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



```js
/*
    * 总结：call apply 使用区别：传递参数不一样，apply是用数组传参，
    *  对比 bind， call和apply都是自动触发函数，
    *  bind: 返回的是一个新函数，不会主动的触发，需要被调用一次，传参的形式和call一样，直接在后面拼接
    * */
var _obj = {name: "wxm", age: 19};

    function fn1() {
        // 使用bind后该函数内部的this绑定了 _obj 对象
        console.log("fn1内部的this值：")
        console.log(this);
        console.log(this.name + "------" + this.age)
    };

    var test = {
        addrs: "china",
        fn1,
        funInner: function (addrs) {
            console.log("test.funInner内部的this值：")
            console.log(this);
            console.log("test对象内部的接收参数：" + addrs);
        }
    }

    // bind函数是绑定this 它会创建一个新函数，它不会立刻执行，需要调用，
    // fn1.bind(_obj)();
    // test.fn1.bind(_obj)();
    // 在使用需要传递参数的方法时可以在bind 内传递参数：列如："nanchang" 传递给 addrs；
    test.funInner.bind(_obj, "nanchang")();


    // test.funInner();

    function fn2() {
        console.log("fn2内部的this值：")
        console.log(this);
        console.log(this.x)
    };

    var _obj2 = {
        x: "xxx"
    };

    var test2 = {
        addrs2: "china",
        fn2,
        funInner2: function (addrs2) {
            console.log("test.funInner2内部的this值：")
            console.log(this);
            console.log("test对象内部的接收参数：" + addrs2);
        }
    }
    /*
    * call apply 都是函数的方法，在函数上使用
    * call apply 都会立即执行
    * 当需要传递参数是 call可以传递任意的，apply 后面是使用数组的形式传递参数
    * */
    // fn2.call(_obj2);
    // test2.funInner2.call(_obj2, "nihao");
    
    test2.funInner2.apply(_obj2, ["nihao"]);
```

