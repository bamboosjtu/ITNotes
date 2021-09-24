# Django视图


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

- 模板视图
`django.views.generic.TemplateView`

- 列表视图
`django.views.generic.ListView`

- 查询视图
`django.views.generic.edit.DetailView`

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
| template_name | 模板文件名 |
| context_object_name | 上下文对象名 |
| get_context_data() | 获取上下文对象 |
| get_queryset() | 查询模型 |
| as_view() | url的第二个参数 |
