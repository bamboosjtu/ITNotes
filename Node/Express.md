# Express

是Node语言的一个Web服务器框架，官网是`expressjs.com`，与`Connect`是同一个作者，因此有类似之处。

## 安装
```bash
npm install express
express site
npm install -d

node app.js
```

## 简单主文件

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
### 模板
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


- jade



## 其他框架
- `Express-Resource`提供了简化的MVC功能
- `RailwayJS`基于`Express`，并仿照`Ruby on Rails`
- `Tower.js`是一个完整支持MVC的Web框架
