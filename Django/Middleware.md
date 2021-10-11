# Django中间件

Django的中间件在项目启动时会被初始化，等接受请求后，会根据settings中的MIDDLEWARE配置顺序挨个调用，传递request作为参数。

## 一、中间件示例
可以在应用目录下的middleware文件夹或middlewares.py自定义中间件，如

### （一）新模式

```shell
blog
├── middleware
    ├── __init__.py
    └── user_id.py
```


```python
# user_id.py
# 访问统计中间件
import uuid

USER_KEY = 'uid'
TEN_YEARS = 60*60*24*365*10


class UserMiddleware:
    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        uid = self.generate_uid(request)
        request.uid = uid
        response = self.get_response(request)
        response.set_cookie(USER_KEY, uid, max_age=TEN_YEARS, httponly=True)
        return response

    def generate_uid(self, request):
        try:
            uid = request.COOKIES[USER_KEY]
        except KeyError:
            uid = uuid.uuid4().hex()
        return uid
```



### （二）旧模式
```python
# 统计访问速度
import time
from django.http import response
from django.urls import reverse
from django.utils.deprecation import MiddlewareMixin

class TimeItMiddleware(MiddlewareMixin):
    def process_request(self, request):
        self.start_time = time.time()
        return None

    def process_view(self, request, func, *args, **kwargs):
        if request.path != reverse('index'):
            return None

        start = time.time()
        response = func(request)
        costed = time.time() - start
        print('process view: {:.2f}'.format(costed))
        return response

    def process_exception(self, request, exception):
        pass

    def process_template_response(self, request, response):
        costed = time.time() - self.start_time
        print('render cost: {:.2f}'.format(costed))
        return response

    def process_response(self, request, response):
        costed = time.time() - self.start_time
        print('request to response cost: {:.2f}'.format(costed))
        return response
```