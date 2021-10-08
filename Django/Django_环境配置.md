# 环境配置

## 一、Django核心配置
### （一）数据库
- DATABASES
是一个嵌套字典对象，字典的Key是数据库别名（必须包含default），字典的值是数据库配置信息，可以指定多个数据库。指定网站所使用的数据库类型以及连接方式。

- DATABASE_ROUTERS
是一个列表，列表元素是一个实现了特殊路由方法的Python类的路径。数据库路由配置，当执行数据库操作时，Django会根据路由配置选择恰当的数据库执行操作。


### （二）文件上传
- DEFAULT_FILE_STORAGE
任何文件操作所使用的文件系统。

- FILE_CHARSET
从磁盘读取文件时所使用的编码格式，默认值是"utf-8"，包括读取模板文件和数据库文件的方式。

- FILE_UPLOAD_HANDLERS
文件上传处理程序。

- FILE_UPLOAD_MAX_MEMORY_SIZE
允许上传的文件的最大体积，单位为字节（B），默认值为2.5MB.

- FILE_UPLOAD_PERMISSIONS
为上传的文件设置权限，默认值为None，可选值为Linux文件权限的数值模式。

- FILE_UPLOAD_DIRECTORY_PERMISSIONS
为上传文件过程中所创建的文件夹设置权限，其他同上。

- FILE_UPLOAD_TEMP_DIR
文件上传时，文件的临时存放路径，默认为None，由系统默认。

- MEDIA_ROOT
用于保存上传文件的绝对路径，默认是空字符串，不可与STATIC_ROOT相同。使用前需要修改urls.py和TEMPLATES设置。

- MEDIA_URL
用于处理MEDIA_ROOT中所保存文件的URL，如果不为空必须以`/`结尾。


### （三）调试
- DEBUG
用于开启调试模式，如果出现异常情况，异常信息会被输出到网页上。

- DEBUG_PROPAGATE_EXCEPTIONS
当Django的视图方法出现异常或者需要返回HTTP 500的响应时，异常信息会被Web服务器接收而不是Django处理。


### （四）HTTP
- DATA_UPLOAD_MAX_MEMORY_SIZE
一次HTTP请求最大的体积，单位为字节，默认是2.5MB，检查内容不包括正在上传的文件体积。

- DATA_UPLOAD_MAX_NUMBER_FIELDS
一次HTTP请求所能接收的最大参数数量，包括GET请求和POST请求，默认为1000。

- DEFAULT_CHARSET
HTTP响应默认使用的字符集，默认是`utf-8`。

- DEFAULT_CONTENT_TYPE
HTTP响应默认的文档类型，默认是`text/html`。

- WSGI_APPLICATION
指向WSGI应用的Python路径。


### （五）国际化
- DATE_FORMAT
- DATE_INPUT_FORMATS
- DATETIME_FORMAT
- DATETIME_INPUT_FORMATS
- TIME_FORMAT
- TIME_INPUT_FORMATS

- TIME_ZONE
中国所在时区为`Asia/Shanghai`。

- USE_I18N
表示是否启用翻译系统，为True时，LANGUAGE_CODE才能生效，Django将系统语言翻译成LANGUAGE_CODE指定的语言。

- USE_L10N
表示是否启用格式化系统，为True时，Django会对数字、日期、时间等字符串格式化。

- USE_TZ
表示是否使用UTC时间，为True时，所有系统中的时间被自动转换为UTC时间。

- LANGUAGE_CODE
默认为`en-US`，简体中文为`zh-Hans`。


### （六）日志
- LOGGING
表示日志配置信息。

- LOGGING_CONFIG
指向一个用于配置日志系统的可调用对象的路径，如果为None，代表禁用日志功能。


### （七）模板
- TEMPLATES


### （八）安全
跨站请问伪造保护：
- CSRF_COOKIE_AGE
- CSRF_COOKIE_DOMAIN
- CSRF_COOKIE_NAME
- CSRF_COOKIE_PATH
- CSRF_COOKIE_SECURE
- CSRF_USE_SESSIONS
- CSRF_FAILURE_VIEW
- CSRF_HEADER_NAME
- CSRF_TRUSTED_ORIGINS

Django工程的密钥，用于加密签名，在创建时会自动创建，不要上传GITHUB。
- SECRET_KEY


### （九）URL
- ROOT_URLCONF
URL配置的根位置。

- APPEND_SLASH
为True时，如果访问的URL不是以`/`为结尾，并且路由系统没有在URLConf中找到匹配的URL，会自动添加`/`。

- PREPEND_WWW
优先使用WWW作为URL前缀。



## 二、第三方软件安装

### （一）数据库
MySQL在Ubuntu 环境下，大致如下

1. 安装：`sudo apt-get install mysql-server`
2. 创建工作目录：`sudo mkdir -p /var/run/mysqld && sudo chown mysql /var/run/mysqld/ && sudo service mysql restart`
3. 初始化（设置密码）：`sudo mysql_secure_installation`
4. 登陆：`sudo mysql -uroot -p`
5. 创建数据库：`CREATE DATABASE <数据库名> CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;`
6. 创建用户：`CREATE USER '<用户名>'@'%' IDENTIFIED  BY '<密码>';`
7. 配置用户权限：`GRANT ALL PRIVILEGES ON <数据库名>.<表名> TO <用户名>@'%';`
8. 刷新配置：`FLUSH PRIVILEGES;`
9. 修改配置文件（可选）：`/etc/mysql/mysql.conf.d/mysqld.cnf`
10. 安装python包：`pipenv install pymysql && pipenv install cryptography`