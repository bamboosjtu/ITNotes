# Django管理后台

管理后台集成自`django.contrib.admin.ModelAdmin`类，通过`@admin.register(<modelname>)`将数据模型注册到管理后台上，从而进行数据库的增删改查。


## 属性
### 列表页
- list_display：配置列表页所展示的字段。

- list_display_links：配置那些字段可作为链接。

- list_filter：配置右侧的过滤器使用的字段，可以通过集成`django.contrib.admin.SimpleListFilter`自定义过滤器。
    - title：显示过滤器标题
    - parameter_name：查询时URL参数的名字
    - `lookups(self, request, model_admin)`
    - `queryset(self, request, queryset)`：根据URL Query的内容返回列表页数据。

- search_fields：配置上方的搜索栏使用的字段。

- actions_on_top：配置上方的操作栏是否显示。

- actions_on_bottom：配置下方的操作栏是否显示。



### 添加页及修改页
- fields：新增页所需填写的属性。

- save_on_top：上方的操作栏是否显示。



## 方法
- `save_model(self, request, obj, form, change)`：点击保存按钮后，数据库操作前的一些处理，obj是当前要保存的对象，form是页面提交过来的表单，change标志本次保存的数据是新增的还是更新的。

- `<operator>(self, obj)`：自定义操作，需要通过`django.utils.html.format_html`返回HTML，可用于后台展示。
    - short_description：显示名称。