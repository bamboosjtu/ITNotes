# Django Model简介

ORM是代码（软件）层面对于数据库和关系的一种抽象。Django的Model是ORM的一个具体实现。

## 一、字段（Field）
字段类型及参数的官方文档参考[这里](https://docs.djangoproject.com/en/3.2/ref/models/fields/)。

### （一）字段类型

#### 1. 数值型
| Model字段类型 | Python数据类型 | 备注 |
|--------------|--------------|------|
| AutoField | int(11） | 自增主键，Django Model默认提供id字段，但可以重写 |
| BooleanField | tinyint(1) | |
| DecimalField | decimal | 金融常用，需要指定精确到多少位 |
| IntegerField | int(11) | |
| PositiveIntegerField | int(11) | 非负整数 |
| SmallIntegerField | smallint | 小整数 |

#### 2. 字符型
| Model字段类型 | MySQL数据类型 | 备注 |
|--------------|--------------|------|
| CharField | varchar |  |
| TextField | longtext | 常用于存档大量文本 |
| URLField | varchar | 实现了对URL的特殊处理 |
| UUIDField | char(32) | 在PostgreSQL中使用uuid类型 |
| EmailField | varchar | 实现了对email的特殊处理 |
| FileField | varchar | 实现了对文件的特殊处理 |
| ImageField | varchar | 实现了对图片的特殊处理 |

#### 3. 日期型
- DateField
- DateTimeField
- TimeField

#### 4. 关系型
- ForeignKey
- OneToOneField：在外键字段上加unique
- ManyToManyField：会创建中间表


### （二）字段参数
| 参数名称 | 参数说明 |
|---------|--------|
| null | 数据库层面是否允许为空 |
| blank | 业务层面是否允许为空 |
| choices | 设置选项 |
| db_column | 指定Model和数据库表的字段对应关系 |
| db_index | 配置索引 |
| default | 配置默认值 |
| editable | |
| error_messages | 自定义字段值校验失败的异常提示 |
| help_text | 字段提示语 |
| primary_key | 主键，只允许设置一个字段为主键 |
| unique ||
| unique_for_date | |
| unique_for_month | |
| unique_for_year | |
| verbose_name | 后台显示名称 |
| validators | 自定义校验逻辑 |



## 二、模型
一个模型对应一张数据库表，`django.db.models.Model`的内部类`Meta`用于配置模型或者表。

- `ordering`：排序的字段。
- `verbose_name`、`verbose_name_plural`，在后台显示的模型名称。



## 三、QuerySet
数据库有数据操作语言DML，可以通过SQL语句进行CRUD操作，在Models对数据库的查询和更新交互通过QuerySet完成，Models可以看成是中间件，具体操作接口可参考[这里](https://docs.djangoproject.com/en/3.2/ref/models/querysets/)。

QuerySet可进行链式操作，需要时才会真正执行DML语句。

### （一）链式调用接口
- all
- filter
- exclude
- reverse
- distinct
- none


### （二）非链式调用接口
- get：不存在会抛出异常
- create
- update
- delete
- get_or_create
- update_or_create
- count
- latest
- earliest
- first
- last
- exists
- bluk_create
- in_buld
- values
- values_list


### （三）查询操作符
常用于filter接口的参数，*字段名*与*参数*之间通过`__`相连。

- contains
- icontains
- startswith
- istartswith
- endswith
- iendswith
- exact
- iexact
- in
- gt
- lt
- gte
- lte
- range
- count


### （四）特殊接口
- defer：把不需要展示的字段延迟加载。
- only：仅加载所需字段。
- select_related：解决外键产生的N+1问题
- prefetch_related：解决多对多关系产生的N+1问题。


### （五）高级查询
- Q表达式用于OR查询。

- F表达式用来执行数据库层面的计算，从而避免多线程竞争。

- 聚合查询
  - Count
  - Sum
  - Avg
  - Min
  - Max

- annotate：增加临时属性。

- aggregate：直接计算结果。

- raw：原生SQL接口