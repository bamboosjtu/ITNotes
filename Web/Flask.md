# Flask简介

Flask是一个微型框架，主要的三个依赖：路由、调试和WSGI由Werkzeug提供，模板系统由Jinja2提供，命令行集成由Click提供。

数据库访问、Web表单验证、用户身份验证等都需要第三方插件。


常件插件有：

- flask-bootstrap
- flask-moment
- flask-wtf
- flask-sqlalchemy
- flask-migrate
- flask-mail
- flask-login
- flask-httpauth
- flask-sslify
- flask-pagedown
- markdown
- bleach
- httpie
- coverage
- selenium




## 一、Flask基本应用

```python
from flask import Flask, request, render_template

app = Flask(__name__)

@app.route("/")
def index():
    return "<h1>Hello World!</h1>"

@app.route("/user/<name>")
def user(name):
    user_agent = request.headers.get("User-Agent")
    return render_template('user.html', name=name)

if __name__=="__main__":
    app.run()
```



### （一）路由分发

路由规则保存在应用的`url_map`属性中，Flask自动添加静态路由static。

Flask还提供了辅助函数`url_for(name:str, **kwargs:str, _external:bool)`来动态生成URL。


- 装饰器

```python
@app.route("/")
def index():
    return '<h1>Hello!</h1>'

@app.errorhandle(404)
def page_not_found(e):
    return render_template('404.html'), 404
```


- 注册

```python
def index():
    return '<h1>Hello!</h1>'

app.add_url_rule('/', "index", index)
```



### （二）请求—响应循环

#### 1. 应用和请求上下文

Flask使用上下文临时把某些对象编程全局可访问，从而编写视图函数。

| 变量名      | 上下文     | 说明                                                 |
| ----------- | ---------- | ---------------------------------------------------- |
| current_app | 应用上下文 | 当前应用实例                                         |
| g           | 应用上下文 | 处理请求时用作临时存储对象，每次请求都会重置这个变量 |
| request     | 请求上下文 | 封装了客户端发出的HTTP请求中的内容                   |
| session     | 请求上下文 | 用户会话，值为一个字典                               |



可以通过装饰器注册应用上下文对象，如下

```python
@main.app_context_processor
def inject_permissions():
    return dict(Permission=Permission)
```





#### 2. 请求

Flask通过上下文变量`request`对外开放请求对象。

| 属性或方法   | 说明                                                 |
| ------------ | ---------------------------------------------------- |
| form         | 字典，存储请求提交的表单字段                         |
| args         | 字典，存储通过URL查询查询字符串传递的所有参数        |
| values       | 字典，form和args的并集                               |
| cookies      | 字典，存储所有的cookie                               |
| headers      | 字典，存储所有请求的HTTP头部                         |
| files        | 字典，存储上传的所有文件                             |
| get_data()   | 返回请求主体缓冲的数据                               |
| get_json()   | 返回一个字典，包含解析请求主体后得到的JSON           |
| blueprint    | 处理请求的Flask蓝本的名称                            |
| endpoint     | 处理请求的Flask端点的名称                            |
| method       | 请求方法，如GET                                      |
| scheme       | URL方案，如https                                     |
| is_secure()  | 通过HTTPS发送请求时返回true                          |
| host         | 请求定义的主机名，如客户端定义了端口号，还包括端口号 |
| path         | URL的路径部分                                        |
| query_string | URL的查询字符串部分                                  |
| full_path    | path+query_string                                    |
| url          | 客户端请求的完整URL                                  |
| base_url     | url去掉查询字符串报复嗯                              |
| remote_addr  | 客户端的IP地址                                       |
| environ      | 请求的WSGI环境字典                                   |



#### 3. 响应

| 属性或方法      | 说明                         |
| --------------- | ---------------------------- |
| status_code     | HTTP数字状态码               |
| headers         | 字典，存储所有响应的HTTP头部 |
| set_cookie()    | 添加一个cookie               |
| delete_cookie() | 删除一个cookie               |
| content_length  | 响应主体的长度               |
| content_type    | 响应主体的媒体类型           |
| set_data()      | 使用字符串或者字节值设定响应 |
| get_data()      | 返回响应主体                 |



#### 4. 请求钩子

| 钩子装饰器           | 说明                         |
| -------------------- | ---------------------------- |
| before_request       | 在每次请求前允许             |
| before_first_request | 在第一个请求之前运行         |
| after_request        | 在所有处理无异常的请求后运行 |
| teardown_request     | 在所有请求后运行             |



### （三）模板

Flask使用的是Jinja2模板，可以自定义过滤器、宏、标记等。



### （四）表单

flask-wtf包队独立的WTFormss进行了包装，可以提升Flask处理Web的能力，使用时不需要在应用层初始化，但是要配置一个密钥。

#### 1. 用于视图函数

```python
from flask_wft import FlaskForm
from wtforms import StringField, SubmitField
from wtforms.validators import DataRequired

app.config["SECRET_KEY"] = "stored in envinron"

class NameForm(FlaskForm):
    name = StringField("What is your name?", validators=[DataRequired()])
    submit = SubmitField("Submit")
    
@app.route("/", methods=["GET", "POST"])
def index():
    name = None
    form = NameForm()
    if form.validate_on_submit():
        name = form.name.data
        form.name.data = ""
    return render_template("index.html", form=form, name=name)
```



#### 2. 用于模板

- 使用Bootstrap模板，`wtf.quick_form(form)`

- 直接使用表单，`form.name(id="my-text-field")`等



#### 3. WTForms字段

| 字段类型            | 说明                                |
| ------------------- | ----------------------------------- |
| BooleanField        | 复选框，值为True或False             |
| RadioField          | 一组单选按钮                        |
| SelectField         | 下拉列表                            |
| SelectMultipleField | 下拉列表，可选择多个值              |
| DateField           | 文本字段，值为datetime.date格式     |
| DateTimeField       | 文本字段，值为datetime.datetime格式 |
| DecimalField        | 文本字段，值为decimal.Decimal格式   |
| FloatField          | 文本字段，值为浮点数                |
| ImtegerField        | 文本字段，值为整数                  |
| PasswordField       | 密码文本字段                        |
| StringField         | 文本字段                            |
| TextAreaField       | 多行文本字段                        |
| FileField           | 文件上传字段                        |
| MultipleFileField   | 多文件上传字段                      |
| HiddenField         | 隐藏的文本字段                      |
| FormField           | 把一个表单作为字段嵌入另一个表单    |
| SubmitField         | 表单提交按钮                        |



#### 4. WTForms验证函数

| 验证函数      | 说明                                 |
| ------------- | ------------------------------------ |
| DataRequired  | 转换后字段必须有数据                 |
| InputRequired | 字段为必填项                         |
| Optional      | 允许字段无输入，并且跳过其他验证函数 |
| Email         | 字段必须满足Email格式                |
| IPAddress     | 字段必须满足IP地址格式               |
| MacAddress    | 字段必须满足MAC地址格式              |
| URL           | 字段必须满足URL格式                  |
| UUID          | 字段必须满足UUID格式                 |
| NumberRange   | 字段必须在数字范围内                 |
| Anyof         | 字段值的白名单                       |
| Noneof        | 字段值的黑名单                       |
| EqualTo       | 比较两个字段的值，常用于再次输入密码 |
| Regexp        | 字段必须满足正则表达式条件           |
| Length        | 字段长度的要求                       |



此外，FlaskForm还可以对自定义字段的验证函数，`validate_<fieldname>(self, field)`

```python
def validate_username(self, field):
        if User.query.filter_by(username=field.data).first():
            raise ValidationError('用户名已存在')
```




### （五）模型

Flask-SQLAlchemy包扩展了Flask的ORM功能，在ORM模型中用`db.Column`定义字段。

```python
from flask import Flask
from flask_sqlalchemy import SQLAlchemy
import os

basedir = os.path.abspath(os.path.dirname(__file__))

app = Flask(__name__)
app.config["SQLALCHEMY_DATABASE_URI"] = f"sqlite:///{os.path.join(basedir, 'data.sqlite')}"
app.config["SQLALCHEMY_TRACK_MODIFICATIONS"] = False

db = SQLAlchemy(app)

class Role(db.Model):
    __tablename__ = "roles"
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(64), unique=True)
    users = db.relationship('User', backref="role", lazy="dynamic")

    def __repr__(self):
        return f"<Role {self.name}>"


class User(db.Model):
    __tablename__ = "users"
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(64), unique=True, index=True)
    role_id = db.Column(db.Integer, db.ForeignKey('roles.id'))

    def __repr__(self):
        return f"<User {self.username}>"
```


#### 1. 列字段类型

| 列字段类型   | Python类型         | 说明                            |
| ------------ | ------------------ | ------------------------------- |
| Integer      | int                | 普通整数                        |
| SmallInteger | int                | 小整数                          |
| BigInteger   | int                | 不限制精度的整数                |
| Float        | float              | 浮点数                          |
| Numeric      | decimal.Decimal    | 定点数                          |
| String       | str                | 变长字符串                      |
| Text         | str                | 变长字符串，常用于长文本        |
| Unicode      | unicode            | 变长Unicode字符串               |
| UnicodeText  | unicode            | 变长Unicode字符串，常用于长文本 |
| Boolean      | bool               | 布尔值                          |
| Date         | datetime.date      | 日期                            |
| Time         | datetime.time      | 时间                            |
| DateTime     | datetime.datetime  | 日期和时间                      |
| Interval     | datetime.timedelta | 时间间隔                        |
| Enum         | str                | 一组字符串                      |
| PickleType   | 任何Python对象     | 自动使用Pickle序列化            |
| LargeBinary  | str                | 二进制blob                      |



#### 2. 列选项

| 列选项      | 说明           |
| ----------- | -------------- |
| primary_key | 是否为主键     |
| unique      | 是否唯一       |
| index       | 是否为索引     |
| nullable    | 是否允许为空值 |
| default     | 定义默认值     |


#### 3. 关系

- 在”多“端定义外键字段`db.Column(db.Integer, db.ForeignKey('roles.id'))`。
- 在”一“端定义反向引用`db.relationship('User', backref='role')`。

| 关系选项      | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| backref       | 定义在一端，为多端添加反向引用                               |
| primaryjoin   | 为模棱两可的关系明确指定联结条件                             |
| secondary     | 指定多对多关系中联结表名称                                   |
| secondaryjoin | 指定多对多关系中的二级联结条件                               |
| lazy          | 指定如何加载相关记录，可选值有select、immediate、joined、subquery、noload、dynamic |
| uselist       | True则使用列表，False则使用标量值                            |
| order_by      | 记录排序方式                                                 |



#### 4. 数据库操作

##### （1）DDL

| 关系选项        | 说明     |
| --------------- | -------- |
| db.create_all() | 创建表   |
| db.drop_all()   | 删除旧表 |


##### （2）CRUD

| 关系选项                                    | 说明                     |
| ------------------------------------------- | ------------------------ |
| admin_role = Role(name="Admin")             | 创建记录                 |
| admin_role.name = "Administrator"           | 修改记录                 |
| db.session.add(admin_role)                  | 数据库添加或更新记录     |
| db.session.add_all([admin_role, user_role]) | 数据库添加或更新一组记录 |
| db.session.delete(admin_role)               | 数据库删除记录           |
| db.session.remove()                         | 删除全部记录             |
| db.session.commit()                         | 数据库提交事务           |
| db.session.rollback()                       | 数据库回滚事务           |


##### （3）查询

Flask-Alchemy为每个模型类都提供了query对象用于查询。

| 方法           | 说明                                            |
| -------------- | ----------------------------------------------- |
| all()          | 返回全部记录                                    |
| first()        | 返回第一条记录，没有结果则返回None              |
| first_or_404() | 返回第一条记录，没有结果则抛出404错误响应       |
| get()          | 返回指定主键对应的行，没有结果则返回None        |
| get_or_404()   | 返回指定主键对应的行，没有结果则抛出404错误响应 |
| count()        | 返回查询记录的数量                              |
| paginate()     | 返回一个Paginate对象，包含指定范围内的记录      |


##### （4）查询过滤器

过滤器应用于query对象上。

| 过滤器      | 说明                                         |
| ----------- | -------------------------------------------- |
| filter()    | 把过滤器添加到原查询上，返回一个新查询       |
| filter_by() | 把等值过滤器添加到原查询上，返回一个新查询   |
| limit()     | 限制原查询返回的记录数量，返回一个新查询     |
| offset()    | 偏移原查询返回的结果，返回一个新查询         |
| order_by()  | 根据指定条件对原查询结果排序，返回一个新查询 |
| group_by()  | 根据指定条件对原查询结果排序，返回一个新查询 |



#### 5. 分页
SQLAlechmy通过Pagination对象提供分页功能，调用query对象的paginate()方法可以得到分页对象。

```python
page = request.args.get('page', 1, type=int)
pagination = Post.query.order_by(Post.timestamp.desc()).paginate(
                page, per_page=current_app.config['FLASKY_POSTS_PER_PAGE'],
                error_out=False)
posts = pagination.items
```

分页对象有一系列的属性和方法：

| 属性或方法                                                   | 说明                                             |
| ------------------------------------------------------------ | ------------------------------------------------ |
| items                                                        | 当前页面中的记录                                 |
| query                                                        | 分页的源查询                                     |
| page                                                         | 当前页数                                         |
| prev_num                                                     | 上一页的页数                                     |
| next_num                                                     | 下一页的页数                                     |
| has_next                                                     | 如果有下一页，值为True                           |
| has_prev                                                     | 如果有上一页，值为True                           |
| pages                                                        | 查询的总页数                                     |
| per_page                                                     | 每页显示的记录数量                               |
| total                                                        | 查询返回的总记录数                               |
| iter_pages(left_edge, left_current, right_current, right_edge) | 一个迭代器，返回一个在分页导航中显示的页数列表。 |
| prev()                                                       | 上一页的分页对象                                 |
| next()                                                       | 下一页的分页对象                                 |



#### 6. 事件

SqlAlchemy可以监听模型字段变化的事件。

```python
class Post(db.Model):
    # ……
    @staticmethod
    def on_changed_body(target, value, oldvalue, initiator):
        import bleach
        from markdown import markdown
        allowed_tags = ['a', 'abbr', 'acronym', 'b', 'blockquote', 'code', 'em', 'i', 'li', 'ol', 'pre', 
                        'strong', 'ul', 'h1', 'h2', 'h3', 'p']
        target.body_html = bleach.linkify(bleach.clean(markdown(value, output_format='html'), 
                                                       tags=allowed_tags, strip=True))
        
db.event.listen(Post.body, 'set', Post.on_changed_body)
```





### （六）命令行

#### 1. 上下文

定义`FLASK_APP`环境变量后，可命令行使用`flask shell`进行后台管理。

在代码中使用`app.shell_context_processor`装饰器创建上下文处理器，自动导入常用对象。

```python
@app.shell_context_processor
def make_shell_context():
    return dict(db=db, User=User, Role=Role)
```



#### 2. 新命令

在代码中使用`app.cli.command()`装饰器可以定义新命令

```python
@app.cli.command()
def test():
    import unittest
    tests = unittest.TestLoader().discover('tests')
    unittest.TextTestRunner(verbosity=2).run(tests)
```

以上定义了单元测试命令，可以通过命令行`flask test`运行单元测试。




### （七）静态文件

默认情况下，Flask在应用目录中的static子目录中寻找静态文件。

代码、模板中都可以通过静态路由`url_for('static', filename)`来获取文件。




### （八）缓存

```python
from flask import session, redirect, url_for

@app.route("/", methods=["GET", "POST"])
def index():
    name = None
    form = NameForm()
    if form.validate_on_submit():
        session['name'] = form.name.data
        return redirect(url_for('index'))
    return render_template("index.html", form=form, name=session.get('name'))
```



### （九）闪现消息

闪现消息提供一个通知功能。

- 在视图函数中使用`flash(message)`来发送消息
- 在模板中使用`get_flashed_messages()来获取消息`



## 二、样式

flask-bootstrap插件可以提供Bootstrap功能。

```python
from flask_bootstrap import Bootstrap

# ...
bootsrap = Bootstrap(app)
```


在模板中继承`bootsrap/base.html`来复用Bootstrap的样式，基础模板提供了一些预定义的模块，通过`super()`来保留已有的内容。

| 区块名       | 说明                      |
| ------------ | ------------------------- |
| doc          | 整个HTML文档              |
| html_attribs | html标签的属性            |
| html         | html标签中的内容          |
| head         | head标签中的内容          |
| title        | title标签中的内容         |
| metas        | 一组meta标签              |
| styles       | CSS声明                   |
| body_attribs | body标签的属性            |
| body         | body标签中的内容          |
| navbar       | 用户定义的导航栏          |
| content      | 用户定义的页面内容        |
| scripts      | 文档底部的Javascripts声明 |




## 三、数据库迁移

SQLAlchemy的开发人员编写了一个Alembic的迁移框架，Flask-Migrate包对此进行了轻量级包装，提供了`flask db`命令和几个子命令用于迁移数据库。


```python
from flask_migrate import Migrate

# ...

migrate = Migrate(app, db)
```

| 命令               | 说明                       |
| ------------------ | -------------------------- |
| flask db init      | 添加数据库迁移支持         |
| flask db migrate   | 自动创建迁移脚本           |
| flask db revision  | 手动创建迁移脚本的骨架     |
| flask db upgrade   | 把迁移中的改动应用于数据库 |
| flask db downgrade | 删除改动                   |



## 四、邮件

Flask-Mail包装了smtplib包，提供了电子邮件功能。

| 配置          | 默认值    | 说明                         |
| ------------- | --------- | ---------------------------- |
| MAIL_SERVER   | localhost | 电子邮件服务器主机名或IP地址 |
| MAIL_PORT     | 25        | 电子邮件服务器端口           |
| MAIL_USE_TLS  | False     | 是否启用TLS                  |
| MAIL_USE_SSL  | False     | 是否启用SSL                  |
| MAIL_USERNAME | None      | 邮件账号用户名               |
| MAIL_PASSWORD | None      | 邮件账户密码                 |



```python
from flask_mail import Mail, Message

# ...

mail = Mail(app)

msg = Message('test email', sender='you@example.com', recipients=['them@example.com'])
msg.body = 'This is the plain text body.'
msg.html = 'This is the <b>HTML</b> body!'
with app.app_context():
    mail.send(msg)
```



## 五、工程化

项目结构可参考

```bash
├── app
│   ├── __init__.py
│   ├── email.py
│   ├── models.py
│   ├── main
│   │   ├── __init__.py
│   │   ├── errors.py
│   │   ├── forms.py
│   │   └── views.py
│   ├── static
│   └── templates
│       ├── base.html
│       ├── index.html
│       └── user.html
├── migrations
│   ├── README
│   ├── alembic.ini
│   ├── env.py
│   ├── script.py.mako
│   └── versions
│── tests
│   ├── __init__.py
│   └── test1.py
├── config.py
├── data.sqlite
├── .env
├── requirements.txt
└── flasky.py
```



- 测试环境准备

```python
def setUp(self) -> None:
        self.app = create_app('testing')
        self.app_context = self.app.app_context()
        self.app_context.push()
        db.create_all()
        Role.insert_roles()
        self.client = self.app.test_client(use_cookies=True)
        
def tearDown(self) -> None:
        db.session.remove()
        db.drop_all()
        self.app_context.pop()
```





## 六、用户和密码

为保护数据库中用户密码的安全，不应存储密码本身，而应存储密码的散列值（以密码为输入，添加随机内容——盐值后，再使用单向加密算法计算，最终得到一个和原始密码没有关系的字符序列，且无法还原成原始密码）。



### （一）计算密码散列值

可供选择的模块有：

- werkzeug.security
  - generate_password_hash(password, method="pbkdf2:sha256", salt_length=8)
  - check_passsword_hash(hash, password)
- bcrypt.passlib



### （二）Flask-Login扩展

#### 1. 用户模型

Flask-login要求User对象必须实现以下属性或方法，且提供了UserMixin共User类继承。

| 属性/方法        | 说明                                                         |
| ---------------- | ------------------------------------------------------------ |
| is_authenticated | 如果用户登录凭据有效，则返回True，否则返回False              |
| is_active        | 如果允许用户登录，则返回True，否则返回False                  |
| is_anoymous      | 对普通用户必须始终返回False，对表示匿名用户的特殊对象返回True |
| get_id()         | 返回用户唯一标识符，用Unicode编码                            |

此外，还要通过装饰器`@login_manager.user_loader`注册一个函数，返回已登录用户的id，详情如下。

```python
@login_manager.user_loader
def load_user(user_id):
    return User.query.get(int(user_id))
```



#### 2. 登录保护

##### （1）装饰器

Flask-login提供了一些装饰器保护路由。

- @login_required：视图函数只能在用户登录状态下访问



##### （2） 登录与注销

在视图函数中可以是同以下方法进行用户登录和注销。

- login_user(user, keepin:bool)
- logout_user()



用户登录成功后会把用户ID以字符串的形式写入用户会话，并把用户对象（未登录则为Anonymous实例）赋值给当前请求的current_user的上下文变量。



#### 3. 生成令牌

```python
from itsdangerous import TimedJSONWebSignatureSerializer as Serializer

s = Serializer(current_app.config['SECKET_KEY'], expiration)
token = s.dumps({'confirm': self.id})
data = s.loads(token)
```



## 七、RestfulApI

### （一）HTTP状态码

| HTTP状态码 | 名称               | 状态             | 说明                                   |
| ---------- | ------------------ | ---------------- | -------------------------------------- |
| 200        | OK                 | 成功             | 请求成功                               |
| 201        | Created            | 已创建           | 请求成功，而且创建了一个资源           |
| 202        | Accepted           | 已接收           | 请求已接收，但仍在处理中，将异步处理   |
| 204        | No Content         | 没有内容         | 请求成功处理，但是返回的响应没有数据   |
| 400        | Bad Request        | 错误请求         | 请求无效或者不一致                     |
| 401        | Unauthorized       | 未授权           | 请求未包含身份验证信息或提供的凭据无效 |
| 403        | Forbidden          | 禁止             | 请求中发送的身份验证凭据无权访问目标   |
| 404        | Not Found          | 未找到           | URL对应的资源不存在                    |
| 405        | Method Not Allowed | 不允许使用的方法 | 处理请求的过程发生意外的错误           |



### （二）权限认证

由于要支撑多种客户端，api编程无法通过cookie或者session保持用户状态，一般是通过`flask-httpauth`库来实现鉴权，状态保存在服务端的应用上下文`g`中。



#### 1. **鉴权**

```python
from flask_httpauth import HTTPBasicAuth
auth = HTTPBasicAuth()

@auth.verify_password
def verify_password(email_or_token, password):
    if email_or_token == '':
        return False
    if password == '':
        g.current_user = User.verify_auth_token(email_or_token)
        g.token_used = True
        return g.current_user is not None
    user = User.query.filter_by(email=email_or_token).first()
    if not user:
        return False
    g.current_user = user
    g.token_used = False
    return user.verify_password(password)
```



#### 2. 路由保护

```python
@auth.before_request
@auth.login_required
def before_request():
    if not g.current_user.is_anonymous and not g.current_user.confirmed:
        return forbidden('unconfirmed account')
```



#### 3. 错误处理

```python
@auth.error_handler
def auth_error():
    return unauthorized('Invalid Credintials')
```





### （三）序列化转换

#### 1. 序列化

- 给模型添加序列化方法

```python
# models.py
class Comment(db.Model):
    # ……
    
    def to_json(self):
        json_comment = {
            'url': url_for('api.get_comment', id=self.id),
            'body': self.body,
            'body_html': self.body_html,
            'timestamp': self.timestamp,
            'author_url': url_for('api.get_user', id=self.author_id),
            'post_url': url_for('api.get_post', id=self.post_id),
        }
        return json_comment
```



- 实现端点

```python
from flask.json import jsonify

@api.route('/comments/')
def get_comments():
    page = request.args.get('page', 1, type=int)
    pagination = Comment.query.paginate(page, 
                                        per_page=current_app.config['FLASKY_POSTS_PER_PAGE'], 
                                        error_out=False)
    comments = pagination.items()
    prev = None
    if pagination.has_prev:
        prev = url_for('api.get_comments', page=page-1)
    next = None
    if pagination.has_next:
        next = url_for('api.get_comments', page=page+1)
    return jsonify({
        'posts': [comment.to_json() for comment in comments],
        'prev_url': prev,
        'next_url': next,
        'count': pagination.total
    })
```



#### 2. 反序列化

- 给模型添加反序列化方法

```python
class Post(db.Model):
    # ……
    
    @staticmethod
    def from_json(json_post):
        body = json_post.get('body')
        if body is None or body == '':
            raise ValidationError('post does not have a body.')
        return Post(body=body)
```



- 实现端点

```python
@api.route('/posts/', method=['POST'])
@permission_required(Permission.WRITE)
def new_post():
    post = Post.from_json(request.json)
    post.author = g.current_user
    db.session.add(post)
    db.session.commit()
    return jsonify(post.to_json()), 201, {'Location': url_for('api.get_post', id=post.id)}
```



### （四）接口测试

测试Web服务需要使用HTTP客户端，常用的工具有：

- cURL
- HTTPie

```bash
http --json --auth <email>:<password> GET http://127.0.0.1:5000/api/v1/posts
```

