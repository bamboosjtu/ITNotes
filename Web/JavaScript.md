# JavaScript简介


## 内置类型

### Promise
- [MDN 使用Promise](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Using_promises)
- [阮一峰 Promise对象](https://javascript.ruanyifeng.com/advanced/promise.html)
- [菜鸟教程 JavaScript Primise](https://www.runoob.com/js/js-promise.html)
- [菜鸟教程 JavaScript Promise 对象](https://www.runoob.com/w3cnote/javascript-promise-object.html)


## 常用的第三方库
- jQuery：屏蔽了浏览器对DOM API实现的差异性，提供了更加简单的Ajax API。
- [Moment.js](https://momentjs.com/)：功能强大的日期类库，有两个版本：一种支持时区，一种不支持。
- [Numberal.js](http://numeraljs.com/)：格式化数字。
- [seedrandom.js](https://github.com/davidbau/seedrandom)：js的伪随机数无法设置随机种子，本库可以使用随机种子来生成伪随机数。
- [Mustache](https://github.com/janl/mustache.js)：模板系统。
- qs.js：提供更强大的URL参数解析功能。
- MediaElement.js：嵌入能播放MP4视频的Flash备用播放器，使得HTML5的音视频兼容旧浏览器。



## 服务端编程
服务端编程常用Node。常规的JS一般运行在浏览器中，Node使用v8引擎编译后，可以运行在服务器上。

### 服务端框架
- Express
- Koa



## 用户端编程
- 请求服务端数据
```js
fetch(ENDPOINT).then((response) => {
    response.JSON().then((data) => {
        if(data.error) {
            // error handle
            console.log(data.error)
        } else {
            console.log(data)
        }
    })
})
```

- 监听页面事件
```js
const widget = document.querySelector('form')
widget.addEventListener('submit', (e) => {
    e.preventDefault()
    console.log('listening.')
})
```