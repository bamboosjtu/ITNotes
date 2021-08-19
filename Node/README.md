# Node简介

Node.js是一个JavaScript框架，一般的js脚本只能在浏览器运行，window和documenti其实都是浏览器提供的API，但Node.js基于V8引擎可以运行在操作系统上，而且有很多Core和第三方库，可以用作服务端语言。


## 核心库
### 全局对象
- global
- process
- console

### 重要类型
- Buffer
- EventEmitter
- Promise(deprecated) -> await & async

### 进程和异步
工具模块包括：
- child_process
- step
- async

异步处理模式包括：
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

### 工具模块
- 网络通信
  - stream
  - socket
  - dgram：UDP
  - net：TCP
  - http：HTTP
  - [request](https://www.npmjs.com/package/request)：**deprecated**，支持HTTP协议的客户端。

- WEB工具
  - dns
  - url
  - querystring

- 实用工具
  - util：包含`format`、`inspect`、`inherits`等实用函数。
  - underscore
  - lodash
  - [nodemon](https://www.npmjs.com/package/nodemon)：自动检测源代码变化并重启node服务。
  - [validator](https://www.npmjs.com/package/validator)：检查字符串格式。
  - [chalk](https://www.npmjs.com/package/chalk)：为字符串输出添加颜色。
  - repl
  
- 命令行
  - [yargs](https://www.npmjs.com/package/yargs)：处理命令行参数。
  - commander

- 环境变量
  - [env-cmd](https://www.npmjs.com/package/env-cmd)：通过`.env`文件管理配置开发/生产/测试环境，在`package.json`文件中配置。

- 安全&认证
  - bcryptjs：加密用户密码。
  - jsonwebtoken：根据用户身份提供经过**非对称加密**和**base64编码**的token。

- 多媒体：Node操作图形程序和音视频，一是可以通过子进程访问操作系统工具，此方法对windows平台支持较差，二是直接使用模块。
  - PDF
    - PDF Toolkit工具：分解、合并PDF文档，填写PDF表单，加水印，旋转页面，压缩与解压，修改文档。
    - wkhtmltopdf工具：通过WebKit渲染机制将HTML转换为PDF文件，实现对网页的截屏。
    - `pdfkit`：`coffeescript`编写的，提供了创建PDF文档，添加页面，组织文本和图形以及嵌入图片的功能。未来还会有PDF提纲、渐变、表格以及其他特性。
  - Canvas
    - canvas：基于`Cario`的向量图形库。
  - 图片
    - ImageMagick工具：命令行图形工具，制作动画、裁剪尺寸。
    - `imagemadick`：提供了对`ImageMagick`功能的封装；
    - `sharp`：提供图片压缩、格式转换等功能。
  - 视频：包含HTML5 video的程序需要使用`Connect`模块的静态网络服务器，无法使用自制Web服务器，因为自制Web服务器无法处理HTTP ranges。
  - 邮件
    - [SendGrid服务](htt[s://www.sendgrid.com])：第三方邮件服务
    - `Emailjs`：提供一个简易的邮件服务器。
  - 文件
    - multer：处理`multipart/form-data`的中间件，主要用于上传文件。



## 数据库
### 文档数据库
- [mongodb](https://mongodb.github.io/node-mongodb-native/)：文档数据库Mongodb的官方驱动API。
- [mongoose](https://mongoosejs.com/)：文档数据库Mongodb的ORM库，并提供了数据验证的中间件。

### K-V数据库
- redis
- hiredis：非阻塞的，可以提高性能

### 关系型数据库
- db-mysql：不支持事务操作
- node-mysql：不支持事务操作
    - mysql-queues：提供多重查询和数据库事务支持
- sequelize：提供ORM支持，但不支持事务



## Web框架
[Express](./Express.md)：一个WEB框架，与`Connect`是同一个作者，框架本身提供了路由等中间件，用户也可以自定义中间件`(req, res, next) => {}`。

```mermaid
graph LR
    A[new request] --> B[do something]
    B --> C[run route handler];
```

- [Connect](https://github.com/senchalabs/connect)：一个web中间件框架，集成了至少20个中间件。
  - connect.favicon
  - connect.logger
  - connect.cookieParser & connect.parseCookie
  - connect.cookieSession
  - connect.static
- [JSGI](http://wiki.commonjs.org/wiki/JSGI)
- [Crossroads](https://millermedeiros.github.io/crossroads.js/)：路由重定向。
- [http-proxy](https://www.npmjs.com/package/http-proxy)：转发及反向代理。



## 网络通信
WebSockets：一种Web技术，可以在客户端与服务器之间建立直接的实时双向通信，但不是所有的浏览器都支持。

`Socket.IO`通过灵活采用不同机制（WebSockets、Adobe Flash Socket、Ajax long polling、Ajax multipart streaming、Forever iFrame for IE、JSONP Polling），使得浏览器与服务器之间可以建立双向通信，npm模块官网[见此](https://www.npmjs.com/package/socket.io)。编写代码时，服务器与客户端之间相互触发事件。



## 测试
- [Jest](https://jestjs.io)
- [MOCHA](https://mochajs.org)
- [`supertest`](https://www.npmjs.com/package/supertest)：一个WEB测试框架，既可以单独使用，也可以配合其他框架使用。


