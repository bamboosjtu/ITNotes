# Express

是Node语言的一个Web服务器框架，官网是`expressjs.com`，与`Connect`是同一个作者，因此有类似之处。

## 安装
```bash
npm install express
express site
npm install -d

node app.js
```

## 简单示例

```js
const path = require('path')
const express = require('express')

const app = express()
const publicDirectoryPath = path.join(__dirname, '../public')

app.use(express.static(publicDirectoryPath))

app.get('', (req, res) => {
    res.send('Hello express!')
})

app.get('/help', (req, res) => {
    res.send({
        name: 'andrew',
        age: 27
    })
})

app.listen(3000, () => {
    console.log('Server is up on port 3000.')
})
 ```


## 插件
### 输入验证
- Joi


### 中间件（Middleware）
中间件是一个函数`function(req, res, next)`，对HTTP请求和响应进行修改。

- 自定义中间件
```js
app.use(function(req, res, next){
    console.log('logging')
    next()
})
``` 

- 内置中间件
```js
app.use(express.json())
app.use(express.urlencode())
app.use(express.static('public'))
```

- 第三方中间件


### 配置工具
- rc
- config



### 调试工具
- debug



### 模板引擎
- [hbs](https://www.npmjs.com/package/hbs)：`Express`的`handlerbars`，一个模板引擎，模板以`.hbs`为后缀，默认位置在`<project>/views/`文件夹下，但可以修改。

```js
const express = require('express')
const hbs = require('hbs')

const app = express()

const viewsPath = path.join(__dirname, '../templates/views')
const partialsPath = path.join(__dirname, '../templates/partials')

app.set('view engine', 'hbs')
app.set('views', viewsPath)
hbs.registerPartials(partialsPath)

app.get('/about', (req, res) => {
    res.render('about', {
        title: 'App',
        name: 'Andrew'
    })
})
 ```

模板示例如`views/about.hbs`，
```html
<html>
    <head></head>
    <body>
        <h1>{{ title }}</h1>
        <p>Created by {{ name }}</p>
    </body>
</html>
 ```


- Pug（原Jade）：`Express`默认的模板系统。

- EJS（Embeded Javascript）：基于`Ruby EJB`的模板系统

- Mustache

模板引擎除了`tag`语法外，一般还包括`filter`等功能。



### 数据库集成
- mongoose



### 鉴权（Authentication）



### 路由（Router）
```js
// api.js
const router = express.Router()

modulue.exports = router

// index.js
const api = require('api.ks')
app.use('/api', api)

```




## 其他框架
- `Express-Resource`提供了简化的MVC功能
- `RailwayJS`基于`Express`，并仿照`Ruby on Rails`
- `Tower.js`是一个完整支持MVC的Web框架



