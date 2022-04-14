#### express本质是npm第三方的包，用于快速创建web服务器或API接口服务器

基于node.js内部的http内置模块Api的封装，

安装 npm install express 

##### nodemon：

自动的监测nodejs项目并启动  使用：nodemon app.js

全局安装：npm install -g nodemon



##### 路由

路由就是映射关系，（客户端请求和服务器处理函数的映射关系），express路由由三部分组成：请求的类型、请求的URL地址、处理函数：

```js
app.method(path,handle(){});
```

模块化路由：不建议直接挂载到app上，要单独的抽离出路由

在主文件demo.js中调用路由：

```js
const express = require('express');
const app = new express();
// 注册导入的路由模块
const userrouter = require('./router');
// app.use() 函数的作用：注册全局中间件
app.use(userrouter);
app.listen(80, function (err) {
    if (!err) console.log('http://localhost:127.0.0.1')
})
```

在router.js文件中初始化路由

```js
const express = require('express');
// 创建路由对象
const router = express.Router();
// 挂载路由
router.get('/person', (req, res) => {
    res.send("get person");
});
router.post('/info', (req, res) => {
    res.send("get info");
});
// 向外导出module对象，提供router
module.exports = router;

```



#### 中间件

中间处理流程，在express 中的中间件本质是一个function处理函数，

```js
app.get('/',function(req,res,next){
	... 
  next();
})
```

上示function为中间件格式，必须包含next参数

### next（） 

函数的作用：实现多个中间件连续调用的关键，表示吧流转关系转交给下一个中间件或路由。

全局生效的中间价函数：在客户端发起请求，到达服务器之后，都会触发的中间件

```js
// 简写形式：app.use(中间件函数);
app.use(function(req,res,next)=>{
        next();
        });
```

多个中间件之间，共享通一份req和res，基于此，我们可以在上游的中间件中统一为req或者res对象添加属性和方法，供下游调用，（例如：拦截器）

局部中间件：不使用 app.use()，方法挂载，局部生效的中间件

```js
const mv = function(req,res,next)=>{
        next();
        };
// 只会影响 / 这个请求
app.get('/',mv,function(req,res)=>{
        ...
        })
// 定义使用多个中间件
app.get('/',mv,mv1,mv2,function(req,res)=>{
        ...
        })
// 或者使用数组接收
app.get('/',[mv,mv1,mv2],function(req,res)=>{
        ...
        })
```

##### 中间件使用注意事项

一定要在路由前注册中间件

客户端发来的请求可以通过多个中间件

执行完中间件一定要用 next() 函数

为防止逻辑混乱在 next() 后面不写代码

连续调用多个中间件时，中间件共享req 和 res

##### 中间件分类

应用级别：绑定到 app.use() app.get() app.post() 的中间件

路由级别：绑定到 express.Router() 实例上的中间件

错误级别：专门捕获整个项目发生的异常错误，防止项目异常崩溃，错误级别的中间件必须有四个参数，（err,req,res,next）;必须注册在所有路由之后

```js
app.get('/',function(req,res)=>{
        ...
        })
app.use(function(err,req,res,next)=>{
        res.send("Error!"+err.message);
        })
```

Express内置：

express.static：快速托管静态资源的内置中间件

express.json：解析JSON格式的请求体数据

express.urlencoded：解析URL-encoded格式的请求体数据

第三方中间件