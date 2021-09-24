# Django模板

## 模板引擎
- Django Template Language
- Jinjia



## 模板使用
加载模板：
- get_template(template_name, using=None)
- select_template(template_name_list, using=None)

模板渲染：
- render



## 模板语法

标签和过滤器都可以自定义，放在应用的templatetags目录下。

- 变量

- 过滤器
add、capfirst、center、cut、date、default、escape、filesizeformat、join、length、linenumbers、truncatewords、upper。

- 标签
block、comment、cycle、extends、for、if、include、load、now、url、with。

- 人性化语义标签
先在INSATLLED_APPS中注册`django.contrib.humanize`，apnumber、intcomma、intword、naturalday、naturaltime、ordinal。

