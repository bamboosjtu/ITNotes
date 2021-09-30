# Django管理后台

管理后台集成自`django.contrib.admin.ModelAdmin`类，通过`@admin.register(<modelname>, [site])`将数据模型注册到管理后台上，从而进行数据库的增删改查，
site可以通过`django.contrib.admin.AdminSite`进行自定义。

admin是基于Django内置功能开发的，结合了Template、Form、Model和View这些模块，也是MTV模式。


## 页面
### 列表页
- list_display：配置列表页所展示的字段。

- list_display_links：配置那些字段可作为链接。

- list_filter：配置右侧的过滤器使用的字段，可以通过继承`django.contrib.admin.SimpleListFilter`自定义过滤器。
    - title：显示过滤器标题
    - parameter_name：查询时URL参数的名字
    - `lookups(self, request, model_admin)`：配置过滤器选项。
    - `queryset(self, request, queryset)`：根据URL查询过滤列表页数据。

- search_fields：配置上方的搜索栏使用的字段。

- actions_on_top：配置上方的操作栏是否显示。

- actions_on_bottom：配置下方的操作栏是否显示。



### 编辑页
- exclude: 编辑页不需填写的字段。

- fields：编辑页所需填写的字段，不能与fieldsets同时设置。

- fieldsets：用于控制页面布局，格式为有两个元素的元组列表，`((名称, {内容}),(名称, {内容}))`，内容的Key有fields、description、classes等。

- save_on_top：上方的操作栏是否显示。

- filter_horizontal：针对多对多字段，设置那些字段横向展示。

- filter_vertical：针对多对多字段，设置那些字段纵向展示。

- form：通过继承`django.forms.ModelForm`自定义表单控件，只需要配置非默认的字段。

- inlines：通过继承`admin.TabularInline`，配置可编辑的关联数据。
    - fields：关联数据可编辑的字段
    - extra：可额外编辑的数量。
    - model：关联数据模型




## 交互
- `save_model(self, request, obj, form, change)`：点击保存按钮后，数据库操作前的一些处理，obj是当前要保存的对象，form是页面提交过来的表单，change标志本次保存的数据是新增的还是更新的。

- `get_queryset(self, request)`：获取管理后台展示的数据。

- `<operator>(self, obj)`：自定义操作，需要通过`django.utils.html.format_html`返回HTML，可用于后台展示。
    - short_description：显示名称。

- `has_add_permission(self, request)`：判断是否有新增数据的权限。

- `has_change_permission(self, request)`：判断是否有修改数据的权限。

- `has_delete_permission(self, request)`：判断是否有删除数据的权限。

- `has_module_permission(self, request)`：判断是否有查询数据的权限。




## 静态资源
通过`Media`内部类自定义静态资源，为管理后台引入JavaScript和CSS资源。

```python
class PostAdmin(admin.ModelAdmin):
    # 省略其他代码
    class Media:
        css = {
            'all': ('pretty.css',)
        }
        js = ('animations.js', 'actions.js')
```




## 日志
ModelAdmin自带日志记录功能，新建或修改实体时，ModelAdmin都会帮忙调用`django.contrib.admin.models.LogEntry`来创建一条日志，记录变更，具体代码位于`django/contrib/admin/options.py`。

- `log_addition(self, request, object, message)`：记录新增
- `log_change(self, request, object, message)`：记录修改