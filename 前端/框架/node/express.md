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
app.use(中间件函数)
```

