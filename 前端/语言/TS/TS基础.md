### TS基本类型：

布尔类型：boolean

数字类型：number

字符串类型：string

数组类型：array	两种定义方式：

```javascript
1. let arr:number[] =  [ 1,2,3 ]	let arr:string[] = [ '你好', 'world' ]
2. let arr:Array<number> = [ 1,2,3 ]		let arr:Array<string> = [ '你好', 'world' ]
```

元组类型：tuple	数组的一种,指定内部数据的类型						

```js
let arr:[string,number,boolean] = ["world", 1.2, false]
```

枚举类型：enum	主要用于标识状态和固定值 要是没赋值默认是索引值

void 类型：方法函数没有返回任何类型

任意类型：any	

其它类型：unll	undefined



### 函数：

函数声明式：

```js
functoin run():string{
	return "run";
}
```

匿名函数：

```js
var run = function():number{
	return 123;
}
```

函数参数的可选配置和默认配置：

```js
function run ( name:string="wxm", age ?:number ):any{
		....
}
```

三点运算符 接收多个参数传递

```js
function run ( ...arr:number[] ):number{
	for(var i = 0, i<arr.length, i++){ .... }
		return ....
}
```

#### ts 函数的重载

指两个或两个以上的同名函数，但它们接收的参数的类型不同或参数个数不同

```js
function getInfo ( name:string ):string
function getInfo ( age:number ):number
function getInfo ( param:any ):any{
	if(typeof param === "string"){
		return "name"+param
  }else{
    return "age"+param
  }
}

function getInfo ( name:string ):string
function getInfo (  name:string, age:number ):string
function getInfo ( name:any, age?: any):any{
  if(age){
  	return "name"+name+"age"+age
  }else{
  	return "age"+name
  }
}
```



### 类的声明和定义

```js
class Person{
  name: string
  constructor( n:string ){ // 构造函数  实例化类的时候触发的方法
    this.name = n;
  }
  run():void{
    console.log("this.name");
  }
}
```

