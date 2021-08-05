# Express

是Node语言的一个Web服务器框架，官网是`expressjs.com`。
5
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
 - [hbs](https://www.npmjs.com/package/hbs)：`Express`的`handlerbars`，通过模板提供动态视图，模板以`.hbs`为后缀，位置在`<project>/views/`文件夹下

 ```js
app.set('view engine', 'hbs')

app.get('/about', (req, res) => {
    res.render('about', {
        title: 'App',
        name: 'Andrew'
    })
})
 ```

`views/about.hbs`内容如下：
```html
<html>
    <head></head>
    <body>
        <h1>{{ title }}</h1>
        <p>Created by {{ name }}</p>
    </body>
</html>
 ```