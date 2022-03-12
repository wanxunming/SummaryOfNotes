### this指向问题

**this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，实际上this的最终指向的是那个调用它的对象**

<img src="JS常见问题.assets/image-20220308214928539.png" alt="image-20220308214928539" style="zoom:50%;" />

### 作用域



### 闭包

**闭包可以解决函数外部无法访问函数内部变量的问题**

**通过闭包我们可以让函数中的变量持久保持，和JS回收机制有关联**

定义一个函数，外部每次调用该函数都是创建一个新的函数，和上一个函数的调用没有任何关联

```js
function fn(){
   var num = 5;
   num+=1;
   alert(num);
 }　　
fn(); //6
fn(); //6
```

使用闭包：我们首页定义了一个fn函数，里面有个num默认为0，接着返回了一个匿名函数（也就是没有名字的函数）。我们在外部用f接收这个返回的函数。这个匿名函数干的事情就是把num加1，还有我们用来调试的alert。

```js
function fn(){
  var num = 0;
　return function(){
　　num+=1;
    alert(num);　　　
  };　　
 }
 var f = fn();
 f(); //1
 f(); //2
```

这里之所以执行完这个函数num没有被销毁是因为那个匿名函数的问题，因为这个匿名函数用到了这个num，所以没有被销毁，一直保持在内存中，因此我们f()时num可以一直加。



### JS原型对象的理解

#### 有关原型对象的三个重要属性：

protopyte（显式原型）：专属于函数（除箭头函数）的一个属性，原型对象，用来给将来new出来的实例作为父级使用

__ proto __ （隐式原型）:用于指向构造当前实例的构造函数中的prototype，隐式的自调用，可以通过它获取到prototype中的属性和方法

constructor（protopyte专属）：标识当前protopyte所对应的构造函数。

使用构造函数和原型时：将属性写在构造函数中，将方法写在原型中并且在原型中使用constructor来指向前面的构造函数。

```js
// 构造函数
function Fn(name,age){
  // 属性
  this.name = name;
  this.age = age;
}
// 原型对象 内部是key-value形式
Fn.prototype = {
  //反过来引用自身构造函数
  constructor : Fn,
  // 方法
  FnName:function(){
    console.log("@@name="+this.name);
  },
  FnAge:function(){
    console.log("@@age="+this.age);
  }
}
var fnObject = new Fn("wxm",24);
console.log(fnObject.name);	//wxm
console.log(fnObject.age);	//24
fnObject.FnName(fnObject);	//@@name=wxm
fnObject.FnAge(fnObject);		//@@age=24
```

总结上面的例子：每个对象函数有名为protopyte属性，用于引用原型对象，此原型对象上又有constructor属性反过来引用函数本身，这是一种循环引用。

```js
Fn.prototype.constructor === Fn //true
fnObject.__proto__.constructor === Fn //true
```



#### 函数的原型对象：

