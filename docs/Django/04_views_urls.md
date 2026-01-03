# Views and URLs

Learn how to create views that handle user requests and configure URL routing in Django.

## What are Views?

Views are Python functions or classes that:
- Receive web requests
- Process data (often from models)
- Return HTTP responses (HTML, JSON, etc.)

Views are the "controller" in Django's MVC pattern.

## Function-Based Views

Simple views written as functions:

```python
# myapp/views.py
from django.http import HttpResponse
from django.shortcuts import render

def index(request):
    return HttpResponse("Hello, World!")

def about(request):
    return HttpResponse("About Page")
```

### Request Object

The `request` parameter contains information about the HTTP request:

```python
def my_view(request):
    # Request method (GET, POST, etc.)
    method = request.method
    
    # GET parameters
    name = request.GET.get('name', 'Guest')
    
    # POST data
    if request.method == 'POST':
        email = request.POST.get('email')
    
    # User information
    user = request.user
    
    return HttpResponse(f"Hello, {name}")
```

## URL Configuration

Map URLs to views:

### App URLs

```python
# myapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.index, name='index'),
    path('about/', views.about, name='about'),
]
```

### Include in Project URLs

```python
# myproject/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('myapp.urls')),
]
```

## URL Patterns

### Basic Patterns

```python
urlpatterns = [
    path('', views.home),              # /
    path('about/', views.about),       # /about/
    path('contact/', views.contact),   # /contact/
]
```

### URL Parameters

Capture values from URLs:

```python
# myapp/urls.py
urlpatterns = [
    path('post/<int:post_id>/', views.post_detail),
    # Matches: /post/123/
    # post_id = 123
]

# myapp/views.py
def post_detail(request, post_id):
    return HttpResponse(f"Post ID: {post_id}")
```

### Multiple Parameters

```python
urlpatterns = [
    path('post/<int:year>/<int:month>/', views.post_archive),
    # Matches: /post/2024/01/
]

def post_archive(request, year, month):
    return HttpResponse(f"Archive: {year}/{month}")
```

### String Parameters

```python
urlpatterns = [
    path('user/<str:username>/', views.user_profile),
    # Matches: /user/john/
]

def user_profile(request, username):
    return HttpResponse(f"User: {username}")
```

### Slug Parameters

```python
urlpatterns = [
    path('post/<slug:slug>/', views.post_detail),
    # Matches: /post/my-first-post/
]

def post_detail(request, slug):
    return HttpResponse(f"Post: {slug}")
```

## URL Names

Give URLs names for easy referencing:

```python
# myapp/urls.py
urlpatterns = [
    path('', views.index, name='index'),
    path('about/', views.about, name='about'),
    path('post/<int:post_id>/', views.post_detail, name='post_detail'),
]
```

### Reverse URLs

Get URL from name:

```python
from django.urls import reverse

# In views
url = reverse('post_detail', args=[123])
# Returns: '/post/123/'

# In templates
{% url 'post_detail' post.id %}
```

## Rendering Templates

Return HTML instead of plain text:

```python
# myapp/views.py
from django.shortcuts import render

def index(request):
    return render(request, 'myapp/index.html')

def post_detail(request, post_id):
    context = {
        'post_id': post_id,
        'title': 'My Post',
    }
    return render(request, 'myapp/post_detail.html', context)
```

### Template Location

Create templates in:
```
myapp/
    templates/
        myapp/
            index.html
            post_detail.html
```

## Passing Data to Templates

### Using Context Dictionary

```python
def index(request):
    context = {
        'title': 'Home Page',
        'posts': Post.objects.all(),
        'user': request.user,
    }
    return render(request, 'myapp/index.html', context)
```

### Using locals()

```python
def index(request):
    title = 'Home Page'
    posts = Post.objects.all()
    return render(request, 'myapp/index.html', locals())
```

## Class-Based Views

More powerful, reusable views:

### ListView

Display a list of objects:

```python
# myapp/views.py
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'myapp/post_list.html'
    context_object_name = 'posts'
    paginate_by = 10
```

### DetailView

Display a single object:

```python
from django.views.generic import DetailView

class PostDetailView(DetailView):
    model = Post
    template_name = 'myapp/post_detail.html'
    context_object_name = 'post'
```

### URL Configuration for Class Views

```python
# myapp/urls.py
from django.urls import path
from .views import PostListView, PostDetailView

urlpatterns = [
    path('posts/', PostListView.as_view(), name='post_list'),
    path('post/<int:pk>/', PostDetailView.as_view(), name='post_detail'),
]
```

## HTTP Methods

### Handling GET and POST

```python
def contact(request):
    if request.method == 'POST':
        # Process form submission
        name = request.POST.get('name')
        email = request.POST.get('email')
        message = request.POST.get('message')
        
        # Process data...
        
        return HttpResponse("Thank you for your message!")
    else:
        # Display form
        return render(request, 'myapp/contact.html')
```

## Redirects

Redirect to another URL:

```python
from django.shortcuts import redirect
from django.urls import reverse

def my_view(request):
    # Redirect to URL
    return redirect('/about/')
    
    # Redirect using name
    return redirect('about')
    
    # Redirect with reverse
    return redirect(reverse('post_detail', args=[123]))
```

## Complete Examples

### Simple Blog Views

```python
# myapp/views.py
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    posts = Post.objects.filter(status='published').order_by('-created_at')
    context = {
        'posts': posts,
    }
    return render(request, 'myapp/post_list.html', context)

def post_detail(request, post_id):
    post = get_object_or_404(Post, id=post_id, status='published')
    context = {
        'post': post,
    }
    return render(request, 'myapp/post_detail.html', context)
```

### URL Configuration

```python
# myapp/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
    path('post/<int:post_id>/', views.post_detail, name='post_detail'),
]
```

### get_object_or_404

Safely get object or return 404:

```python
from django.shortcuts import get_object_or_404

# Instead of:
try:
    post = Post.objects.get(id=post_id)
except Post.DoesNotExist:
    return HttpResponseNotFound()

# Use:
post = get_object_or_404(Post, id=post_id)
```

## URL Namespaces

Organize URLs when using multiple apps:

```python
# myapp/urls.py
from django.urls import path
from . import views

app_name = 'blog'

urlpatterns = [
    path('', views.index, name='index'),
]

# Usage:
# {% url 'blog:index' %}
# reverse('blog:index')
```

## Best Practices

1. **Use URL names:** Makes URLs maintainable
2. **Organize views:** Group related views together
3. **Use get_object_or_404:** Better error handling
4. **Separate GET and POST:** Clear logic separation
5. **Use class-based views:** For common patterns
6. **Keep views thin:** Move logic to models or separate functions

## Common Mistakes

### 1. Forgetting to Include URLs

```python
# ❌ Wrong
# Created myapp/urls.py but didn't include in project urls.py

# ✅ Correct
# myproject/urls.py
urlpatterns = [
    path('', include('myapp.urls')),
]
```

### 2. Wrong URL Pattern

```python
# ❌ Wrong
path('post/<int:post_id>', views.post_detail),  # Missing trailing slash

# ✅ Correct
path('post/<int:post_id>/', views.post_detail),
```

### 3. Not Using get_object_or_404

```python
# ❌ Wrong
post = Post.objects.get(id=post_id)  # Raises exception if not found

# ✅ Correct
post = get_object_or_404(Post, id=post_id)  # Returns 404 if not found
```

## Practice Exercise

Create views and URLs for:

1. Home page view that lists all posts
2. Post detail view that shows a single post
3. About page view
4. Contact page view (GET shows form, POST processes it)
5. URL patterns with proper names
6. Use get_object_or_404 for detail views

## What's Next?

Now that you understand views and URLs, learn to:

- **Create Templates** - Build HTML pages with Django template language
- **Work with Forms** - Handle user input
- **Use Template Inheritance** - Reuse HTML structure
- **Add Static Files** - Include CSS and JavaScript

---

**Previous Tutorial:** [Models and Databases](03_models_databases.md)  
**Next Tutorial:** [Templates](05_templates.md)

