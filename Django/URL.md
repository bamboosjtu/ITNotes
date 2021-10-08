# Django路由

## 一、处理HTTP的流程
1. 根据settings.py中ROOT_URLCONF的设置，确定URL根配置位置。

2. 加载配置信息，查找urlpatterns。

3. 按顺序检索Urlpatterns中的所有URL模式字符串，并定位在第一个与URL匹配的URL模式字符串。

4. 检索到匹配的URL字符串后，调用对应的视图方法，并传递参数给视图。

5. 如果没有找到，会调用一个用于处理错误信息的视图。


## 二、URL参数类型转换
- str
匹配任意非空字符串，但是不能匹配URL分隔符`/`。

- int
匹配任何大于等于0的整数。

- slug
匹配任意适合做网站连接的字符串，slug字符串可以包含任意ascii字符、数字、`-`和`_`。

- uuid
匹配UUID字符串（字母必须为小写）。

- path
匹配任意非空字符串，包括URL分隔符`/`。

- 用户自定义
使用`django.urls.register_converter`来注册转换器至于URLConf。