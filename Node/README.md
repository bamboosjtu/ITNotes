# Node简介

Node.js是一个JavaScript框架，一般的js脚本只能在浏览器运行，window和documenti其实都是浏览器提供的API，但Node.js基于V8引擎可以运行在操作系统上，而且有很多Core和第三方库，可以用作服务端语言。


## 核心库

### 全局对象
- global
- process


### 内置类型
- Buffer
- EventEmitter
- Promise(deprecated) -> `last call functionality`

 
### 核心模块
- 网络通信
    - stream
    - socket
    - dgram：UDP
    - net：TCP
    - http：HTTP
- 域名解析和URL处理
    - dns
    - url
    - querystring
- 实用工具
    - util
- 进程模块
    - child_process
- 程序控制
    - step
    - async


## 第三方库

- [nodemon](https://www.npmjs.com/package/nodemon)：自动检测源代码变化并重启node服务。
- [validator](https://www.npmjs.com/package/validator)：检查字符串格式。
- [chalk](https://www.npmjs.com/package/chalk)：为字符串输出添加颜色。
- [yargs](https://www.npmjs.com/package/yargs)：处理命令行参数。

### 网络
- [request](https://www.npmjs.com/package/request)：**deprecated**，支持HTTP协议的客户端。

### 数据库
- [mongodb](https://mongodb.github.io/node-mongodb-native/)：文档数据库Mongodb的官方驱动API。
- [mongoose](https://mongoosejs.com/)：文档数据库Mongodb的ORM库。



## 中间件
- [Connect](https://github.com/senchalabs/connect)：一个web中间件框架，集成了至少20个中间件。
    - connect.favicon
    - connect.logger
    - connect.cookieParser & connect.parseCookie
    - connect.cookieSession
    - connect.static
- [JSGI](http://wiki.commonjs.org/wiki/JSGI)
- [Crossroads](https://millermedeiros.github.io/crossroads.js/)：路由重定向。
- [http-proxy](https://www.npmjs.com/package/http-proxy)：转发及反向代理。


## 异步模式
异步模块有`step`和`async`，异步处理模式包括：

- waterfall
- series
- parallel
- queue
- whilst
- until
- auto
- iterator
- apply
- nextTick