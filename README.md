# ITNotes

## Web
### 前端
    - Vue.js


### 后端
    - Django(Python)
    - Express(Node)


## 数据库

### NoSQL
#### 文档数据库
- [MongoDB](https://www.mongodb.com/)：提供JSON格式的数据，默认端口27017。
    - [Robo 3T](https://robomongo.org/)：MongoDB的GUI工具

#### K-V数据库
- [Memcached](https://memcached.org/)：主要用于缓存数据请求，在内存中快速存取，但对复杂数据类型的支持比较有限，支持分布式。
- [Cassandra](https://cassandra.apache.org/)：支持集群和ad hoc，但对复杂数据结构支持有限，
- [Redis](https://redis.io/)：支持持久性存储，仅用于单机？


## DevOps
- 版本管理
    - 代码及其分支管理
    - 数据库模式和数据管理
    - 配置文件管理
    - 依赖关系管理


### 数据库管理
数据库迁移工具有：
- Migration（Ruby on Rails）
- south（Django）
- Migrations Plugin（CachePHP）
- Evolution（Play Framework）
- Flyway
- Liquibase
- dbdeploy


### 依赖管理
- JVM语言:Maven（中央仓库）、Sonatype（中央仓库镜像）
    - Apache Ant
    - Maven
    - sbt
    - Gradle
- CPAN：Perl
- PyPI：Python
- RubyGems：Ruby
- npm：Node.js


### 缺陷管理
一般还具备bug管理、代码管理、Wiki等功能。

- [Trac](https://trac.edgewall.org/)：基于Python。
- [Redmine](https://www.redmine.org/)，基于Ruby on Rails。
- [Bugzilla](https://www.bugzilla.org/)：基于Perl。
- [Mantis](https://www.mantisbt.org/)：基于PHP。
- 商用产品：`JIRA`、`YouTRACK`、`Pivotal Tracker`、`Backlog`、`GITHUB`等SaaS产品。