# Django RESTful API

现代web开发一般是前后端分离的，后端提供RESTful接口，插件`django-rest-framework`来提供RESTful接口。


在项目设置中要加入：

```python
REST_FRAMEWORK = { 
    'DEFAULT_SCHEMA_CLASS': 'rest_framework.schemas.coreapi.AutoSchema',
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.LimitOffsetPagination',
    'PAGE_SIZE': 3,
    }
```



## 一、Serializer

类似form，作用是序列化数据。

```python
# serializers.py
from rest_framework import serializers, pagination

from .models import Post, Category


class PostSerializer(serializers.ModelSerializer):
    category = serializers.SlugRelatedField(
        read_only=True,
        slug_field='name'
    )
    tag = serializers.SlugRelatedField(
        many=True,
        read_only=True,
        slug_field='name'
    )
    owner = serializers.SlugRelatedField(
        read_only=True,
        slug_field='username'
    )
    created_time = serializers.DateTimeField(format="%Y-%m-%d %H:%M:%S")

    class Meta:
        model = Post
        fields = ['id', 'title', 'category', 'tag', 'owner', 'created_time']



class PostDetailSerializer(PostSerializer):
    class Meta:
        model = Post
        fields = ['id', 'title', 'category', 'tag', 'owner', 'content_html','created_time']



class CategorySerializer(serializers.ModelSerializer):
    class Meta:
        model = Category
        fields = ['id', 'name', 'created_time']


class CategoryDetailSerializer(CategorySerializer):
    posts = serializers.SerializerMethodField('paginated_posts')

    def paginated_posts(self, obj):
        print('paginated_posts')
        posts = obj.post_set.filter(status=Post.STATUS_NORMAL)
        paginator = pagination.PageNumberPagination()
        page = paginator.paginate_queryset(posts, self.context['request'])
        serializer = PostSerializer(page, many=True, context={
            'request': self.context['request']
        })
        return {
            'count': posts.count(),
            'result': serializer.data,
            'previous': paginator.get_previous_link(),
            'next': paginator.get_next_link(),
        }

    class Meta:
        model = Category
        fields = ['id', 'name', 'created_time', 'posts']
```



## 二、API

类似view，作用是接受请求并返回Json格式的响应，一般会提供CRUD的接口，viewsets是提供完整的CRUD接口，其他的还有List、Retrieve等单独的接口。

```python
# apis.py
from rest_framework import generics
from rest_framework import viewsets
from rest_framework.decorators import api_view
from rest_framework.response import Response
from rest_framework.permissions import IsAdminUser

from .models import Post, Category
from .serializers import PostSerializer, PostDetailSerializer, CategorySerializer, CategoryDetailSerializer


@api_view(['GET', 'POST'])
def post_list(request):
    posts = Post.objects.filter(status=Post.STATUS_NORMAL)
    post_serializers = PostSerializer(posts, many=True)
    return Response(post_serializers.data)


class PostList(generics.ListCreateAPIView):
    queryset = Post.objects.filter(status=Post.STATUS_NORMAL)
    serializer_class = PostSerializer


class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.filter(status=Post.STATUS_NORMAL)
    serializer_class = PostSerializer
    # permission_classes = [IsAdminUser]

    def retrieve(self, request, *args, **kwargs):
        self.serializer_class = PostDetailSerializer
        return super().retrieve(request, *args, **kwargs)

    def filter_queryset(self, queryset):
        category_id = self.request.query_params.get('category')
        if category_id:
            queryset = queryset.filter(category_id=category_id)
        return queryset


class CategoryViewSet(viewsets.ReadOnlyModelViewSet):
    serializer_class = CategorySerializer
    queryset = Category.objects.filter(status=Category.STATUS_NORMAL)

    def retrieve(self, request, *args, **kwargs):
        self.serializer_class = CategoryDetailSerializer
        return super().retrieve(request, *args, **kwargs)
    
```



## 三、路由

通过浏览器访问是需要带上`?format=json`的查询参数。

```python
# urls.py
from rest_framework.routers import DefaultRouter
from blog.apis import post_list, PostList, PostViewSet, CategoryViewSet

router = DefaultRouter()
router.register('post', PostViewSet)
router.register('category', CategoryViewSet)

urlpatterns = [
    path('api/post/', post_list, name='post-list'),
    path('api/posts/', PostList.as_view(), name='post-list'),path('apis/', include(router.urls)), 
    path('apis/', include(router.urls)),     
]
```



## 四、文档
django-rest-framework自带了API接口生成器。

```python
# urls.py
from rest_framework.documentation import include_docs_urls

urlpatterns = [
    path('apis/docs/', include_docs_urls(title="袋鼠乐园博客接口")),
]
```
