# Django视图

Django的视图主要分为`function view`和`class-base view`。

View处理请求的逻辑：
1.调用dispatch进行分发

2.调用get/post等方法

    1. 调用get_queryset方法，拿到数据源

    2. 调用get_context_data方法，拿到上下文数据

        1. 调用get_paginate_by拿到每页数据

        2. 调用get_context_object_name拿到上下文中queryset数据的名称

        3. 调用paginate_queryset进行分页处理

        4. 将拿到的数据转为dict返回

    3. 调用render_to_response渲染页面

        1. 调用get_template_names获取模板名
        
        2. 把request, context, template_name传递到模板中


## 一、视图基础
### （一）快捷方式
- `render_to_string(template_name, context)`

- `render(request, template_name, context, content_type, status, using=None)`

- `redirect(to, premanent=False)`

- `get_object_or_404`、`get_list_or_404`
从模型中提取数据，如果数据不存在，则抛出HTTP404异常。


### （二）装饰器
装饰器是立即执行的。

限制HTTP方法
- require_http_methods(['GET', 'POST'])
- require_GET()
- require_POST()
- require_safe()


`django.views.decorators.gzip`：GZip是目前Internet上非常流行的数据压缩格式，通过GZip装饰器可以改善网页访问速度。


决定是否使用缓存
- `django.views.decorators.vary_on_headers`
- `django.views.decorators.vary_on_cookie`


缓存控制(`django.views.decorators.cache`)：
- cache_control()
- never_cache


### （三）预置视图
- 查看静态文件
`django.views.static.serve`视图可以用来查看任意路径下的文件，例如用户上传完成后，使用serve视图来查看文件是否保存成功。
`static.serve(request, path, document_root, show_indexes=False)`

- 页面不存在
`django.views.defaults.page_not_found(request, exception, template_name='404.html')`

- 服务器内部错误
`django.views.defaults.server_error(request, template='500.html')`

- 无访问权限
`django.views.defaults.permission_denied(request, template='403.html')`

- 请求无效
`django.views.defaults.bad_request(request, template='400.html')`



## 二、请求与响应
### （一）请求

#### HttpRequest属性

| HTTP请求属性 | 说明 |
|--------|------|
| scheme | 请求所用网络协议，http或https |
| method | 请求所用的方法，GET或POST等 |
| body | HTTP请求的body部分 |
| path | 全路径 |
| path_info | URL主机名后面的内容 |
| encoding | 表单提交数据的编码类型，可修改 |
| content_type | MIME类型 |
| content_params | CONTENT_TYPE头的值，格式为字典 |
| GET | 所有GET参数，格式为字典 |
| POST | 所有POST参数，格式为字典 |
| COOKIES | 所有cookie，格式为字典，key和value均为字符串 |
| FILES | 被上传的文件，格式为字典，key是input控件的name，value是UploadedFile对象 |
| META | HTTP头，格式为字典 |


#### 中间件属性

| 中间件请求属性 | 说明 | 中间件 |
|---------------|------|-------|
| session | 当前session的信息 | SessionMiddleware |
| site | 当前网站信息的属性 | CurrentSiteMiddleware |
| user | 当前用户的属性 | AuthenticationMiddleware |


#### HttpRequest方法

| HTTP请求方法 | 说明 |
|-------------|------|
| get_host | 取得HTTP_X_FORWARDED_HOST和HTTP_HOST的值 |
| get_port | 取得网站端口号 |
| get_full_path | 返回URL主机名后的全部信息 |
| build_absolute_uri | 根据location返回URI |
| get_signed_cookie | 取得一个已签名的cookie的值，还可以加盐 |
| is_secure | 是否启用HTTPS协议 |
| is_ajax | 是否通过XMLHttpRequest对象 |



### （二）响应
#### HttpResponse属性

| HTTP响应属性 | 说明 |
|--------|------|
| content | 内容 |
| charset | 编码格式 |
| status_code | 状态码 |
| reason_phrase | 状态说明 |
| streaming | 永远为False，用于中间件处理流响应 |
| closed | 如果响应关闭则返回True |


#### HttpResponse方法

| HTTP响应方法 | 说明 |
|--------|------|
| __getitem__ | 获取HTTP头 |
| __setitem__ | 设置HTTP头 |
| __delitem__ | 删除HTTP头 |
| has_header | 判断HTTP头是否存在 |
| setdefault | 设置HTTP头 |
| set_cookie | 设置cookie |
| set_signed_cookie | 设置cookie并加密 |
| delete_cookie | 删除cookie |
| write | 添加content |
| flush |  |
| tell |  |
| getValue |  |
| readable |  |
| seekable |  |
| writable |  |
| writelines |  |


#### HTTPReponse子类
- HttpResponseRedirect
请求跳转到其他地址，状态码为301。

- HttpResponsePermanentRedirect
请求跳转到其他地址，状态码为302。

- HttpResponseNoteModified
页面没有变化，可以使用缓存，状态码为304。

- HttpResponseBadRequest
状态码为400。

- HttpResponseGone
状态码401。

- HttpResponseNotFound
状态码404。

- HttpResponseForbidden
状态码403。

- HttpResponseNotAllowed
状态码405。

- HttpResponseServerError
状态码500。


### （三）模板响应
TemplateResponse为保留模板和上下文，需要输出时才将模板编译成HTML文档，它的基类是SimpleTemplateResponse，模块为`django.template.response`。

触发渲染：
- 明确调用render方法
- 为content属性赋值
- 通过template response中间件之后，response中间件之前


TemplateResponse还可以注册回调函数，回调函数在模板渲染结束后立即执行。


### （四）文件上传
`forms.FileField`，只有POST请求才会触发文件上传动作，用于文件上传操作的表单元素需要包含enctype="multipart/form-data"属性。


```python
# 多文件上传
from django.views.generic.edit import FormView

class FileFieldForm(forms.Form):
    file_field = forms.FileField(widget=forms.ClearableFileInput(attrs={'multiple': True}))

class FileFieldView(FormView):
    form_class = FileFieldForm
    template_name = 'multyupload.html'
    success_url = '/blog/success/files'

    def post(self, request, *args, **kwargs):
        form_class = self.get_form_class()
        form = self.get_form(form_class)
        files = request.FILES.getlist('file_field')
        if form.is_valid():
            for f in files:
                handle_upload_file(f)
            return self.form_valid(form)
        else:
            return self.form_invalid(form)

    def form_valid():
        return super().form_valid(form)
```



## 四、视图类

代码的逻辑被重复使用，且数据需要被共享时，可以考虑使用视图类。

- 视图类
`django.views.View`，能够接受请求并返回响应的可调用对象，实现了基于HTTP方法的分发逻辑，需要自行实现get方法或post方法。

- 模板视图
`django.views.generic.TemplateView`，继承自View，可以直接用来返回指定模板，实现了get方法，可以传递变量到模板中来进行数据展示。

- 列表视图
`django.views.generic.ListView`，继承自View，实现了get方法，可以绑定模板来批量获取数据。自带paginator组件，通过paginate_by属性设置每一个条目数，为上下文提供一个page_obj属性供模板渲染。

- 详情视图
`django.views.generic.edit.DetailView`，继承自View，实现了get方法，可以绑定模板来获取单个实例的数据，需要路由提供pk参数。

- 提交视图
`django.views.generic.edit.CreateView`

- 删除视图
`django.views.generic.edit.DeleteView`

- 更新视图
`django.views.generic.edit.UpdateView`

- 表单视图
`django.views.generic.edit.FormView`


| 通用视图属性&方法 | 说明 |
|-------------|------|
| model | 使用的模型 |
| queryset | 与model二选一，设定基础的数据集，相比model有过滤功能 |
| kwargs | 路由传递的参数字典 |
| pk_url_kwarg | DetailView需要的pk参数的别名 |
| template_name | 模板文件名 |
| context_object_name | 上下文对象名 |
| get_context_data() | 获取上下文对象，如果有新增数据需要传递到模板中，可以重写本方法 |
| get_queryset() | 查询模型，如果设定了queryset会直接返回queryset |
| get_object() | 根据URL参数，从queryset上获取对应的实例 |
| as_view() | url的第二个参数，提供视图函数 |


```python
# 视图类的伪代码
class View:
    @classmethod
    def as_view(cls, **initkwargs):
        def view(request, *args, **kwargs):
            self = cls(**initkwars)
            handler = getattr(self, request.method.lower())
            if handler:
                return handler(request)
            else:
                raise Exception('Method Not Allowed!)
        return view
```
