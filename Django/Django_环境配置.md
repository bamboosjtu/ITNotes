# 环境配置

## Django核心配置
### 数据库
- DATABASES
是一个嵌套字典对象，字典的Key是数据库别名（必须包含default），字典的值是数据库配置信息，可以指定多个数据库。指定网站所使用的数据库类型以及连接方式。

- DATABASE_ROUTERS
是一个列表，列表元素是一个实现了特殊路由方法的Python类的路径。数据库路由配置，当执行数据库操作时，Django会根据路由配置选择恰当的数据库执行操作。


### 文件上传
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


### 调试


### HTTP


### 国际化


### 日志


### 模板


### 安全


### URL




## 第三方软件安装

### 数据库
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