# 工具软件

## 一、数据库
- [PonyOrm](https://ponyorm.org/)：提供在线的工具绘制ER图。
- SQLAlchemy
- Peewee

## 二、Web
### （一）中间件
- [Gunicorn](https://gunicorn.org/)：一款Python WSGI HTTP服务器，仅用于Linux系统，语法为`gunicorn app:<应用名>`
- [Werkzeug](https://werkzeug-docs-cn.readthedocs.io/zh_CN/latest/)：一个基础的WSGI工具包，可作为Web框架底层库。

### （二）Web开发框架
- [web.py](https://webpy.org/)：一个Web框架，非常简单。
- [bottle](https://www.osgeo.cn/bottle/)：一个Web框架，只依赖Python核心库。
- [Flask](https://flask.palletsprojects.com/en/2.0.x/)：一个Web框架，特点是小，基于WSGI，框架本身只提供核心能力，不提供数据库相关功能。
- [Tornado](https://www.tornadoweb.org/en/stable/)：一个Web框架，特点是高性能（异步和非阻塞），不基于WSGI协议。
- [Django](https://www.djangoproject.com/)：一个Web框架，功能比较齐全，定制化难度较大。


## 三、并发编程
- gevent
- greenlet
- gthread


## 四、Django插件
- xadmin：
提供基于Bootstrap管理后台，但与Django 2以上的兼容性非常不好，需要大量修改。

- django-autocomplete-light：
提供自动补全功能。

- django-rest-framework：
提供Restful API功能。

- django-ckeditor：
提供富文本编辑器的功能。

- django-haystack：
提供基于haystack的搜索功能。

- django-debug-toobar：
排查性能，优化项目，还可以在此基础上继续开发面板，如djdt_flamegraph（函数调用耗时）、pympler（内存使用情况）、line-profiler（行级性能分析）等。

- silk：
jazzband组织下的东西，有django插件可用于分析项目性能。

- django-redis：
提供redis缓存功能，一般还会配合`hiredis`以增强性能。

- django-simple-captcha：
提供验证码功能。