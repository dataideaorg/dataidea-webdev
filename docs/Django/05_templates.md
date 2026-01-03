# Templates

Learn how to create dynamic HTML pages using Django's template system.

## What are Templates?

Templates are HTML files with special Django syntax that allow you to:
- Display dynamic data
- Use template inheritance
- Include reusable components
- Apply filters and tags

## Template Location

Create templates in your app:

```
myapp/
    templates/
        myapp/
            index.html
            post_detail.html
```

Django looks for templates in:
1. `app/templates/app/` (app-specific)
2. `templates/` (project-wide)

## Basic Template

### Simple Template

```html
<!-- myapp/templates/myapp/index.html -->
<!DOCTYPE html>
<html>
<head>
    <title>My Blog</title>
</head>
<body>
    <h1>Welcome to My Blog</h1>
    <p>This is the home page.</p>
</body>
</html>
```

### Rendering Template

```python
# myapp/views.py
from django.shortcuts import render

def index(request):
    return render(request, 'myapp/index.html')
```

## Template Variables

Display data from views:

### In View

```python
def index(request):
    context = {
        'title': 'Home Page',
        'name': 'John',
        'age': 30,
    }
    return render(request, 'myapp/index.html', context)
```

### In Template

```html
<h1>{{ title }}</h1>
<p>Hello, {{ name }}! You are {{ age }} years old.</p>
```

### Accessing Object Attributes

```python
# View
def post_detail(request, post_id):
    post = get_object_or_404(Post, id=post_id)
    return render(request, 'myapp/post_detail.html', {'post': post})
```

```html
<!-- Template -->
<h1>{{ post.title }}</h1>
<p>{{ post.content }}</p>
<p>Published: {{ post.created_at }}</p>
```

## Template Tags

Special syntax for logic in templates:

### for Loop

```html
<ul>
    {% for post in posts %}
        <li>{{ post.title }}</li>
    {% endfor %}
</ul>
```

### if Statement

```html
{% if user.is_authenticated %}
    <p>Welcome, {{ user.username }}!</p>
{% else %}
    <p>Please log in.</p>
{% endif %}
```

### if-else

```html
{% if post.status == 'published' %}
    <p>This post is published.</p>
{% else %}
    <p>This post is a draft.</p>
{% endif %}
```

### Empty for Loop

```html
{% for post in posts %}
    <p>{{ post.title }}</p>
{% empty %}
    <p>No posts available.</p>
{% endfor %}
```

## Template Filters

Modify variable output:

### Common Filters

```html
<!-- Uppercase -->
{{ name|upper }}

<!-- Lowercase -->
{{ name|lower }}

<!-- Title case -->
{{ title|title }}

<!-- Length -->
{{ posts|length }}

<!-- Date formatting -->
{{ post.created_at|date:"F d, Y" }}

<!-- Truncate text -->
{{ post.content|truncatewords:30 }}

<!-- Default value -->
{{ name|default:"Guest" }}

<!-- Safe (render HTML) -->
{{ content|safe }}
```

### Chaining Filters

```html
{{ name|upper|truncatewords:5 }}
```

## Template Inheritance

Reuse common HTML structure:

### Base Template

```html
<!-- myapp/templates/myapp/base.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{% block title %}My Blog{% endblock %}</title>
    <style>
        /* Common styles */
    </style>
</head>
<body>
    <header>
        <h1>My Blog</h1>
        <nav>
            <a href="/">Home</a>
            <a href="/about/">About</a>
        </nav>
    </header>
    
    <main>
        {% block content %}
        {% endblock %}
    </main>
    
    <footer>
        <p>&copy; 2024 My Blog</p>
    </footer>
</body>
</html>
```

### Child Template

```html
<!-- myapp/templates/myapp/index.html -->
{% extends 'myapp/base.html' %}

{% block title %}Home - My Blog{% endblock %}

{% block content %}
    <h2>Latest Posts</h2>
    {% for post in posts %}
        <article>
            <h3>{{ post.title }}</h3>
            <p>{{ post.get_excerpt }}</p>
            <a href="{% url 'post_detail' post.id %}">Read more</a>
        </article>
    {% endfor %}
{% endblock %}
```

## Including Templates

Reuse template components:

### Component Template

```html
<!-- myapp/templates/myapp/post_card.html -->
<div class="post-card">
    <h3>{{ post.title }}</h3>
    <p>{{ post.get_excerpt }}</p>
    <small>{{ post.created_at|date:"M d, Y" }}</small>
</div>
```

### Include in Main Template

```html
{% for post in posts %}
    {% include 'myapp/post_card.html' %}
{% endfor %}
```

## URL Tag

Generate URLs in templates:

```html
<!-- Using URL name -->
<a href="{% url 'post_detail' post.id %}">Read more</a>

<!-- With namespace -->
<a href="{% url 'blog:post_detail' post.id %}">Read more</a>

<!-- With multiple arguments -->
<a href="{% url 'post_archive' year=2024 month=1 %}">Archive</a>
```

## Static Files

Include CSS, JavaScript, and images:

### Settings

```python
# settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']
```

### In Template

```html
{% load static %}

<link rel="stylesheet" href="{% static 'css/style.css' %}">
<script src="{% static 'js/main.js' %}"></script>
<img src="{% static 'images/logo.png' %}" alt="Logo">
```

## Complete Example

### Base Template

```html
<!-- myapp/templates/myapp/base.html -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>{% block title %}My Blog{% endblock %}</title>
    {% load static %}
    <link rel="stylesheet" href="{% static 'css/style.css' %}">
</head>
<body>
    <header>
        <nav>
            <a href="{% url 'post_list' %}">Home</a>
            <a href="{% url 'about' %}">About</a>
        </nav>
    </header>
    
    <main>
        {% block content %}
        {% endblock %}
    </main>
    
    <footer>
        <p>&copy; 2024 My Blog</p>
    </footer>
</body>
</html>
```

### Post List Template

```html
<!-- myapp/templates/myapp/post_list.html -->
{% extends 'myapp/base.html' %}

{% block title %}Posts - My Blog{% endblock %}

{% block content %}
    <h1>Latest Posts</h1>
    
    {% if posts %}
        <div class="post-list">
            {% for post in posts %}
                <article class="post-card">
                    <h2><a href="{% url 'post_detail' post.id %}">{{ post.title }}</a></h2>
                    <p class="meta">
                        Published: {{ post.created_at|date:"F d, Y" }}
                        by {{ post.author.username }}
                    </p>
                    <p>{{ post.get_excerpt }}</p>
                    <a href="{% url 'post_detail' post.id %}">Read more →</a>
                </article>
            {% endfor %}
        </div>
    {% else %}
        <p>No posts available.</p>
    {% endif %}
{% endblock %}
```

### Post Detail Template

```html
<!-- myapp/templates/myapp/post_detail.html -->
{% extends 'myapp/base.html' %}

{% block title %}{{ post.title }} - My Blog{% endblock %}

{% block content %}
    <article>
        <h1>{{ post.title }}</h1>
        <p class="meta">
            Published: {{ post.created_at|date:"F d, Y" }}
            by {{ post.author.username }}
        </p>
        <div class="content">
            {{ post.content|linebreaks }}
        </div>
        <a href="{% url 'post_list' %}">← Back to posts</a>
    </article>
{% endblock %}
```

## Template Context Processors

Add data to all templates automatically:

```python
# settings.py
TEMPLATES = [
    {
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

This makes `request` and `user` available in all templates.

## Best Practices

1. **Use template inheritance:** Avoid repeating HTML
2. **Keep logic in views:** Templates should display, not process
3. **Use includes:** For reusable components
4. **Organize templates:** Group by app
5. **Use URL names:** Makes URLs maintainable
6. **Load static files:** Use `{% load static %}`

## Common Mistakes

### 1. Not Extending Base Template

```html
<!-- ❌ Wrong - repeating HTML -->
<!DOCTYPE html>
<html>
<head>...</head>
<body>...</body>
</html>

<!-- ✅ Correct -->
{% extends 'myapp/base.html' %}
{% block content %}...{% endblock %}
```

### 2. Forgetting to Load Static

```html
<!-- ❌ Wrong -->
<link rel="stylesheet" href="/static/css/style.css">

<!-- ✅ Correct -->
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

### 3. Logic in Templates

```html
<!-- ❌ Wrong - complex logic in template -->
{% for post in posts %}
    {% if post.status == 'published' and post.created_at > yesterday %}
        ...
    {% endif %}
{% endfor %}

<!-- ✅ Correct - filter in view -->
# In view:
posts = Post.objects.filter(status='published', created_at__gte=yesterday)
```

## Practice Exercise

Create templates for:

1. Base template with header, navigation, and footer
2. Home page listing all posts
3. Post detail page showing full post
4. About page
5. Use template inheritance
6. Include static CSS file
7. Use URL tags for navigation

## What's Next?

Now that you understand templates, learn to:

- **Handle Forms** - Process user input
- **User Authentication** - Login, logout, registration
- **Admin Interface** - Customize Django admin
- **Deploy Your App** - Put your site online

---

**Previous Tutorial:** [Views and URLs](04_views_urls.md)  
**Next Tutorial:** [Forms](06_forms.md)

